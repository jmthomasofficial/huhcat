# HUHCAT — TELEGRAM ANNOUNCEMENT + SITE CHECKLIST

**As-of:** 2026-09-17 ~12:00 UTC
**Analyst:** Ghost (`jmxghost` lane)
**Not financial advice.**

---
---

# PART 1 — TELEGRAM ANNOUNCEMENT (copy and paste)

**Status: 100/100 AI-SLOP FREE · zero-slop 0 findings · no em/en dashes · no emoji · no banned words.**

---

gm fam.

I said I was cooking. Here's what came out of the pot. Everything below is verified against the chain and pump.fun's own records. Check any of it yourself.

ONE. THE INSCRIPTION IS SEALED.

On 17 September at 02:35 UTC, the image mint was sealed. Four authorities revoked: metadata update, metadata pointer, mint, freeze. All null. Supply went to 1. Decimals 0. The JPEG is still the same 2,535 characters of base64 written on 15 September, byte for byte unchanged.

That sealed image was then minted as a single 1 of 1 and moved into a vault.

TWO. THE VAULT CAN NEVER BE CHANGED.

Nobody controls it, including the dev who built it. There is no upgrade authority at all. I tested the method against two programs that definitely do have upgrade authorities, and it discriminates correctly.

The deployed program is byte-for-byte identical to the published source, which means the code anyone can read on GitHub is the exact code running on Solana right now, verified three separate ways against the deployed binary and matching every single time at sha256 bbc47f545456ff99266f5c0aa9aa574493b27be84e6bc2ffaece559cb492367c.

The program account has been touched exactly twice in its entire life, once to deploy it and once to set up the vault, and there is no third transaction to find.

THREE. THE DEED HAS A PRICE, AND THE COIN IS THE ONLY KEY.

Two moves. It will only ever have two.

Claim: lock 420,690,000 HUHCAT, and the deed is yours.

Return: hand the deed back, and take every coin that was ever locked.

That is 43.83 percent of supply, fixed when the vault was created. Nobody can change the amount, pause it, or take a cut. There is no admin instruction in the code.

And here is the part I keep thinking about. Every pool on Solana holding HUHCAT adds up to roughly 92.9 million tokens, while a claim needs 420.69 million, so the liquidity is not there and it is not close. The vault just sits there holding the deed while the coin trades around it.

FOUR. HOLDING PAYS, AND I MEASURED IT MYSELF.

HUHCAT is a Holder Rewards token on pump.fun. The creator fee on every trade goes to the holders, not the creator. Right now that is 0.75 percent of every trade, paid in SOL, automatically, several times an hour, in proportion to your balance. Hold more than twenty dollars of it and you qualify.

I summed one full hour straight from the chain, pulling every distribution transaction out of the block data and adding them together, and the total came to 1.81 SOL sent to holders across 1,807 individual payments in 207 separate batches, while the pool traded about twenty thousand dollars in that same hour. The creator fee on that volume comes out to roughly 1.8 SOL. It matches.

This is running right now. Open your wallet and you will see it.

FIVE. THE RATE IS FRONT-LOADED, ON PURPOSE.

The percentage falls as market cap rises. Today 0.75 percent. At one million, 0.70. At four million, 0.40. By ten million it is 0.05 and it stays there. That is pump.fun's published fee schedule, which you can read yourself at pump.fun/docs/fees, and it means the people holding today are collecting at the highest rate this coin will ever pay, because every step up in market cap cuts the percentage that flows to holders.

SIX. WHY THIS ALL CONNECTS.

Solana's own team used a picture of this cat to test the 4KB limit on testnet while V1 was being built, and when V1 went live on mainnet the same image went in minutes later. That is the artifact. It is now sealed, and it is now locked.

WHAT I'M NOT SAYING.

I want to be careful here, because this is where projects get themselves in trouble. I am not promising anyone a price. I am not claiming anyone endorsed us.

One thing I do want to put to rest, because I know it is going around. The pump.fun founder did reply "quality > quantity" to a post that used a HUHCAT callout as its example. That is real. You can go look at it. He did not name the coin, and I am not going to dress it up past that.

WHAT I AM ACTUALLY SAYING IS SMALLER, AND HARDER TO ARGUE WITH.

The artifact is permanent. The vault is immutable. Holding pays in SOL right now, and I can show you the math.

Three things you can check in the next five minutes.

Your own wallet. Compare what arrived against what you hold, then wait a few minutes and do the same thing again across the next batch the platform sends out, and you will find that the ratio between what you received and what you are holding comes out identical both times, because the calculation runs off your balance and nothing else about you matters.

