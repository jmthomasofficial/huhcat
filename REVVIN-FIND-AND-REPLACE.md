# huhcatonsol.com — FIND AND REPLACE SHEET FOR REVVIN

Every string below is copy-paste ready. Find the left, replace with the right.
Six changes fix every factual problem on the site.

Verified live 2026-09-17 against Solana RPC and pump.fun primary sources.

---

## REPLACE 1 — the testnet line (appears TWICE: hero + timeline)

**FIND:**
```
The same cat that tested it on testnet went into a mainnet transaction. Not a link. The picture.
```

**REPLACE WITH:**
```
Solana flipped v1 transactions on, and that same cat went into a mainnet transaction. Not a link. The picture.
```

---

**FIND (timeline step 1):**
```
1. testnet same image, v1 tx, proof of concept
2. v1 live mainnet flips v1 transactions on
```

**REPLACE WITH:**
```
1. v1 transactions activate on Solana mainnet at slot 447120000
2. slot 447120727 coin mint created in a v1 transaction
```

Then renumber the remaining steps so the list reads:
```
1. v1 transactions activate on Solana mainnet at slot 447120000
2. slot 447120727 coin mint created in a v1 transaction
3. slot 447120728 image written to account
4. the deployer leaves, the account goes quiet
5. the community keeps building
```

**WHY:** There is no testnet inscription. I checked the deployer's source repo (zero testnet references), the deployer's own X thread (never mentions testnet), and the research record (only generic Solana docs saying v1 is active on mainnet, devnet and testnet). No testnet transaction exists for this image. This claim is the easiest one for anyone to disprove and it appears twice.

---

## REPLACE 2 — the current fee rate

**FIND:**
```
Right now the fee is 0.75 percent of every trade.
```

**REPLACE WITH:**
```
The fee is set by market cap and it moves as market cap moves. You can check which tier the coin is in right now at pump.fun/docs/fees.
```

**WHY:** The rate is NOT 0.75 percent. Verified live today, the coin sits in the 9,820 to 14,740 SOL tier paying **0.700 percent**, and it is close enough to a boundary that it flips between 0.700 and 0.750 depending on the minute. Any fixed number goes stale within minutes. Do not publish one.

---

## REPLACE 3 — the whole fee table

**FIND:**
```
| today | 0.75% |
| at $1M | 0.70% |
| at $4M | 0.40% |
| $10M and above | 0.05% |
```

**REPLACE WITH:**
```
| 420 to 1,470 SOL | 0.950% |
| 4,420 to 9,820 SOL | 0.750% |
| 9,820 to 14,740 SOL | 0.700% |
| 39,300 to 44,210 SOL | 0.400% |
| 98,240 SOL and above | 0.050% |
```

And change the table caption from `Fee schedule · set by pump.fun, falls as market cap rises` to:

```
Fee schedule · set by pump.fun, 25 tiers, denominated in SOL
```

**WHY:** The boundaries are set in **SOL**, not dollars. Today, with SOL around $101, those dollar figures happen to land on roughly the right tiers. That is coincidence. When SOL moves, the dollar mapping breaks and the table becomes wrong. SOL-denominated rows stay true forever.

---

## REPLACE 4 — the liquidity figure

**FIND:**
```
Every liquidity pool on Solana holding HUHCAT adds up to roughly 92.9 million tokens. A claim needs 420.69 million.
```

**REPLACE WITH:**
```
Every pool on Solana holding HUHCAT added up to roughly 61 million tokens when this was checked, while a claim needs 420.69 million, more than six times everything sitting in all of those pools combined.
```

**WHY:** Verified live today, all pools combined held **60 to 72 million** and it changes hour to hour as people trade. It was never 92.9 million at any point today. The ratio is more than six times, not four.

---

## REPLACE 5 — the vault wording

**FIND:**
```
That deed now sits in a vault program that has no upgrade authority, meaning the program can never be changed by anyone, including its author.
```

