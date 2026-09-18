# Graph Report - huhcat  (2026-09-16)

## Corpus Check
- 4 files · ~269,665 words
- Verdict: corpus is large enough that graph structure adds value.

## Summary
- 63 nodes · 109 edges · 12 communities (9 shown, 3 thin omitted)
- Extraction: 95% EXTRACTED · 5% INFERRED · 0% AMBIGUOUS · INFERRED: 5 edges (avg confidence: 0.5)
- Token cost: 0 input · 0 output

## Graph Freshness
- Built from commit: `3717e981`
- Run `git rev-parse HEAD` and compare to check if the graph is stale.
- Run `graphify update .` after code changes (no API cost).

## Community Hubs (Navigation)
- HUHCAT Website Handoff — CA Verification & Alignment
- a
- index-C1purPdB.js
- Xt
- sd
- Vo
- xd
- tc
- ad
- zd
- 5. Token `A9AHYeqb7nQk7LZUraw7rBCzYRjy2DRvE6NqWfFHKRdH` — what metadata URI actually is
- od

## God Nodes (most connected - your core abstractions)
1. `xd()` - 12 edges
2. `sd()` - 11 edges
3. `Xt()` - 9 edges
4. `RESEARCH — Solana V1 transactions and on-chain image “inscriptions”` - 9 edges
5. `a()` - 7 edges
6. `Wd()` - 6 edges
7. `tc()` - 5 edges
8. `Vo()` - 4 edges
9. `pd()` - 4 edges
10. `Do()` - 4 edges

## Surprising Connections (you probably didn't know these)
- `od()` --calls--> `a()`  [EXTRACTED]
  game/assets/index-C1purPdB.js → game/assets/index-C1purPdB.js  _Bridges community 1 → community 11_
- `sd()` --calls--> `a()`  [EXTRACTED]
  game/assets/index-C1purPdB.js → game/assets/index-C1purPdB.js  _Bridges community 1 → community 4_
- `sd()` --calls--> `Vo()`  [EXTRACTED]
  game/assets/index-C1purPdB.js → game/assets/index-C1purPdB.js  _Bridges community 5 → community 4_
- `sd()` --calls--> `ud()`  [EXTRACTED]
  game/assets/index-C1purPdB.js → game/assets/index-C1purPdB.js  _Bridges community 11 → community 4_
- `ad()` --calls--> `sd()`  [EXTRACTED]
  game/assets/index-C1purPdB.js → game/assets/index-C1purPdB.js  _Bridges community 4 → community 8_

## Import Cycles
- None detected.

## Communities (12 total, 3 thin omitted)

### Community 1 - "a"
Cohesion: 0.24
Nodes (10): a(), _d(), f(), Fd(), Fo(), Ho(), md(), pd() (+2 more)

### Community 2 - "index-C1purPdB.js"
Cohesion: 0.29
Nodes (5): dd, lc, nc, rc, te

### Community 3 - "Xt"
Cohesion: 0.22
Nodes (13): Bo(), Do(), gd(), hd(), Ja(), jd(), Ka(), tc() (+5 more)

### Community 4 - "sd"
Cohesion: 0.50
Nodes (4): Ed(), kd(), sd(), Td()

### Community 5 - "Vo"
Cohesion: 0.50
Nodes (4): id(), ld(), rd(), Vo()

### Community 6 - "xd"
Cohesion: 0.29
Nodes (6): 3. Are there documented “inscriptions” on Solana?, 4. Disconfirming evidence (bear case), Executive read, Judgment, RESEARCH — Solana V1 transactions and on-chain image “inscriptions”, Sources retrieved 2026-09-15

### Community 7 - "tc"
Cohesion: 0.50
Nodes (4): 1. Is there an official “V1 transaction” format in 2026?, Mainnet activation — docs disagree; chain is T0, Official distinction, SIMDs (not Token-2022)

### Community 9 - "zd"
Cohesion: 0.50
Nodes (4): 2. Actual mechanism for embedding an image in token metadata, Metaplex Token Metadata (PDA, not the mint), Token-2022 (on the mint), What is *not* documented

### Community 10 - "5. Token `A9AHYeqb7nQk7LZUraw7rBCzYRjy2DRvE6NqWfFHKRdH` — what metadata URI actually is"
Cohesion: 0.67
Nodes (3): 5. Token `A9AHYeqb7nQk7LZUraw7rBCzYRjy2DRvE6NqWfFHKRdH` — what metadata URI actually is, Coin mint (the CA) — **T0** `getAccountInfo` 2026-09-15T17:51:48Z, Companion mint (where the data URI actually lives) — **T0**

## Knowledge Gaps
- **19 isolated node(s):** `dd`, `nc`, `rc`, `lc`, `te` (+14 more)
  These have ≤1 connection - possible missing edges or undocumented components.
- **3 thin communities (<3 nodes) omitted from report** — run `graphify query` to explore isolated nodes.

## Suggested Questions
_Questions this graph is uniquely positioned to answer:_

- **Why does `RESEARCH — Solana V1 transactions and on-chain image “inscriptions”` connect `xd` to `zd`, `5. Token `A9AHYeqb7nQk7LZUraw7rBCzYRjy2DRvE6NqWfFHKRdH` — what metadata URI actually is`, `tc`?**
  _High betweenness centrality (0.064) - this node is a cross-community bridge._
- **Why does `1. Is there an official “V1 transaction” format in 2026?` connect `tc` to `xd`?**
  _High betweenness centrality (0.024) - this node is a cross-community bridge._
- **Why does `2. Actual mechanism for embedding an image in token metadata` connect `zd` to `xd`?**
  _High betweenness centrality (0.024) - this node is a cross-community bridge._
- **Are the 3 inferred relationships involving `a()` (e.g. with `_d()` and `md()`) actually correct?**
  _`a()` has 3 INFERRED edges - model-reasoned connections that need verification._
- **What connects `dd`, `nc`, `rc` to the rest of the system?**
  _19 weakly-connected nodes found - possible documentation gaps or missing edges._