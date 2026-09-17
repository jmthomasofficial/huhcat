# HUHCAT: REVVIN CHECKLIST v2 for huhcatonsol.com

As of: 2026-09-17 (verified live from Solana RPC + pump.fun primary sources)
Prepared by: Analyst (Ghost / jmxghost lane)
For: Revvin, owner of huhcatonsol.com

This supersedes the earlier checklist. The earlier version contained an error
about the fee schedule that has since been corrected. Every claim below was
re-verified against primary sources today.

Nothing here is opinion. Each item states what the site currently says, what
the chain or pump.fun actually says, and the exact replacement text.

---

## HOW TO READ THIS

- **WRONG = currently false, fix immediately
- **UNVERIFIED = cannot be proven, remove or soften
- **IMPRECISE = true in spirit but technically attackable, tighten it
- **SLOP = AI writing pattern, remove for credibility
- **OK = verified correct, leave alone

The reason precision matters: CT is reading this site. Every claim is a
potential attack surface. A single wrong number discredits the whole page.

---

# SECTION A: WRONG RIGHT NOW

## A1. The fee rate "today" is wrong

**Site says:** `today | 0.75%`

**Truth:** The rate is a function of market cap. Verified live today, the
market cap was moving between roughly 9,900 and 12,600 SOL, which places the
coin in the **9,820 to 14,740 SOL** tier paying **0.700%**.

The rate changes as market cap moves, in both directions. It currently sits close to a tier boundary, so it flips between 0.700% and 0.750% depending on the minute. Any hardcoded "current rate" is wrong within minutes.

**Replace the entire fee table + surrounding sentence with:**

> The creator fee is set by market cap on a schedule of 25 tiers that pump.fun
> publishes. It runs from a peak of 0.950 percent down to a floor of 0.050
> percent once the market cap reaches 98,240 SOL. That spread is nineteen times
> for the same trade.
>
> The coin moves between tiers as its market cap moves, in both directions, so
> a fall in market cap raises the rate again. The table is the fixed part.
>
> The full schedule is at pump.fun/docs/fees, and the exact rate at any moment
> depends on which tier the coin occupies right now.

**Do not publish a "current rate" number.** Point at pump.fun/docs/fees instead.

---

## A2. The USD-framed tier rows are fragile

**Site says:**

| today | 0.75% |
| at $1M | 0.70% |
| at $4M | 0.40% |
| $10M and above | 0.05% |

**Truth:** The tier boundaries are denominated in **SOL**, not dollars. Today,
at SOL around $101, those dollar figures happen to land on the right tiers. That
is coincidence. The moment SOL price moves, the mapping breaks:

- At $1M with SOL at $101 → 9,880 SOL → 0.700% (site is right today)
- At $1M with SOL at $200 → 4,940 SOL → 0.750% (site would be wrong)
- At $10M with SOL at $50 → 197,600 SOL → 0.050% (still right, but only by luck)

**Replace with SOL-denominated rows:**

| Tier (SOL market cap) | Creator fee |
| --- | --- |
| 420 to 1,470 | 0.950% (peak) |
| 4,420 to 9,820 | 0.750% |
| 9,820 to 14,740 | 0.700% |
| 39,300 to 44,210 | 0.400% |
| 98,240 and above | 0.050% (floor) |

Then add: `Market-cap tiers are set in SOL, and there are 25 of them in total.`

---

## A3. The liquidity figure is wrong and it moves

**Site says:** `Every liquidity pool on Solana holding HUHCAT adds up to roughly 92.9 million tokens. A claim needs 420.69 million.`

**Truth:** Verified live today, all pools combined held roughly **61 to 72
million tokens**, moving hour to hour as people trade. Never 92.9 million at any
point today.

**Replace with:**

> Every pool on Solana holding HUHCAT added up to roughly 61 million tokens when
> this was checked, while a claim needs 420.69 million, which is more than six
> times everything sitting in all of those pools combined.

**Better option:** state it as a ratio with a timestamp, or link a live source,
so the number cannot go stale.

---

## A4. The testnet claim has no source

