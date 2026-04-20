# My Top 10 Claude Ecom Hacks — Elite Edition

**Live workshop with Paul Waddy's community — 20 April 2026**
**Presenter:** Luke Heka, Selr AI — [selrai.com.au](https://selrai.com.au)

---

## Before you start

**What you need:** Claude.ai (Pro recommended for long inputs), or Claude Desktop (free, unlocks MCP connections to Shopify / Meta Ads / etc.).

**Time per hack:** 10-15 min to run first time. 2-5 min once set up.

**No technical skills for Hacks 1-7.** Copy, paste, swap the `[[DOUBLE BRACKETS]]` bits, run.

**Hacks 8-10 are elite tier.** They connect Claude live to your Meta Ads, Shopify, and Higgsfield accounts. One-time setup of 10-30 minutes each. Every future analysis is instant. This is the difference between "AI tools" and "AI owning part of my business."

These aren't surface prompts. Each one is a multi-phase system with input audits, framework-grounded reasoning, schema-locked outputs, and self-critique loops. Battle-tested on Shopify stores doing $500K to $20M+ ARR.

**How to read them:** each prompt has a Phase 0 audit. That's Claude checking whether your inputs are strong enough. If they're weak, Claude tells you exactly what to add before proceeding. Do not skip this — it's the difference between generic output and elite output.

---

## IF YOU ONLY SET UP ONE THING TODAY

**→ Hack 10: Shopify ↔ Claude Direct Connection (the capstone).**

Every other hack in this workshop becomes 10x more powerful once Claude can see your real store data. 10 minutes to set up. Direct API via MCP server. No Zapier, no n8n, no middleware tax. That's the elite stack.

---

## The 10 hacks at a glance

| # | Hack | What dies | Framework spine |
|---|------|-----------|-----------------|
| 1 | Customer Voice Transplant | Brand-voice product pages that don't convert | Schwartz 5 Awareness + JTBD |
| 2 | Awareness-Level Creative Matrix | Ad fatigue, "we only run 3 ads" | Schwartz + Halbert Starving Crowd |
| 3 | Support Clone (500+ tickets) | 4 hours/day on replies + voice drift | Voss tactical empathy + Ritz-Carlton |
| 4 | Post-Purchase LTV Engine | Leaky "thanks for your order" flows | BJ Fogg behavioural model |
| 5 | Review → UGC Brief Factory | Bad briefs = bad UGC = wasted spend | Story Arc + Hook-Hold-Close |
| 6 | Review Response Generator | Generic public replies that tank trust | Voss labelling + Ritz-Carlton + E-E-A-T |
| 7 | 30-Day Organic Content Engine | Posting inconsistency + generic slop | Content Pillars + Hook Bank + Founder Voice |
| 8 | Meta Ads Performance Debugger (MCP) | Burning $$ on dying ads | Diagnostic hierarchy CPM→CTR→CVR→ROAS |
| 9 | Higgsfield + Claude Pipeline (Soul ID) | Beautiful AI slop that doesn't convert | Strategy → Script → Scene prompts → Assembly |
| **10** | **Shopify ↔ Claude Direct Connection** | **Zapier subscriptions + $2k/mo agency dashboards** | **Direct Admin API via MCP, zero middleware** |

---

## The stack (how the hacks feed each other)

```text
HACK 10 (Shopify MCP) ─────────────────────────────┐
  │                                                │
  ├─→ HACK 1 (Voice Transplant) ← real reviews     │
  ├─→ HACK 2 (Creative Matrix) ← real products     │
  ├─→ HACK 3 (Support Clone) ← real tickets        │
  ├─→ HACK 4 (LTV Engine) ← real order history     │
  ├─→ HACK 5 (UGC Brief) ← real product data       │
  ├─→ HACK 6 (Review Response) ← live reviews      │
  ├─→ HACK 7 (Content Engine) ← real products      │
  ├─→ HACK 8 (Meta Debugger) ← real customer LTV ──┘
  └─→ HACK 9 (Higgsfield) ← real product images

HACK 8 (Meta Ads MCP) — direct token auth, zero middleware
HACK 9 (Higgsfield Ultra) — Soul ID training unlocks everything
```

**Each prompt lives in its own file in the `prompts/` folder. Copy the full prompt from there.** Short summaries below with links to each file.

---

# HACK 1 — Customer Voice Transplant

**What it does:** Mines verbatim customer phrases from reviews, maps them to Schwartz's 5 Awareness Levels, diagnoses where your page speaks in brand voice when customers speak in a different voice, rewrites in their words with a self-critique loop.

**Why it works:** Your brand voice is written for you. Your customer's voice is what converts other customers. This prompt refuses to write anything generic because it audits inputs first and loops its own output against a sceptical mobile shopper.

**Minimum input:** 20-50 customer reviews (more = better). Current product page URL or copy. 1-line avatar.

**Time saved:** 2-3 hours of senior copywriter work per product.

**Full prompt:** [`prompts/01-customer-voice-transplant.md`](prompts/01-customer-voice-transplant.md)

---

# HACK 2 — Awareness-Level Creative Matrix

**What it does:** One product in, 10 ad angles out. Each angle mapped to a Schwartz awareness level (Unaware → Problem → Solution → Product → Most aware). Every angle has hook + body + CTA drafted for 9:16 and 1:1.

**Why it works:** Most founders run 2-3 ads targeting the same awareness level. Top performers run 30, covering cold strangers to warm fans. This prompt forces the full range in one session.

**Minimum input:** One product + winning review quote from Hack 1.

**Time saved:** 6-8 hours of media buyer + creative strategist work.

**Full prompt:** [`prompts/02-creative-matrix.md`](prompts/02-creative-matrix.md)

---

# HACK 3 — Support Clone (Elite v3 — 500+ tickets)

**What it does:** Trains a co-pilot on 500-2,000 of your real support tickets. Extracts your voice fingerprint across 7 dimensions (lexicon, cadence, openers, apologies, humour, closers, escalation markers). Deploys as Claude Project with channel-specific response matrix (email / SMS / IG DM / chat). Surfaces the top 5 revenue leaks hiding in your tickets as a free bonus.

**Why v3 beats v2:** 15 tickets = toy. 500+ = actual tone signal. The clone sounds like the founder, not a DTC support bot.

**Minimum input:** 500 tickets from Gorgias / Zendesk / Shopify Inbox (CSV export). Bootstrap mode if you have <500.

**Time saved:** 3-4 hours/day across support team. Plus the pattern report replaces a $2k/mo CRO audit.

**Elite upgrade:** Connect via Shopify MCP (Hack 10) so the clone knows customer LTV + order history before drafting.

**Full prompt:** [`prompts/03-support-clone.md`](prompts/03-support-clone.md)

---

# HACK 4 — Post-Purchase LTV Engine

**What it does:** Builds a 30-day post-purchase sequence (email + SMS) structured as PROTECT → ACTIVATE → UNLOCK. Uses BJ Fogg's behaviour model (Motivation × Ability × Prompt) to time each trigger against the customer's product journey. Includes replenishment math (day-X cross-sell fires when the product empties, not arbitrarily).

**Why it works:** Retention is where the money lives. Most post-purchase flows are one "thanks for your order" email. This builds a full cohort nurture.

**Minimum input:** Product details, repeat-purchase cycle (days), brand voice.

**Time saved:** 2 weeks of email strategist + Klaviyo build work.

**Full prompt:** [`prompts/04-post-purchase-ltv.md`](prompts/04-post-purchase-ltv.md)

---

# HACK 5 — Review → UGC Brief Factory

**What it does:** Turns customer reviews into a complete UGC brief for a creator: story arc (Problem → Struggle → Discovery → Transformation), hook-hold-close script, shot list, b-roll, voiceover guidance. The creator gets the plot, not a shot list.

**Why it works:** Briefs are the #1 reason UGC underperforms. Brands send creators product specs. Winners send creators a STORY.

**Minimum input:** Product + 10 reviews + 1 creator persona.

**Time saved:** Creator works faster, ads perform 2-3x better.

**Full prompt:** [`prompts/05-ugc-brief-factory.md`](prompts/05-ugc-brief-factory.md)

---

# HACK 6 — Review Response Generator

**What it does:** Writes every public review reply across Yotpo, Okendo, Judge.me, Stamped, Loox, Google Business Profile. Different templates per star rating (5-star 30-60 words; 1-star 60-100 words with Ritz-Carlton recovery). Built-in SEO boost (E-E-A-T signal). Flags fake reviews. Surfaces pattern intelligence as a free bonus.

**Why it works:** The real audience of a review reply is the NEXT customer reading it, not the reviewer. This one rule changes everything.

**Minimum input:** Batch of reviews (5-50). Brand voice profile.

**Time saved:** 1-2 hours/week. Review-response SEO lift is 3-6 months cumulative.

**Full prompt:** [`prompts/06-review-response-generator.md`](prompts/06-review-response-generator.md)

---

# HACK 7 — 30-Day Organic Content Engine

**What it does:** Maps 22 posts across 5 pillars (Education / BTS / Product-in-use / Social-proof / POV) for TikTok, Reels, LinkedIn, Shorts, Pinterest. Includes 12-pattern hook bank (≥8 must be used), founder-voice extraction, and a repurpose matrix (one idea → 5 platforms).

**Why it works:** Gary Vee's "document, don't create." Founder voice beats production value. This forces a pillar mix that can't be generated by AI alone.

**Minimum input:** Hero product, founder voice sample (1 voice memo or 10 tweets), 3 competitor handles.

**Time saved:** 1 hour/week posting + 4 hours/month planning. Cap founder effort at 2 hrs/week for filming.

**Full prompt:** [`prompts/07-organic-content-engine.md`](prompts/07-organic-content-engine.md)

---

# HACK 8 — Meta Ads Performance Debugger (Elite v3 — MCP-First)

**What it does:** Connects Claude Desktop to your Meta Ads account via direct Meta Ads MCP (System User token, never expires). 9-tool call sequence reads your account like a doctor reads labs. Kill list + scale list + leak diagnostic (creative vs audience vs landing page vs offer) + next 3 tests + compliance scan. AU-specific benchmark table included.

**Why v3 beats v2:** MCP = live account read in seconds. CSV paste is now the fallback mode (MODE C). Elite ecom founders don't export CSVs; they query live.

**Setup:** Meta Business Suite → System Users → generate token → install `meta-ads-mcp` → paste config. 10 min, one-time. Full walkthrough in the prompt file.

**Minimum input (MCP mode):** Ad account ID, target CPA, target ROAS, AOV, margin, vertical. Claude pulls the rest.

**Time saved:** 4-6 hours per audit. Replaces most "paid media agency reporting retainer" work.

**Full prompt:** [`prompts/08-meta-ads-debugger.md`](prompts/08-meta-ads-debugger.md)

---

# HACK 9 — Higgsfield + Claude Creative Pipeline (Elite v3 — Soul ID)

**What it does:** Full creative pipeline from one product to 4 testable ads. Strategy → timestamped script → scene-by-scene Higgsfield prompts (A/B/C variations per scene) → negative prompt library → overlay map → audio design (audio-on + audio-off versions) → CapCut assembly shot sheet → 3 creative variations → cost math. Trains Soul IDs (founder + product) so every ad is brand-consistent.

**Why v3 beats v2:** Soul ID training protocol included. Batch gen (3 variations per scene, never ship first gen). Negative prompt library. Full production economics. This is the difference between "I made an AI ad and it looks weird" and "I ship 4 tested variations per product per week."

**Setup:** Higgsfield Ultra ($49/mo) + 40 founder photos + 30-50 product photos. Train 2 Soul IDs (60 min, run in background). One-time.

**Minimum input:** Product, brand reference grid, hex codes, angle from Hack 2, winning review quote from Hack 1.

**Time saved:** 80% reduction in creative production cost vs UGC shoots. Faster variation testing.

**Full prompt:** [`prompts/09-higgsfield-creative-pipeline.md`](prompts/09-higgsfield-creative-pipeline.md)

---

# HACK 10 — Shopify ↔ Claude Direct Connection (THE CAPSTONE)

**What it does:** Connects Claude Desktop directly to your Shopify Admin API via MCP server. No Zapier, no n8n, no middleware. Once connected, you ask questions in plain English: "top 20 products by margin × velocity," "customers who haven't bought in 90 days with LTV >$300, draft win-backs," "SKUs that will stock out in 14 days, draft POs." Bulk operations gated with dry-run + confirmation.

**Why it's the capstone:** Every other hack in this workshop becomes 10x more powerful once Claude can see real store data, not imagined examples. This is the move from "I use AI for prompts" to "AI runs parts of my business."

**The elite setup (Path A):**
1. Shopify Admin → Settings → Apps and sales channels → Develop apps → Create app
2. Configure Admin API scopes (start READ-ONLY, add writes later)
3. Install → copy the Admin API access token (shown once)
4. Install the MCP server: `npm install -g @ajackus/shopify-mcp-server` (community Admin API MCP — the official `@shopify/dev-mcp` is for docs only, doesn't access your store data)
5. Paste config into `claude_desktop_config.json` with shop domain + token
6. **Fully quit Claude Desktop (Cmd+Q) and reopen** — not just close the window
7. Test: "Use the Shopify MCP. Run `shop_info`."

**The broader pattern:** if a platform has an API, you don't need Zapier. API key → MCP server → Claude. That stack beats every bridge tool. Same playbook for Meta Ads (Hack 8), Klaviyo, Gorgias, Stripe, Google Analytics.

**First 10 queries after you connect:** see the prompt file — copy-paste ready.

**Time saved:** Replaces most $2k/mo agency dashboard retainers. Sub-second query speed vs 2-5s Zapier latency.

**Full prompt + setup walkthrough:** [`prompts/10-shopify-connection.md`](prompts/10-shopify-connection.md)

---

## Level-up stack (all 10 hacks on autopilot)

Everything in this workshop is deliverable with pure prompt + MCP setup. No agents required. But if you want to go beyond prompts, here's what's next.

### Layer 1 — Claude Projects (free, inside Claude)

- Save each hack as a Project with the system prompt + knowledge docs
- Upload your brand voice guide, review CSV, product data
- One Project per hack; launch with Project-specific prompt
- Works today with nothing installed

### Layer 2 — MCP connectors (free-$49/mo, Claude Desktop)

- **Shopify MCP** (Hack 10) — ALL store data, live
- **Meta Ads MCP** (Hack 8) — live ad account read + scale/kill
- **Klaviyo MCP** — flow analysis, cohort builds, campaign drafts
- **Gorgias / Zendesk MCP** — live ticket read for Hack 3 clone
- **Stripe MCP** — subscription analysis, MRR cohorts
- **Google Analytics MCP** — attribution deep-dive
- Install once per tool, integrate into every hack

### Layer 3 — Scheduled agents (n8n, cron, Claude Desktop schedule)

- Monday 9am: Meta Ads debugger runs on last 7 days, drops report in Slack
- Wednesday 9am: Shopify inventory risk check + supplier POs drafted
- Friday 3pm: Review response generator runs on week's new reviews, submits to review platform
- This is where we build custom for clients at Selr AI

### Layer 4 — Custom agents + workshops

- If you're doing >$1M/yr and want this fully built, not DIY
- Come to the Sydney 2-day workshop (22-23 April 2026)
- DM Luke on Instagram or LinkedIn

---

## The rules for every prompt

1. **Do the audit.** Phase 0 exists to stop you giving Claude rubbish inputs. If it flags WEAK, fix the inputs.
2. **Feed winners forward.** Hack 1 feeds Hack 2. Hack 2 feeds Hack 9. Every winning review quote, hook, angle goes into the next prompt. Never start from scratch twice.
3. **Save the voice fingerprint once.** Hacks 3, 4, 5, 6, 7 all need brand voice. Build once in Hack 3, reuse everywhere.
4. **Connect the live data when possible.** A Meta Ads MCP or Shopify MCP query beats a CSV paste every time. Direct API beats middleware every time.
5. **Never copy-paste without editing the bracketed inputs.** `[[THIS]]` must be YOUR data. Nothing generic survives.

---

## One-line summary per hack (for the Zoom chat)

- **H1 Voice Transplant** — [`prompts/01-customer-voice-transplant.md`](prompts/01-customer-voice-transplant.md)
- **H2 Creative Matrix** — [`prompts/02-creative-matrix.md`](prompts/02-creative-matrix.md)
- **H3 Support Clone** — [`prompts/03-support-clone.md`](prompts/03-support-clone.md)
- **H4 LTV Engine** — [`prompts/04-post-purchase-ltv.md`](prompts/04-post-purchase-ltv.md)
- **H5 UGC Brief** — [`prompts/05-ugc-brief-factory.md`](prompts/05-ugc-brief-factory.md)
- **H6 Review Response** — [`prompts/06-review-response-generator.md`](prompts/06-review-response-generator.md)
- **H7 Content Engine** — [`prompts/07-organic-content-engine.md`](prompts/07-organic-content-engine.md)
- **H8 Meta Debugger (MCP)** — [`prompts/08-meta-ads-debugger.md`](prompts/08-meta-ads-debugger.md)
- **H9 Higgsfield Pipeline** — [`prompts/09-higgsfield-creative-pipeline.md`](prompts/09-higgsfield-creative-pipeline.md)
- **H10 Shopify Connection ★** — [`prompts/10-shopify-connection.md`](prompts/10-shopify-connection.md)

---

Questions? DM Luke on Instagram [@lukeheka](https://instagram.com/lukeheka) or LinkedIn.
Join the Sydney 2-day workshop 22-23 April: [selrai.com.au/workshops](https://selrai.com.au/workshops).
