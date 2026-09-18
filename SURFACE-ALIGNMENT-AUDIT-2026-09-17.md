# SURFACE ALIGNMENT AUDIT — GitHub Pages site + huhcatonsol.com vs the verified article

**Auditor:** Ghost (`jmxghost` lane) · **Date:** 2026-09-17, ~21:30 UTC
**Reference truth:** the X article (post 2100588328831578416, audited factual earlier this session, receipt `ARTICLE-AUDIT-2026-09-17.md`) + live chain reads + live pump.fun API/docs.
**Drift-class numbers (mcap, tier, pool totals, distribution counts) out of scope unless unhedged or unmeasured — per operator.**

## VERDICT

**GitHub Pages site (`jmthomasofficial.github.io/huhcat/`): NOW ALIGNED** — after fixing one materially false block (see fix log below). All other structural claims verified live: activation slot, both create txs (v1, one slot apart), four authorities null, supply 1 deed, vault state 420,690,000 = 43.83%, hash match, program touches = 2, fee schedule (25 tiers / 0.950 peak / 0.050 floor / 98,240 SOL / 19×), $20 floor attribution, 1.81 SOL / 1,807 / 207 hour measurement, six seal txs 02:35:49–02:36:29, "four minutes later" (= 3m52s, correct), hedged ~70M pool figure.

**huhcatonsol.com (Revvin's): NOT YET ALIGNED.** The two known real errors are still live on the page as of 21:30 UTC: the testnet claim (×2) and the unmeasured "92.9 million" pool figure. Everything else on his site that I could check agrees with the article and the chain — including the USD fee-tier table and the 0.75% figure my earlier correction sheet wrongly flagged (they were accurate at publish; operator was right). His "deployer closed their position" is T0-true (deployer wallet holds 0 HUHCAT, verified live). He holds `REVVIN-CORRECTIONS-v2.md`; it has not been applied. Do not take "done" on faith — re-pull and diff when he reports back.

## FIX LOG — our site (commit `6c6fa74`, pushed, verified live serving)

| Defect | Was | Now | Evidence |
|---|---|---|---|
| Supply card contradicted chain AND the site's own 43.83% card | "Total Supply 1,000,000,000" | "Live Supply 959,904,004 · as of 17 Sep 2026" | Chain `getTokenSupply` = 959,904,004.75. 420.69M is 43.83% of 959.9M but only 42.07% of 1B — the old page was internally contradictory |
| Fabricated allocation split | "70% Public Pool / 18% Community / 12% Team (6mo vesting)" | Single-distribution fair-launch legend, no team allocation | DexScreener: all 6 pools ≈ $148K liquidity ≈ ~97M coin-side ≈ ~10% of supply, not 70%. No on-chain basis for any 70/18/12 split; "12% team" contradicts the takeover story and the site's own footer ("no formal team") |
| Pie CSS painted 70/18/12 | conic-gradient 3 segments | single 100% arc | same |
| LP card unverifiable template claim | "LP Status: Locked 🔒 / Burned Forever" | "PumpSwap · liquidity in pump.fun's canonical pool" | pump.fun API `complete: true`; live pumpswap pair on DexScreener. "LP burned" is not a verified fact for this token |

## FLAGS — our site, not auto-fixed (operator decision needed)

1. **Lore naming conflation.** Site says "Meet **Ben Cat** … **Ben the Melbourne feline**." Two sources conflict: Know Your Meme calls the meme cat "Ben Cat" (pet of @planetvenus500); the linked SBS article names the Melbourne cat **Bender** (owner Nellie Cage, Tecoma). The current line fuses KYM's name with SBS's location. Followers/likes figures hold (TikTok live today: 3.4M followers, 104.5M hearts vs site's "over 3.2M / over 89.9M" floors). But the name+city blend is attackable. Recommend: either follow SBS fully (Bender, Melbourne) or drop the personal name.
2. Roadmap "Phase 1 — Fair Launch … LP locked, authorities revoked": the "LP locked" phrase repeats the same unverified claim; harmless in intent but same fix class as the LP card if you want it airtight.

## Revvin's site — checked items that AGREE (so his fix list is genuinely only the 2 errors)

- Coin CA, image mint, vault program, deed account, state account, hash `bbc47f54…2367c`, "upgrade authority: none" ✓
- 959.9M supply snapshot, 0/0 tax, revoked, 6 decimals ✓
- Slots 447120727/447120728, both v1, one slot apart ✓
- Vault mechanics: 420,690,000 = 43.83%, claim/return, fixed, no admin instruction ✓
- Fee schedule USD translation (0.75% today → 0.70% at $1M → 0.40% at $4M → 0.05% at $10M+): **recomputed against live pump.fun table — all four correct** (assuming ≈$101/SOL as at publish)
- "Deployer closed their position" ✓ T0 (wallet balance 0)
- Hedged honest-gambling disclaimer ✓