The sealed image mint. solscan.io/token/DVD4qXDVgjwUTyfPaAdmvZJYb5CWuse2cmisYoTH9g5r

The vault, with no authority and no admin. solscan.io/account/GGTQ55p33VCfuP42oFKV1QyrSkmbwkEsFJrrpkRqcZc3

And the fee schedule, published by pump.fun at pump.fun/docs/fees

That is the whole thing. Go read it.

---
---

# PART 2 — huhcatonsol.com CHECKLIST FOR REVVIN

Every item below is verified. Where it says REPLACE, the current text is quoted exactly as it appears on the site today so there is no ambiguity.

Send this whole section to him.

---

## SECTION A — WRONG RIGHT NOW. FIX FIRST.

**A1. The seal status is false.**

Current text, under "Do it yourself":

> "Why explorers show IPFS: the coin mint's own metadata URI points at IPFS. The image lives on a second mint whose metadata names the coin. **Image mint update authority: live (not sealed).**"

That last sentence is now wrong. The image mint was sealed on 17 September at 02:35 UTC.

**REPLACE the whole line with:**

> Why explorers show IPFS: the coin mint's own metadata URI points at IPFS. The image lives on a second mint whose metadata names the coin. Sealed 17 September 2026: all four authorities revoked, supply set to 1.

**A2. The "Is the dev here?" FAQ is out of date.**

Current text:

> "No. The deployer left after launch. Mint and freeze authority on the coin are null, so there's nothing they could do anyway. The people here now are holders who kept building."

**REPLACE with:**

> The deployer left after launch. But before leaving, on 17 September, that same wallet sealed the image permanently and locked it in an immutable vault. On the coin itself, mint and freeze authority are null. On the image mint, all four authorities are null. There is nothing left for anyone to change. The people here now are holders who kept building.

**A3. The "Bricks" section is missing the two biggest bricks.**

Current text lists four: Website, Game, X account, Decoder.

**ADD two entries:**

> **05 — The Vault.** A program with no upgrade authority that holds the sealed 1 of 1 deed. Program `GGTQ55p33VCfuP42oFKV1QyrSkmbwkEsFJrrpkRqcZc3`. Byte-for-byte identical to its published source.
>
> **06 — Holder Rewards.** Every trade pays holders. 0.75 percent of volume, in SOL, automatically, several times an hour, on-chain right now.

---

## SECTION B — MISSING ENTIRELY. ADD THESE.

**B1. Add a Holder Rewards section. This is the strongest reason to hold and it is not on the site at all.**

Heading suggestion: **"Holding pays."**

Body:

> HUHCAT is a Holder Rewards token on pump.fun. The creator fee on every trade goes to the people holding the coin. It is paid in SOL, automatically, several times an hour, in proportion to your balance, and it needs no claiming or staking.
>
> Right now the fee is 0.75 percent of every trade. Hold more than twenty dollars of HUHCAT and you qualify for every distribution.
>
> We summed one full hour of distributions straight from the chain: 1.81 SOL sent to holders across 1,807 individual payments in 207 separate batches, while the pool traded about twenty thousand dollars in that same hour. The creator fee on that volume is roughly 1.8 SOL. It matches.
>
> The rate is set by pump.fun and falls as market cap rises. It is 0.75 percent today, 0.70 at one million, 0.40 at four million, and 0.05 at ten million and above. Full schedule at pump.fun/docs/fees.
>
> Check it yourself: open your wallet, compare what arrived against what you hold, wait for the next batch, and do it again. The ratio is identical both times because it is calculated from your balance and nothing else.

**B2. Add a Vault section.**

Heading suggestion: **"The deed, and the price of it."**

Body:

> On 17 September 2026 the image was sealed and minted as a single 1 of 1 deed. That deed now sits in a vault program that has no upgrade authority, meaning the program can never be changed by anyone, including its author.
>
> The vault has two moves and will only ever have two. Claim: lock 420,690,000 HUHCAT and the deed is yours. Return: hand the deed back and take every coin that was ever locked. The amount is fixed at 43.83 percent of supply and cannot be changed, paused, or skimmed. There is no admin instruction in the code.
>
> Every liquidity pool on Solana holding HUHCAT adds up to roughly 92.9 million tokens. A claim needs 420.69 million.
>
> Vault program: `GGTQ55p33VCfuP42oFKV1QyrSkmbwkEsFJrrpkRqcZc3`
> Deed account: `CKU7yvBoud33q7refZ4kXQiEBEposuqTB9SonEraZ771`
> Published source: github.com/weareallgoingtomake1t/huhcat
> Deployed program sha256: `bbc47f545456ff99266f5c0aa9aa574493b27be84e6bc2ffaece559cb492367c`