**Site says (twice):**
- `The first cat JPEG inscribed on Solana in a v1 transaction.`
- `The same cat that tested it on testnet went into a mainnet transaction.`
- `1. testnet same image, v1 tx, proof of concept`

**Truth:** There is **no evidence for a testnet inscription** anywhere. The
deployer's published source repository contains no testnet reference. The
deployer's own X thread announcing this never mentions testnet. Neither the
scan evidence nor the on-chain record supports it.

The mainnet claim IS solid and provable: the image went into a mainnet v1
transaction at slot 447,120,728, and a full 729-block scan found it was the
only image-bearing v1 transaction in that window.

**Remove every testnet reference.** Replace the opening line with:

> The first cat JPEG inscribed on Solana in a v1 transaction. The cat is in the coin.

And replace timeline step 1 with the verified sequence:

> 1. v1 transactions activate on Solana mainnet at slot 447,120,000
> 2. slot 447,120,727 coin mint created in a v1 tx
> 3. slot 447,120,728 image written in a v1 tx
> 4. the deployer leaves, the account goes quiet
> 5. the community keeps building

If Revvin has a testnet transaction signature, publish it. Without one, cut it.

---

## A5. "Roughly 92.9 million" also appears in the FAQ area

Search the whole site for `92.9` and `92,900,000` and fix every instance with
the corrected figure from A3.

---

# SECTION B: IMPRECISE (Revvin flagged these, he was right)

## B1. "The program can never be changed by anyone"

**Site says:** `vault program that has no upgrade authority, meaning the program can never be changed by anyone, including its author`

**Problem:** The vault is controlled by the program. Only the program can sign
for its accounts. Saying it can "never be changed" is loose.

**Replace with:**

> The vault has no human admin, no pause function, no close function, and no
> upgrade authority. Only the program itself can sign for the accounts it holds.

---

## B2. "The vault has two moves and will only ever have two"

**Site says:** `The vault has two moves and will only ever have two.`

**Problem:** Claim and Return are live functions of the program. Saying nothing
can ever happen to it is wrong.

**Replace with:**

> The program carries two intended actions, and those are Claim and Return.

---

## B3. "Is the dev here?" FAQ answer overstates

**Site says:** `There is nothing left for anyone to change.`

**Replace with:**

> On the coin itself, mint and freeze authority are null. On the image mint, all
> four authorities are null. The program's code and its fixed requirement cannot
> be changed, and its only intended actions are Claim and Return.

---

## B4. Add the Holder Rewards irreversibility fact

This one is **verified and worth adding**. pump.fun stated on 12 September 2026:

> Existing Cashback & Creator Fee tokens can be switched to a Holder Rewards
> token. Once a token becomes a Holder Rewards token, it cannot be changed.

That is a strong, sourced, permanent fact. Add it near the rewards section:

> Once a token switches to Holder Rewards, pump.fun does not allow it to switch
> back. That is pump.fun's own rule, stated in their 12 September announcement.

---

# SECTION C: AI SLOP PATTERNS TO REMOVE

These read as machine-written and undercut credibility. The project's whole
edge is that it sounds like a real person being precise.

| Current text | Why it flags | Fix |
| --- | --- | --- |
| `That's it. That's the pitch. Huh.` | Closing kicker, classic AI cadence | End the paragraph on the substance instead |
| `` | Slogan kicker | Cut it, or replace with a concrete statement |
| `Nobody here is holding a roadmap.` | Defining by what it isn't | `Everyone here is holding a timestamp you can still open, and a JPEG you can still decode.` |
| `Not a link. The picture.` | Negative-then-positive fragment | `The picture itself went into a mainnet transaction.` |
| `Milestones, not promises.` | Same negative parallelism | `Milestones with dates that are already behind us.` |

---

# SECTION D: VERIFIED CORRECT, LEAVE ALONE

These were checked today and are accurate. Do not let anyone "fix" them.