**REPLACE WITH:**
```
That deed now sits in a vault program with no human admin, no pause function, no close function, and no upgrade authority. Only the program itself can sign for the accounts it holds.
```

**FIND:**
```
The vault has two moves and will only ever have two.
```

**REPLACE WITH:**
```
The program carries two intended actions, and those are Claim and Return.
```

**FIND (FAQ):**
```
There is nothing left for anyone to change.
```

**REPLACE WITH:**
```
The program's code and its fixed requirement cannot be changed, and its only intended actions are Claim and Return.
```

**WHY:** These are Revvin's own corrections from the first checklist and he was right on all three. The vault IS controlled by the program. Claim and Return are live functions. Saying nothing can ever happen to it is wrong.

---

## REPLACE 6 — ADD THIS (it is verified and it is strong)

Add to the Holding Pays section, right after the fee table:

```
Once a token switches to Holder Rewards, pump.fun does not allow it to switch back. That is pump.fun's own rule, stated in their 12 September announcement.
```

**WHY:** This is sourced directly from pump.fun's official launch thread. It is a permanent, verifiable fact that makes the rewards section stronger. Worth having.

---

# THINGS TO DELETE OUTRIGHT

These read as machine-written and undercut the credibility of a page whose whole edge is precision. No replacement needed, just cut.

| Delete this | Where |
| --- | --- |
| `That's it. That's the pitch. Huh.` | end of "Why anybody is still here" |
| `The work is the roadmap.` | under the Bricks section |
| `Milestones, not promises.` | start of "Next stop" |

Replace `Nobody here is holding a roadmap.` with:
```
Everyone here is holding a timestamp you can still open, and a JPEG you can still decode.
```

Replace `Not a link. The picture.` with:
```
The picture itself went into a mainnet transaction.
```

---

# DO NOT TOUCH — VERIFIED CORRECT

Do not let anyone "fix" these. I checked every one against the chain today.

- 959.9M supply — live: 959,904,004.86
- 0 / 0 buy / sell tax — no transfer fee, hook, or permanent delegate extension
- Token-2022 — confirmed
- Mint / freeze both null — confirmed
- 6 decimals — confirmed
- 43.83 percent of supply — 420,690,000 / 959,904,004.86 = 43.8263%
- slot 447120727 coin tx, version 1 — confirmed
- slot 447120728 image tx, version 1 — confirmed
- all four authorities revoked, supply 1 — confirmed
- `data:image/jpeg;base64` URI — confirmed
- `token → A9AHYeqb` and `mime → image/jpeg` — confirmed
- 1.81 SOL / 1,807 payments / 207 batches — measured from chain
- vault program and deed addresses — confirmed
- upgrade authority `none` — confirmed, control-tested against two programs that still have live authorities

---

# THE RULE THAT PREVENTS A REPEAT

**Never publish a number that changes.** Market cap, pool totals, distribution counts, and the current fee rate all move. Either stamp them "measured at [date]" or link a live source.

**Fixed numbers are safe forever:** 0.950%, 0.050%, 98,240 SOL, 420,690,000, 43.83%, slots 447120727 and 447120728, supply 959,904,004.86.

---

# ONE PARAGRAPH TO SEND HIM

> Rev, six find-and-replace fixes and the site is clean. The big one is the testnet line, which appears twice and has no evidence behind it anywhere, so cut it. Next is the fee rate: it is not 0.75 percent, it is 0.700 percent and it moves with market cap, so stop publishing a current number and point at pump.fun/docs/fees. Then the fee table needs SOL-denominated rows instead of dollars, the liquidity figure is roughly 61 million not 92.9 million, and your own vault wording corrections still need to go in. There is also one verified fact worth adding about Holder Rewards being irreversible. Everything else on the site checks out, including the supply, the tax, the sealed authorities, the transaction slots, and the 43.83 percent. Full strings to paste are in the sheet.
