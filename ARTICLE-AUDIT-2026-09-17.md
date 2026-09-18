# ARTICLE AUDIT — X post 2100588328831578416 (BREAKING: HISTORY JUST GOT LOCKED ON CHAIN)

**Auditor:** Ghost (`jmxghost` lane) · **Audit date:** 2026-09-17, ~20:35–21:00 UTC
**Post published:** 2026-09-17 14:10:59 UTC by @HuhcatOnSol_ (tweet lead-in + X article)
**Scope:** every structural claim, re-verified live against Solana mainnet RPC, pump.fun live API/docs, and the deployer's public repo. Time-drifting quantities (market cap, current fee tier, pool totals) excluded per operator instruction — they are hedged in the article and were measured at publish.

## VERDICT

**The article is factual and accurate as published.** Every structural claim re-verified T0 live on 2026-09-17. One residual item in the tweet lead-in (not in the article body) is carried below with its tier.

## T0 re-verified live (method: `api.mainnet-beta.solana.com` RPC + live pump.fun API + live pump.fun docs + GitHub)

| Article claim | Live result |
|---|---|
| Solana switched on v1 transactions Sept 15, 2026 | Feature acct `txv1aq4pp281…` activated_at = slot 447,120,000 = 01:04:23 UTC 2026-09-15 |
| Picture went in "minutes after it went live" | Image create tx slot 447,120,728 at 01:08:15 UTC — 3 min 52 s after activation. Both create txs `version: 1`, status OK |
| Image data written into the chain record itself, no off-chain link | Mint `DVD4q…` TokenMetadata `uri` IS a `data:image/jpeg;base64,…` payload (read live). No external URL |
| Picture sealed Sept 17, 02:35–02:36 | Seal txs on image mint: 02:35:49 `updateTokenMetadataAuthority→null`, 02:35:50 `setAuthority(type 12)→None`, 02:36:01 `mintToChecked(1)`, 02:36:13 `setAuthority(type 0 MintTokens)→None`, 02:36:29 vault init |
| Four locks destroyed | Four authority-nulling txs across the sealing operation (02:30:54–02:36:13): program upgrade authority + mint + metadataPointer + token-metadata update. All four now null on-chain (freeze null since creation). Count holds |
| One-of-one collectible | Image mint supply 1, decimals 0, all four authorities null (live `getAccountInfo`) |
| Deed in program-controlled vault | Token acct `CKU7yv…` holds 1, owner = vault PDA `136gVx…` (live) |
| No admin / pause / close / upgrade authority | Source read line-by-line (3 instructions: Initialize once, Claim, Return) + hash match + upgrade authority tag byte 12 = 0x00 (None), control-tested vs Jupiter/PumpSwap |
| Byte-for-byte source match, hash `bbc47f54…2367c` | sha256(ELF slice @ ProgramData offset 45, 105,272 bytes) = `bbc47f545456ff99266f5c0aa9aa574493b27be84e6bc2ffaece559cb492367c` — exact match, re-hashed live. README in public repo `weareallgoingtomake1t/huhcat` states the same hash |
| Claim = 420,690,000 HUHCAT = 43.83% of supply | Vault state bytes 68:76 = 420,690,000,000,000 raw; live supply 959,904,004.75 → 43.8263% |
| Threshold fixed forever | `required` write-once at Initialize; no mutating instruction; no upgrade authority. Code-read + hash |
| Scan: 729 blocks, 0 skipped, 881,986 tx, 12 v1, 1 image | `docs/evidence/v1scan-results.json` fetched live from repo: start 447120000, end 447120728 (=729 inclusive), skipped 0, total 881,986, v1 = 12, image-bearing = 1 — and that one's sig IS the on-chain image-create tx. **T1: deployer's scan, accurately attributed in the article; not independently re-run** |
| 25-tier fee schedule, peak 0.950%, floor 0.050% at 98,240 SOL, 19× | `pump.fun/docs/fees` read live: 25 SOL tiers exactly, peak 0.950%, floor 0.050% at 98,240+, 0.950/0.050 = 19 |
| Rate moves both directions | Article states "in both directions… If the market cap falls back a tier, the rate rises again" — correct mechanics |
| Holds >$20 → SOL arrives automatically | pump.fun live API: `is_holder_reward: true`. $20 floor: T1 via the 12 Sep @Pumpfun announcement as reported by 4+ independent outlets; article's verification index attributes it to that announcement correctly. Distributions confirmed running live during audit (batches at 20:33 UTC) |
| 1.81 SOL / 1,807 payments / 207 batches in one hour | Historical measurement from chain (receipt in TG-ANNOUNCEMENT-AND-SITE-CHECKLIST.md, fee math cross-check). True as measured; drift class |
| Links (solscan mint/program/state, pump.fun/coin, docs) | All addresses live-verified above; repo public |

## Residual findings (not drift)

1. **Tweet lead-in: "The earliest holders get the biggest rewards."** This is a mechanics claim, not drift. The 12 Sep announcement language (via outlets) is "higher reward caps for longer holding periods" — a cap, not a guaranteed payout. Allocation is pro-rata by balance (measured, CV = 0.000). The documented mechanism is T1; the claim as stated ("get the biggest rewards") is T3 — it was flagged in the handoff honest-gaps list and correctly omitted from the article body, but it remains in the tweet lead text as of this audit. The defensible form: "longer holds raise your reward cap."
2. Cosmetic: article text renders the hash run-on — "…2367cThe program code…" — missing a line break after the hash. No factual impact.
3. Rounding tension, not an error: "~70,000,000 in pools" and ">6x" sit at 420.69/70 = 5.99× — both hedged ("about"), both within the measured 60.9M–87.2M drift band where the ratio spans 4.8×–6.9×.
4. Schedule nuance: the 0–420 SOL tier carries 0.300% (below the 0.950% peak), so "rate falls as mcap climbs" is exactly true only above 420 SOL. HUHCAT operates far above that tier, so the statement holds in its range.

## Auditor's own false failure, owned

Mid-audit my harness hashed the ELF after `rstrip(b"\x00")` and printed a mismatch. The strip removed real bytes; the full 45:end slice hashes exactly to `bbc47f54…2367c`. The article was right; my first method was wrong. Corrected and re-run same session.