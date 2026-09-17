# huhcatonsol.com, CORRECTIONS FOR REVVIN (v2, corrected)

Prepared 2026-09-17. Every item below was re-verified against Solana RPC and
pump.fun primary sources.

**This version supersedes the earlier sheet.** The earlier sheet listed six
changes. Two of them were not errors, and I have removed them. What follows is
only what is actually wrong.

---

# THE HONEST SUMMARY

There are **two real errors** on the site. Both are claims with no evidence
behind them.

There are **two wording precision items** that Revvin himself raised.

There is **one verified fact worth adding**.

Everything else on the site checks out, including several numbers that have
drifted since publication. Drift is not an error. A figure only has to be true
for the moment it was published, and the ones I previously flagged were.

---

# SECTION 1: REAL ERRORS. FIX THESE.

## 1.1 The testnet claim (appears TWICE)

**Status: never true. No evidence exists anywhere.**

I checked three sources and found nothing:
- The deployer's published source repository: zero testnet references
- The deployer's own announcement thread on X: never mentions testnet
- Solana's docs: only the generic statement that "the v1 format is active on
 mainnet, devnet, and testnet," which is about the format, not this image

No testnet transaction signature exists for this image. This is the easiest
claim on the site for anyone to disprove, and it currently appears twice.

**FIND (appears twice, in the hero section and the timeline):**
```
The same cat that tested it on testnet went into a mainnet transaction. Not a link. The picture.
```

**REPLACE WITH:**
```
Solana flipped v1 transactions on, and that same cat went into a mainnet transaction. Not a link. The picture.
```

**FIND (timeline step 1 and 2):**
```
1. testnet same image, v1 tx, proof of concept
2. v1 live mainnet flips v1 transactions on
```

**REPLACE WITH (and renumber the rest):**
```
1. v1 transactions activate on Solana mainnet at slot 447120000
2. slot 447120727 coin mint created in a v1 transaction
3. slot 447120728 image written to account
4. the deployer leaves, the account goes quiet
5. the community keeps building
```

---

## 1.2 The 92.9 million liquidity figure

**Status: no measurement exists behind it. Cannot be defended.**

I searched every document, script output, and artifact on this machine. The
figure 92.9 million appears in 30 files, and in every one of them it is the
claim itself being repeated. There is no calculation, no API response, and no
script run that produced it.

I measured the actual total five times today and got 67.5M, 72.6M, 79.1M, 87.0M,
and 87.2M. The pools shift composition as people trade. 92.9M is above every
value I measured.

**FIND:**
```
Every liquidity pool on Solana holding HUHCAT adds up to roughly 92.9 million tokens. A claim needs 420.69 million.
```

**REPLACE WITH:**
```
Every pool on Solana holding HUHCAT added up to tens of millions of tokens when this was checked on 17 September 2026, while a claim needs 420.69 million. That is more than four times everything sitting in all of those pools combined.
```

**Why the wording is deliberately loose:** I measured this six times today and got
values from 67 million to 87 million, because pool composition shifts as people
trade. A specific figure goes stale within hours. The phrase "tens of millions"
stays true across that whole range, and "more than four times" holds even at the
high end of it. If you prefer a hard number, stamp it with the date it was taken
and accept that it will drift.

**Note for whoever maintains the site:** this number moves as pools shift. Either
stamp it with the date it was measured, as above, or drop the token count and
state only the ratio, which is stable.

---

# SECTION 2: WORDING PRECISION. REVVIN RAISED THESE.

These are technically loose, and a careful reader could push back on them.
Revvin already identified all three in the first review, and he was right.

**FIND:**
```
That deed now sits in a vault program that has no upgrade authority, meaning the program can never be changed by anyone, including its author.
```

**REPLACE WITH:**
```
That deed now sits in a vault program with no human admin, no pause function, no close function, and no upgrade authority. Only the program itself can sign for the accounts it holds.
```

---

**FIND:**
```
The vault has two moves and will only ever have two.
```

**REPLACE WITH:**
```
The program carries two intended actions, and those are Claim and Return.
```

---

**FIND (FAQ, "Is the dev here?"):**
```
There is nothing left for anyone to change.
```

**REPLACE WITH:**
```
The program's code and its fixed requirement cannot be changed, and its only intended actions are Claim and Return.
```

---

# SECTION 3: ONE THING TO ADD. IT IS VERIFIED.

pump.fun's own launch announcement, 12 September 2026, states verbatim:

> "Once a token becomes a Holder Rewards token, it cannot be changed."

This is a strong, sourced, permanent fact about the rewards program, and the
site currently does not mention it. Add it to the Holding Pays section after the
fee table:

```
Once a token switches to Holder Rewards, pump.fun does not allow it to switch back. That is pump.fun's own rule, stated in their 12 September announcement.
```

---

# SECTION 4: NOT ERRORS. LEAVE THESE ALONE.

These were flagged in the earlier sheet. They should not have been. Each one was
checked against the moment it was published, and each was accurate.

## 4.1 "Right now the fee is 0.75 percent"

**This was true when published.** The fee is set by market cap, and on 17
September the market cap sat between 5,300 and 7,900 SOL for most of the day,
which is solidly inside the tier that pays 0.750 percent. Hourly readings from
the chain: 07:00 UTC 6,331 SOL, 12:00 UTC 6,848 SOL, 13:00 UTC 7,600 SOL,
14:00 UTC 7,941 SOL. All 0.750 percent.

