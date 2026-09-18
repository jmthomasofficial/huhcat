# HUHCAT — VAULT VERIFICATION RECORD

**As-of:** 2026-09-17 ~11:00 UTC
**Analyst:** Ghost (`jmxghost` lane)
**Trigger:** deployer published source at `github.com/weareallgoingtomake1t/huhcat`
**Method:** cloned source, read every program module, then compared against live mainnet state byte-for-byte.
**Not financial advice.**

---

## 0. CORRECTION TO MY OWN PRIOR REPORT

Last night I wrote, in `BRIEF-2026-09-17.md`:

> "The vault program is **upgradeable**. Upgrade authority = the same dev wallet. A lock you don't control is a lock someone else controls."

**That was wrong.** I inferred it from a hand-rolled byte-offset parse of the ProgramData account, and I misread the account layout.

**The actual bug — and it is a classic one:** the `UpgradeableLoaderState::ProgramData` layout is

```
offset  0..4     enum tag        (3 = ProgramData)
offset  4..12    slot            (u64, last write)
offset 12..13    authority Option discriminant   <-- I SKIPPED THIS
offset 13..45    authority pubkey (32 bytes)
offset 45..      ELF
```

My first parse read bytes `13..45`, saw 32 non-zero bytes, and printed them as a live authority. **I never read the discriminant byte at offset 12 that says whether those 32 bytes mean anything.** When the authority is `None` (tag `0x00`), the loader **leaves the old pubkey bytes sitting in place** as a stale remnant — they are ignored by every parser, but they are still physically present in the account.

So the bytes were never wrong. My read of them was: I read a payload without reading its discriminant.

**Corrected, and this time verified against a control group at the byte level:**

```
                     tag@12   bytes 13:45        RPC authority       verdict
Jupiter   programdata  0x01   CvQZZ23qYDWF…      CvQZZ23qYDWF…       AGREE (Some)
PumpSwap  programdata  0x01   7gZufwwAo17y…      7gZufwwAo17y…       AGREE (Some)
HUHCAT    programdata  0x00   9AgnpU9ZspPt…      None                AGREE (None wins)
                               ^ stale remnant
```

Two programs that demonstrably *have* authorities report tag `0x01` with the pubkey matching RPC exactly. The vault reports tag `0x00` and RPC says `None` — and the same stale pubkey still sits in the bytes. **The tag is authoritative; the payload bytes are not.**

**And the finalize transaction settles it beyond argument:**

```
sig 3yQBPatumyzK63pZJd2JAWcscsSditgnk8UPGBacRcLttGzPRJ91TLNGjxSPK4jGKkGT1BrZRWiQUxPFthpVaKCv
slot 447681940  (3 slots after deploy, 02:30:50 UTC)
ix: setAuthority
    { "account": "DPAM4ZwLrBCRwVu2sqw2HRunJSkmdnExhuE5tp8dD2Gs",
      "authority": "9AgnpU9ZspPtUccPHx2BtAsPWjNFo6Vd1wKbzqhiHRm9",
      "newAuthority": null }
```

**The deployer explicitly set the upgrade authority to `null` three slots after deploying.** That is the `--final` flag doing its job, signed and on-chain, publicly visible.

**The deployer's claim "burned upgrade key" is TRUE. The vault program is immutable.** ✅

I state this plainly because it cuts against my own prior finding: I told you a lock had a key. It does not.

*Lesson recorded: when parsing a serialized enum containing an Option, read the discriminant before the payload. Never publish a load-bearing claim derived from raw byte offsets without a known-positive control test. Use the parser the protocol itself ships (`jsonParsed`), or the official CLI.*

---

## 1. THE SOURCE MATCHES THE DEPLOYED BINARY — EXACTLY

The deployer's README claims you can verify this yourself. I did.

```
on-chain ELF length  : 105,272 bytes
committed .so length : 105,272 bytes
sha256 (on-chain)    : bbc47f545456ff99266f5c0aa9aa574493b27be84e6bc2ffaece559cb492367c
sha256 (committed)   : bbc47f545456ff99266f5c0aa9aa574493b27be84e6bc2ffaece559cb492367c
README's stated hash : bbc47f545456ff99266f5c0aa9aa574493b27be84e6bc2ffaece559cb492367c
```

