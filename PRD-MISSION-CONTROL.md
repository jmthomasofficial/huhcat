# PRD — MISSION CONTROL (HUHCAT community web app)

**Companion to MASTERPLAN.md + MARATHON-7DAY.md.** Ghost-authored, built on audited Deckard research (fabrications removed).

## 1. PURPOSE (one sentence)

Mission Control removes every friction between a holder deciding to promote $HUHCAT and actually publishing good, fact-locked content today.

## 2. NORTH STAR

Actions per holder per week (a "promoter action" = a personalized mission completed with posted proof). Every feature either raises that number or it gets cut.

## 3. FRICTIONS THE APP MUST KILL (from the audited friction analysis)

| # | Friction | Kill feature |
|---|---|---|
| F1 | "I don't know what to say" | Daily Mission cards with fact-locked, fill-in-the-blank templates |
| F2 | "I'll look dumb / cringe" | Personalization slots ([YOUR_REASON]) + the fact that every post is anchored to a verifiable link, so the post can't be wrong |
| F3 | "I don't know the facts" | The Fact Vault: every template embeds only pre-verified facts, with source links; nothing unverified can ship from the app |
| F4 | "My account is small, why bother" | Community meter: every action feeds a visible aggregate (week total, streak flame count) so small accounts see their contribution count in a bigger thing |
| F5 | "Making content is hard" | One-click Story Card generator + embedded meme maker (canvas, renders locally, nothing uploaded) |
| F6 | "Posting everywhere is tedious" | Per-platform output sizing (1080×1080 / 9:16 / 16:9) from one asset; native share links prebuilt |
| F7 | "I don't know if I qualify for rewards" | Wallet check: read-only balance fetch → shows live balance vs the $20 floor |
| F8 | "I missed the start / momentum died" | Streaks + seasons (the app makes the campaign continuous, momentum never sees a finish line) |

## 8 fabrications from the research phase, REJECTED and forbidden in this app: multiplied holder rewards, custom fee-rate API keys, redirected per-post SOL payouts, community-vote supply changes, "only image in Solana history" (must stay scoped to v1), scan attribution errors, "1,807 holders", and any content implying access to the real cat.

## 4. PHASE 1 (static GitHub Pages, ship in 48h)

Single-page app, no backend, everything client-side:

| ID | Feature | Spec |
|---|---|---|
| P1-1 | Daily Mission Board | 3 mission cards/day from a dated JSON file in the repo. Mission = template + platform + points + proof instruction. Team edits JSON; site updates on push |
| P1-2 | Fact Vault | `facts.json` = the canonical verified fact set with source links (the audit-clean set: supply 959,904,004 live, 43.83%, 4 authorities null, hash bbc47f54…, slots, $20 floor, tier bounds 0.950%/0.050%, measured 1.81 SOL/hr snapshot labeled with date). Templates render FROM this file, so a fact correction updates every template in one push |
| P1-3 | Content Kit | 8 X templates + 4 video scripts + 2 IG templates + reply kit, each with [YOUR_REASON] slots; copy-to-clipboard, per-platform aspect export |
| P1-4 | Story Card Generator | Canvas: pick template → renders verified fact + real cat image + user's custom line → PNG download. No server, no upload |
| P1-5 | Meme Maker | Port the existing huhcatonsol.com browser meme maker (already built, reuse the code) |
| P1-6 | Wallet Check | "Message signing" = sign a nonce to prove ownership (read-only, no approval, no spending). Display: balance vs $20 floor, holder-rewards eligibility, live tier link to pump.fun/docs/fees. Never store keys, never ask for seed phrases |
| P1-7 | Missions Board + Proof Gallery | A GitHub Actions daily run that pulls #proof posts from the TG bot export and renders a public wall-of-fame grid. [TG export API access needed — verify during build] |
| P1-8 | Streak + Season display | Client-side localStorage + optional wallet-signed "claim streak" (signed message stored in repo via GitHub Action from team-side form). Phase 1 honest-manual, Phase 2 automated |

**Phase 1 success = the app is useful with zero server cost and zero key exposure, and every fact on it is traceable to a source link.**

## 5. PHASE 2 (backend, after the first marathon, informed by telemetry)

| ID | Feature | Spec |
|---|---|---|
| P2-1 | Mission Control API | Real leaderboard: wallet-verified accounts, mission completions, XP, streaks, referral trees |
| P2-2 | Referral tracking | Signed referral codes; credits referrer on invitee's first verified action (never on purchase) |
| P2-3 | Content audit queue | Team-only view of content flagged by the honesty filters before it enters the wall |
| P7-2 A/B variants | Template A/B per season with per-template engagement (clicks on the short link per template) |
| P2-4 | Anti-abuse | Rate limits, dedupe (identical text/asset = zero points, first warning), pod-pattern detection (synchronized like/comment clusters), multi-account heuristic (same wallet cluster, stylometric similarity). Enforcement ladder: void points → 48h hold → ban |
| P2-5 | Season engine | Seasonal resets, titles (Kitten/Cat/Top Cat/Alpha Cat), season archive pages (public, permanent, linkable proof of the community's real history) |

## 6. DESIGN PRINCIPLES

1. **Facts are load-bearing.** If it renders in the app, it traces to a source. The Fact Vault is the single source of truth, versioned in the repo. No fact ships without a link.
2. **No key exposure, ever.** Read-only RPC + nonce signing only. No transaction is ever constructed by the app. No seed phrase input, ever.
3. **Honest metrics only.** The app displays real counts (posts, streaks, members), never vanity-inflated ones. No view-count fabrication, no bot counters.
4. **Small account dignity.** UI explicitly celebrates first-time posters, streak starts, "first video ever posted" badges. The 237-person community is the product; everyone sees everyone.
5. **Public copy gate.** All default template text ships at 100/100 on the slop analyzer, and the Fact Vault keeps template copy re-rendered from the gated text, so updates inherit the gate.

## 7. TECH

Phase 1: static site on GitHub Pages (free, aligned with the "no treasury" story), vanilla JS or light framework, all data as dated JSON in repo, GitHub Actions for the daily proof-wall rebuild. Phase 2: small Node/Cloudflare Workers API + KV or a tiny Postgres. Wallet adapter: standard open-source Solana wallet adapters, nonce-sign only. RPC: public mainnet endpoint with a cached supply/tier read (refreshed hourly, timestamped on display).

## 8. OUT OF SCOPE (v1)

Trading features, price charts in-app (link out to DexScreener instead), any token-based reward automation (legal cliff, see MASTERPLAN), auto-posting to platforms (API ToS + authenticity risk — the app prepares content, humans post it), DM automation.