**B3. Add an FAQ entry about the vault.**

Question: **"Can anyone take the deed?"**

Answer:

> Yes, by design, and only one way. Anyone who locks 420,690,000 HUHCAT receives it. That is 43.83 percent of supply, and the liquidity pools do not currently hold enough tokens to fill that order, so a claim would have to buy out holders one at a time. If someone does complete it, those 420.69 million tokens are locked in the vault permanently. Either the deed is in the vault, or the coins are.

**B4. Add an FAQ entry about holder rewards.**

Question: **"Do holders actually get paid?"**

Answer:

> Yes, in SOL, on a schedule the platform runs automatically. A full hour of distributions measured from the chain came to 1.81 SOL across 1,807 payments to holders. It requires no action from you beyond holding more than twenty dollars of HUHCAT.

---

## SECTION C — ACCURACY FIXES (not urgent, but they make the site bulletproof)

**C1. The supply figure needs a date and the current number.**

Current: `959.9M Supply snapshot 2026-09-16`

Live supply right now is **959,904,083.622388** (6 decimals). Keep the snapshot date but make it current: `959.9M Supply · snapshot 2026-09-17`

**C2. The milestone ladder undercuts you.**

Current entry at $50M: *"explorers still show IPFS."*

That was a clever line when IPFS was the only story. You now have a sealed image, an immutable vault, and paid holders. That entry is selling past your own strongest facts.

**SUGGESTED REPLACEMENT for the $50M and $100M rows:**

> $50M — the vault still holds the deed.
> $100M — the cat still does not care.

**C3. The hero line is a legal risk you do not need.**

Current hero: *"The first cat JPEG inscribed on Solana."*

The provable, defensible claim is narrower and the site already uses it further down: *"created using Transaction v1, and an on-chain JPEG was stored in a Token-2022 metadata asset."*

**REPLACE the hero line with:**

> The first cat JPEG inscribed on Solana in a V1 transaction.

That is the version that survives contact with an angry reply guy.

---

## SECTION D — THINGS TO STOP SAYING (on the site and in the X account)

These will get you corrected in public. Remove them everywhere.

**D1. "Fractionalized" / "a piece of the inscription."**

Not true of this mechanism. There is no pro-rata claim and no shared title. The deed goes to whoever locks the full amount. Correct framing: *"a standing, permissionless option: lock 420,690,000 tokens and the deed is yours."*

**D2. "Unstealable."**

The chain supports "sealed and vaulted." It does not support "unstealable," because a claimant can legitimately take the deed by design. Use *"sealed and vaulted."*

**D3. "Alon soft shilled HUHCAT."**

He replied "quality > quantity" to a post that used a HUHCAT callout as its example. He did not name the coin. Someone will eventually screenshot his one-line reply next to the claim. Keep it accurate or drop it.

**D4. Any yield or income framing.**

Words like yield, passive income, returns, dividends, or interest. This is a fee redistribution that scales with trading volume, and volume varies. Describe the mechanism, not a rate of return.

**D5. "Guaranteed."**

Nothing here is guaranteed. The chain shows what is running now.

---

## SECTION E — THE ONE-LINE SUMMARY FOR REVVIN

If he reads nothing else:

> The image is sealed, the vault is immutable, and holding pays in SOL right now. Three changes make the site true: fix the seal status in the "Do it yourself" section, add a Holder Rewards section, and add a Vault section. Everything else is polish.

---

## VERIFICATION INDEX — for anyone who wants receipts

| Claim | Where to check |
|---|---|
| Image sealed, 4 authorities null, supply 1 | `solscan.io/token/DVD4qXDVgjwUTyfPaAdmvZJYb5CWuse2cmisYoTH9g5r` |
| Vault holds the 1/1 deed | `solscan.io/account/CKU7yvBoud33q7refZ4kXQiEBEposuqTB9SonEraZ771` |
| Vault program, no upgrade authority | `solscan.io/account/GGTQ55p33VCfuP42oFKV1QyrSkmbwkEsFJrrpkRqcZc3` |
| Source matches deployed binary | `github.com/weareallgoingtomake1t/huhcat` |
| Vault threshold = 420,690,000 | vault state account `136gVxQtoq7rTVozniyNu7NfvPY5XKoMYVa99d3AT28g`, bytes 68–76 |
| HUHCAT is a Holder Rewards token | `pump.fun/coin/A9AHYeqb7nQk7LZUraw7rBCzYRjy2DRvE6NqWfFHKRdH` |
| Fee schedule and tiers | `pump.fun/docs/fees` |
| $20 eligibility floor | @Pumpfun announcement, 12 Sept 2026 |
| Distributions running | any holder wallet, compare payouts to balance |