**Byte-identical. All three agree.** This is the equivalent of a verified build, done by hand — and it's stronger than most "verified" stamps, because it's a direct byte comparison rather than a metadata attestation.

> Note for anyone reproducing: the README's two commands differ in one respect — `solana program dump` writes the ELF without trailing padding, so a plain `sha256` on the dumped file matches. If you pull the account via raw RPC you must strip the ProgramData header (45 bytes) and trailing nulls. I did both; both agree.

---

## 2. WHAT THE PROGRAM ACTUALLY IS (read line by line, then confirmed on-chain)

Native Rust (not Anchor). **Three instructions. That is the entire attack surface:**

| Tag | Instruction | Effect |
|---|---|---|
| `0x00` + u64 | `Initialize` | One-time. Seals setup, moves deed in. Cannot re-run (checks `VaultAlreadyExists`). |
| `0x01` | `Claim` | Lock exactly `required` coin → receive the 1/1 deed. |
| `0x02` | `Return` | Give the deed back → receive **every** locked coin. |

**There is no admin instruction. No close. No pause. No withdraw-to-team. No set-authority. No arbitrary CPI.** The program has no path to move value anywhere except between a claimant and the vault.

### The guardrails that matter (`checks.rs`)

- `assert_sealed_deed` — refuses unless the deed mint has **supply == 1, decimals == 0, and null mint AND freeze authority**.
- `assert_allowed_extensions` — **only** `MetadataPointer` and `TokenMetadata` may be present, on *both* mints. This explicitly blocks transfer fees, transfer hooks, permanent delegates and close authorities — the exact extensions that could drain, freeze or destroy what the vault holds. This is a thoughtful check; most projects would not have written it.
- `assert_token_account_for` — every token account is verified to belong to the declared mint.
- `AccountAliasing` guard — a claimant cannot name the vault's own accounts (closes the Token-2022 self-transfer no-op hole).
- `create_pda_account` — handles pre-funded addresses so the vault can't be griefed into an uncreatable state.
- All vault token accounts carry the **ImmutableOwner** extension and are PDAs; only the program can sign for them.

### The one thing I checked hardest, because it's the real risk

`Initialize` sets `required` **once**. `Claim` and `Return` read it from stored state and never write it.
There is no instruction that mutates `required`, and no instruction that mutates anything in the state account after `Initialize`.

**So the threshold cannot be changed, paused, or skimmed — not by any wallet, not by a multisig, not by the (nonexistent) upgrade authority.** Confirmed by reading; confirmed by the deployed hash matching that source.

---

## 3. THE VAULT IS ARMED — LIVE STATE

Vault account `136gVxQtoq7rTVozniyNu7NfvPY5XKoMYVa99d3AT28g`, 76 bytes, layout per `state.rs`:

```
discriminator : 1
bump          : 255
deed_bump     : 253
coin_bump     : 254
deed_mint     : DVD4qXDVgjwUTyfPaAdmvZJYb5CWuse2cmisYoTH9g5r   ← matches offset 4
coin_mint     : A9AHYeqb7nQk7LZUraw7rBCzYRjy2DRvE6NqWfFHKRdH   ← matches offset 36
required      : 420,690,000,000,000 raw units
              = 420,690,000 HUHCAT  (6 decimals)
              = 43.83% of live supply (959,904,083.622)
```

**Right now, the vault holds:**
- Deed token account `CKU7yvB…`: **1 DVD4** ✅ (owner = the vault PDA — only the program can sign)
- Coin token account `AQHLmHH…`: **0 HUHCAT** ✅

**The deed is in the vault. The vault is empty of coin. State = "locked, awaiting a claimant."**

Note: the coin mint's own metadata authorities are *also* revoked (`updateAuthority: null`, `metadataPointer.authority: null`) — verified live. So there is no remaining lever anywhere in this system.

---

## 4. THE DEV'S THREAD — WHAT'S TRUE, WHAT'S LOOSE