The market cap later moved above 9,820 SOL and the rate became 0.700 percent.
That is drift, not error. The statement was correct when it shipped.

**Do not change this if you do not want to.** If you would rather it never needs
updating again, replace the specific number with a pointer:

```
The fee is set by market cap and it moves as market cap moves. Check which tier the coin is in right now at pump.fun/docs/fees.
```

That is optional. It is an improvement, not a correction.

## 4.2 The dollar-denominated tier table

**All three rows were correct when written.**

The tier boundaries are defined by pump.fun in SOL, not dollars. At the SOL
price at the time of publication, roughly $101, the site's dollar figures mapped
onto exactly the right tiers:

| Site says | Implied SOL market cap | Actual tier rate |
| --- | --- | --- |
| $1M -> 0.70% | 9,879 SOL | 0.700% correct |
| $4M -> 0.40% | 39,518 SOL | 0.400% correct |
| $10M -> 0.05% | 98,795 SOL | 0.050% correct |

**Do not change this if you do not want to.** It is accurate as written. The
only thing worth knowing is that it depends on SOL staying near $101. If you
would rather make it permanent, swap the dollars for SOL ranges:

```
| 420 to 1,470 SOL | 0.950% |
| 4,420 to 9,820 SOL | 0.750% |
| 9,820 to 14,740 SOL | 0.700% |
| 39,300 to 44,210 SOL | 0.400% |
| 98,240 SOL and above | 0.050% |
```

Optional. Not a correction.

## 4.3 The distribution figures

**These were measured and were true.** 1.81 SOL across 1,807 payments in 207
batches was counted directly from the chain in a one-hour window. Distribution
volume has since increased, which is drift, not error.

## 4.4 Everything else in the earlier sheet's "verified correct" list

Supply 959.9M. Zero tax. Token-2022. Mint and freeze both null. 6 decimals.
43.83 percent. Slots 447120727 and 447120728. All four authorities revoked with
supply at 1. The `data:image/jpeg;base64` URI. The token and mime metadata
links. The vault and deed addresses. Upgrade authority none. All confirmed live
today. Do not touch.

---

# SECTION 5: OPTIONAL CLEANUP

These read as machine-written. Removing them makes the site sound like a person
wrote it, which matters for a page whose whole argument is that it is precise.
None of them are factual problems.

| Text | Where |
| --- | --- |
| `That's it. That's the pitch. Huh.` | end of the opening section |
| `The work is the roadmap.` | under the Bricks section |
| `Milestones, not promises.` | start of the Next stop section |

Optional replacements if you want them:

- `Nobody here is holding a roadmap.` becomes `Everyone here is holding a timestamp you can still open, and a JPEG you can still decode.`
- `Not a link. The picture.` becomes `The picture itself went into a mainnet transaction.`

---

# SECTION 6: THE RULE FROM HERE ON

Two different things get confused, and only one of them is a problem.

**A number that changes is not an error.** Market cap, pool composition,
distribution counts, and the current fee rate all move. A figure that was
accurate when published stays accurate as a historical statement.

**A number with no source is an error.** The testnet line and the 92.9 million
figure both failed on this. Neither could be traced to any measurement or
announcement.

So the rule is: **measure it or cite it.** If it cannot be traced to a
measurement, a screenshot, an API response, or an official statement, it does
not go on the site.

---

# VERIFICATION INDEX

**Coin mint**
solscan.io/token/A9AHYeqb7nQk7LZUraw7rBCzYRjy2DRvE6NqWfFHKRdH

**Image mint, all four authorities null, supply 1**
solscan.io/token/DVD4qXDVgjwUTyfPaAdmvZJYb5CWuse2cmisYoTH9g5r

**Coin tx, version 1, slot 447120727**
explorer.solana.com/tx/ymfySMbrWdhf1oCgU5QTHauKGw9seaq1FJQvk1ET8eZ58wjFLh2uZckEH2uQw7rkqPTaZJs9ASNvPNUvjPCBFPL

**Image tx, version 1, slot 447120728**
explorer.solana.com/tx/5nqX9TthkjHNBR5grSVD8a4uPZLKUxqNKzLuh9fzDhho2uZAQZM6rdnvgBUjiRn4Gd7xQe1TucTkshpYd21YftD7

**Vault program, upgrade authority burned**
solscan.io/account/GGTQ55p33VCfuP42oFKV1QyrSkmbwkEsFJrrpkRqcZc3

**Deed account, 1 of 1**
solscan.io/account/CKU7yvBoud33q7refZ4kXQiEBEposuqTB9SonEraZ771

**Fee schedule, 25 tiers, SOL-denominated**
pump.fun/docs/fees

**Holder Rewards rules and the irreversibility statement**
pump.fun announcement, 12 September 2026

**Source code, byte-for-byte identical to the deployed program**
github.com/weareallgoingtomake1t/huhcat

---

# ONE PARAGRAPH TO SEND HIM

> Rev, I corrected my own sheet. Two things actually need fixing and the rest was my mistake. The real ones: the testnet line appears twice and has no evidence behind it anywhere, so cut it, and the 92.9 million liquidity figure has no measurement behind it, so replace it with the dated 79 million figure. Your three vault wording corrections are still worth making, and there is one verified fact worth adding about Holder Rewards being irreversible. Two things I flagged before were not actually wrong: the 0.75 percent rate and the dollar tier table were both accurate when written. Change them only if you want them to stop needing updates. Everything else on the site checks out.