| Claim on site | Verification |
| --- | --- |
| `959.9M Supply` | Live: 959,904,004.86 |
| `0 / 0 Buy / sell tax` | Extensions are only tokenMetadata + metadataPointer. No transfer fee, no hook, no permanent delegate |
| `Token-2022` | Mint owner is TokenzQdBNbLqP5VEhdkAS6EPFLC1PHnBqCXEpPxuEb |
| `Revoked Mint / freeze both null` | Both confirmed null |
| `6 Decimals` | Confirmed 6 |
| `43.83 percent of supply` | 420,690,000 / 959,904,004.86 = 43.8263% |
| `slot 447120727 coin mint created · tx ymfySMbr` | Confirmed: slot 447,120,727, version 1 |
| `slot 447120728 image written · tx 5nqX9Tth` | Confirmed: slot 447,120,728, version 1 |
| `Sealed 17 September 2026: all four authorities revoked, supply set to 1` | All four null, supply 1, decimals 0 |
| `Metadata URI is data:image/jpeg;base64` | Confirmed in the metadata |
| `Metadata fields token → A9AHYeqb, mime → image/jpeg` | Confirmed |
| `1.81 SOL / 1,807 payments / 207 batches in one hour` | Measured from chain |
| `vault program GGTQ55…` / `deed account CKU7yv…` | Both confirmed correct |
| `upgrade authority: none` | Confirmed, control-tested against two programs that still have live authorities |

---

# SECTION E: THE ONE-PARAGRAPH SUMMARY FOR REVVIN

> Three things on the site are factually wrong and need fixing today: the
> "0.75% today" rate (it is 0.700% and it moves with market cap, so stop
> publishing a current number and point at pump.fun/docs/fees), the "92.9
> million tokens in pools" figure (it is roughly 61 million and it changes
> hourly), and every testnet reference (there is no evidence for a testnet
> inscription anywhere, so cut it).
>
> Two things are technically loose: "the program can never be changed" and
> "the vault has two moves and will only ever have two". Replace both with the
> exact wording in Section B.
>
> One thing is worth adding: pump.fun's own rule that a Holder Rewards token
> cannot switch back.
>
> Everything else on the site checks out. The supply, the decimals, the zero
> tax, the sealed authorities, the transaction slots, the 43.83 percent, the
> vault addresses, the distribution numbers: all verified live today.

---

# VERIFICATION INDEX

Anyone reading this can check every line.

**Coin mint**
solscan.io/token/A9AHYeqb7nQk7LZUraw7rBCzYRjy2DRvE6NqWfFHKRdH

**Image mint (all four authorities null, supply 1)**
solscan.io/token/DVD4qXDVgjwUTyfPaAdmvZJYb5CWuse2cmisYoTH9g5r

**Coin tx, v1, slot 447120727**
explorer.solana.com/tx/ymfySMbrWdhf1oCgU5QTHauKGw9seaq1FJQvk1ET8eZ58wjFLh2uZckEH2uQw7rkqPTaZJs9ASNvPNUvjPCBFPL

**Image tx, v1, slot 447120728**
explorer.solana.com/tx/5nqX9TthkjHNBR5grSVD8a4uPZLKUxqNKzLuh9fzDhho2uZAQZM6rdnvgBUjiRn4Gd7xQe1TucTkshpYd21YftD7

**Vault program (upgrade authority burned)**
solscan.io/account/GGTQ55p33VCfuP42oFKV1QyrSkmbwkEsFJrrpkRqcZc3

**Deed account (1 of 1)**
solscan.io/account/CKU7yvBoud33q7refZ4kXQiEBEposuqTB9SonEraZ771

**Fee schedule and tiers, straight from pump.fun**
pump.fun/docs/fees

**Holder Rewards distribution rules**
@Pumpfun announcement, 12 September 2026

**Source code, byte-for-byte identical to the deployed program**
github.com/weareallgoingtomake1t/huhcat

---

# RULE FROM HERE ON

Never publish a number that changes. Market cap, liquidity pool totals,
distribution counts, and the current fee rate all move. State them as
"measured at [date]" or link a live source. Fixed endpoints like 0.950%,
0.050%, 98,240 SOL, 420,690,000, and 43.83% are safe forever.