Thread: `@wewillallmake1t`, posted **2026-09-17 02:57Z**. The seal transactions ran **02:35–02:36Z** — **they sealed first, then announced.** Good order. That's how it should be done.

| Claim in thread | Verdict |
|---|---|
| "metadata authority revoked, pointer authority revoked, mint authority revoked" | **TRUE** — all three confirmed live, plus freeze authority |
| "the inscription has exactly one deed" | **TRUE** — supply 1, decimals 0 |
| "locked in a vault program with no admin and a burned upgrade key" | **TRUE** — `Authority: None`, control-tested |
| "the vault has two moves and will only ever have two" | **TRUE** — three instructions total, one of which is one-time init |
| "nobody can change the amount, pause it, or take a cut" | **TRUE** — `required` is write-once; no admin path exists |
| "first image inscription on the Solana blockchain" | **TRUE, but with a narrower scope than the words imply** — see §5 |

**The one line that overreaches is not the dev's — it's the amplifier's.** `@jidn_w` wrote:

> "Dev just fractionalised the inscription, locked it in a vault and gave ownership to holders. So anyone that buys $huhcat receives a piece of the first ever inscription."

**That is not what the mechanics do, and you should not repeat it.**
This is not fractionalisation. There is no pro-rata claim, no dividend, no shared title. The vault has exactly two states, and the deed goes to **whoever locks the fixed amount first, in full**. Everyone else holds a coin that is *optionally* convertible. The accurate framing is:

> **"$HUHCAT carries a standing, permissionless option: lock 420,690,000 tokens and the deed is yours."**

That is a *better* story than fractionalisation anyway, because it's true and it's verifiable — and it implies something powerful: **the only way to take the deed is to remove 43.83% of supply from circulation.** The vault is a structural bid, not a share certificate.

---

## 5. THE "FIRST" CLAIM — THE DEV DID THE WORK I SAID COULDN'T BE DONE

In the prior research pass I wrote: *"uniqueness not checked… T? for global uniqueness."* I said it couldn't be proven without an exhaustive scan.

**The deployer ran the exhaustive scan.** `docs/evidence/v1scan.py` + `v1scan-results.json`:

| Metric | Result |
|---|---|
| Slots scanned | **729** — 447,120,000 → 447,120,728 inclusive, **none skipped** |
| Transactions examined | **881,986** |
| Transactions with `version == 1` | **12** |
| v1 transactions carrying image data | **1 — the HUHCAT inscription** |

They also scanned the 60 blocks *before* activation. And they correctly anchor activation to the **feature account itself** (`txv1aq4…`, `activated_at = 447120000`) rather than to an announcement — because **validators reject v1 transactions before that slot, no earlier block can physically contain one.**

They then audited every v1 transaction with ≥64 bytes of instruction data and classified by entropy: the Memo spam (1.58 bits/byte), two Phoenix order-book payloads (~4.8), one failed tx, pump.fun IPFS creates — and the HUHCAT JPEG (compressed-image entropy, ~7.5–8, zero-bytes 0%).

**Honest residuals they disclosed themselves:** (1) the RPC served complete block contents — the hash chain rules out missing *blocks*, but not a silent transaction omission within a served block; (2) "image" means recognisable image content.

**Upgraded tier:** the claim **"first image inscribed on Solana in a v1 transaction"** moves from **T3/T?** to **T1 (corroborated by an exhaustive, reproducible, self-disclosed-method scan)** — and I independently verified the anchor facts it rests on (activation slot, the two transaction slots, the 2,535-char data URI).

**What is still NOT claimed and should not be:** "first image on Solana, period" — compressed NFTs put data on-chain in 2023. The defensible, narrow, provable claim is the **v1** one. **Use the narrow claim. It is unbreakable. The broad one is breakable.**

---

## 6. THE ECONOMICS — WHAT THIS MEANS FOR THE BOOK

Live, 2026-09-17 ~11:00 UTC:

| | |
|---|---|
| Price | **$0.000599** (main PumpSwap pool) |
| Main pool liquidity | **$81,761** |
| FDV | **~$575,209** |
| **Cost to claim the deed** | **420,690,000 × $0.000599 ≈ $252,077** |
| …as multiple of main-pool liquidity | **3.1×** the entire pool |
| …as share of FDV | **43.8%** |

**Read this carefully, because it's the single most important market insight in this document:**

The deed is not claimable at current prices without *massively* moving the price. Anyone attempting it must acquire 43.83% of supply through a pool holding $82K — the slippage alone would reprice the token several hundred percent before they finished.

**Consequences:**
1. **The vault functions as a hard structural bid.** To take the deed you must buy ~44% of supply and then *lock it forever*. That removes it permanently.
2. **The "Return" path is the interesting one over time.** If someone eventually claims the deed, the vault then holds 420.69M coin — and the deed can only be redeemed by returning it *for those coins*. It is a two-way door with a fixed exchange rate.
3. **The dev's own framing — "the coin is the only key" — is mechanically correct.** No wallet, no multisig, no admin. Verified.

---

## 7. VERIFICATION CHECKLIST — REPRODUCE EVERY WORD

```bash
# 1. Program has no upgrade authority (compare against a control)
solana program show GGTQ55p33VCfuP42oFKV1QyrSkmbwkEsFJrrpkRqcZc3
solana program show JUP6LkbZbjS1jKKwapdHNy74zcZ3tLUZoi5QNyVTaV4   # control: HAS one

# 2. On-chain bytes == published source
solana program dump GGTQ55p33VCfuP42oFKV1QyrSkmbwkEsFJrrpkRqcZc3 onchain.so
sha256(onchain.so) == sha256(docs/evidence/huhcat_vault.deployed.so)
                          == bbc47f545456ff99266f5c0aa9aa574493b27be84e6bc2ffaece559cb492367c

# 3. The deed is sealed
#    DVD4qXDVgjwUTyfPaAdmvZJYb5CWuse2cmisYoTH9g5r
#    supply 1 · decimals 0 · mint/freeze/update/pointer authorities all null

# 4. The deed is in the vault
#    token acct CKU7yvBoud33q7refZ4kXQiEBEposuqTB9SonEraZ771 holds 1, owner = vault PDA

# 5. The vault is program-derived
solana find-program-derived-address GGTQ55p33VCfuP42oFKV1QyrSkmbwkEsFJrrpkRqcZc3 \
  string:vault pubkey:DVD4qXDVgjwUTyfPaAdmvZJYb5CWuse2cmisYoTH9g5r

# 6. The terms
#    vault state 136gVxQtoq7rTVozniyNu7NfvPY5XKoMYVa99d3AT28g @68 : u64 LE
#    == 420,690,000,000,000 raw == 420,690,000 HUHCAT
```

---

## 8. VERDICT

**This is, to my knowledge, one of the more rigorously constructed community-token artefacts I have audited.** Not because the idea is clever — because the follow-through is honest:

- The binary matches the published source **byte for byte**.
- The authority is genuinely burned, **control-tested**.
- The image is genuinely sealed, **four authorities revoked**.
- The code refuses mints with extensions that could hurt the vault.
- The "first" claim was proven by **exhaustive scan**, with the method and its residuals **published**.
- They sealed the artefact **before** announcing it.
- When they needed a claim verified that they couldn't prove, they didn't assert it — they wrote a scanner.

**The one thing that still overstates is a third-party quote-tweet, not the deployer.** Correct the amplification, not the source.

**Two live risks that remain (unchanged, and both now smaller than I thought):**
1. **The 1/1 is genuinely claimable by anyone who can afford it.** That is the design. But it means the deed can leave the vault — by *Return*, at the holder's choice. "Sealed and vaulted" remains the accurate phrase; "unstealable" still overstates, because a claimant can legitimately take it. What cannot happen is *unauthorised* movement.
2. **The coin mint has no remaining authorities, so it cannot be reconfigured** — confirmed live. There is no back door here.

**Bottom line: the dev's thread is accurate. The chain agrees with it. My previous objection was wrong and is withdrawn.**
