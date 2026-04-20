# HACK 10 — Shopify ↔ Claude Direct Connection (Elite — THE CAPSTONE)

## The REAL way to connect Claude to your Shopify store: direct Admin API via MCP server. No Zapier. No n8n. No middleware tax.

**This is the move that separates "I use Claude for prompts" from "Claude runs parts of my business." Every other hack in this workshop gets 10x more powerful once Claude can see your real store data.**

---

## THE PLAYBOOK: why direct API beats every bridge tool

Zapier, n8n, Make — all of them are middleware. They wrap the same Shopify Admin API that you can access directly with an API token. Every middleman charges you: time (setup), money (per-action fees), and latency (extra hops).

**The native stack in 2026:**

| Path | Setup | Speed | Limits | Cost | When to use |
|------|-------|-------|--------|------|-------------|
| **Direct Admin API via Shopify MCP server** (Claude Desktop) | 10 min, paste 1 config | <1s per call | None (Shopify rate limits only) | Free | THE real answer. Default to this. |
| **Direct API from Claude Code** | 2 min, paste curl commands | <1s | None | Free | Developers / power users |
| **Shopify Storefront MCP** (official Shopify, buy-side) | 5 min | <1s | Storefront scope only (no admin actions) | Free | Product search, cart, checkout agents |
| Zapier MCP | 20 min | 2-5s | 100/mo free, metered after | $29/mo+ | Last resort if you refuse to install anything |
| n8n MCP | 60 min | 2-5s | Self-hosted complexity | Free (self-hosted) | Builders with existing n8n workflows |

**Golden rule**: if a platform has an API, you never need Zapier. **API key → MCP server → Claude.** That's the stack.

---

## PATH A — THE REAL ANSWER — Shopify Custom App + MCP server

### Total time: 10 minutes, one-time. Every future analysis is instant.

### Step 1 — Create a Shopify Custom App (gives you the Admin API token)

- Shopify Admin → **Settings → Apps and sales channels → Develop apps**
- Click **Create an app**
- Name it: `Claude MCP`
- Click **Configure Admin API scopes**
- Select the scopes you need (start READ-ONLY, add writes later when you're confident):

READ (always safe, install today):

- `read_orders`
- `read_customers`
- `read_products`
- `read_inventory`
- `read_locations` (needed for fulfilment + supplier queries)
- `read_analytics`
- `read_checkouts`
- `read_draft_orders`
- `read_fulfillments`
- `read_shipping` (needed for shipping rates + draft POs)
- `read_reports`
- `read_discounts`
- `read_price_rules`
- `read_marketing_events`

WRITE (only when you're ready — these let Claude change things):

- `write_products` (for bulk description updates — Hack 1)
- `write_draft_orders` (for creating win-back drafts — Hack 4)
- `write_customers` (for tagging cohorts)
- `write_price_rules` (for discount testing)

- Click **Install app** → confirm install
- Shopify shows you the **Admin API access token** ONCE. Copy it. Format: `shpat_xxxxxxxxxxxxxxxxxxxx`
- Note your shop domain: `your-store.myshopify.com`

### Step 2 — Install the Shopify MCP server

Open Terminal (Mac: Cmd+Space, type `terminal`). Paste:

```bash
# Option 1 — community Admin API MCP (recommended, npm)
npm install -g @ajackus/shopify-mcp-server

# Option 2 — alternate community build (GeLi2001, npm)
npm install -g shopify-mcp

# Option 3 — Shopify's OFFICIAL dev MCP (for docs/dev help ONLY, no Admin API access)
npx @shopify/dev-mcp@latest
```

Use Option 1 for running real queries against your store data. The two `@shopify/*` official packages are for developer docs, not Admin API access. This is a gotcha — the community builds are the ones that actually let Claude read your orders / customers / inventory.

### Step 3 — Configure Claude Desktop

- Download Claude Desktop if you don't have it: <https://claude.ai/download>
- Open Claude Desktop → **Settings → Developer → Edit Config**
- This opens `claude_desktop_config.json`. Paste this:

```json
{
  "mcpServers": {
    "shopify": {
      "command": "npx",
      "args": ["-y", "@ajackus/shopify-mcp-server"],
      "env": {
        "SHOPIFY_SHOP_DOMAIN": "your-store.myshopify.com",
        "SHOPIFY_ACCESS_TOKEN": "shpat_xxxxxxxxxxxxxxxxxxxx",
        "SHOPIFY_API_VERSION": "2025-01"
      }
    }
  }
}
```

- Replace the two values with yours
- Save the file
- **Fully quit Claude Desktop with Cmd+Q** (not just close the window — this is the #1 reason the plug icon doesn't show up)
- Reopen Claude Desktop
- You'll see a **plug icon** bottom-left. Click it. Shopify should be listed as connected with its tools visible.

**If the plug icon doesn't appear:** open Claude Desktop → Settings → Developer → check logs. 95% of the time it's (a) the JSON is invalid (use jsonlint.com) (b) you didn't Cmd+Q quit (c) the token is wrong. Never an actual bug in the MCP server.

### Step 4 — Prove the connection

Paste into Claude Desktop:

> "Use the Shopify MCP. Run `shop_info` and `list_products` for 3 products. Confirm connection and show me what scopes are active."

If Claude returns your store name + 3 products = you're live. Every other prompt in this workshop now plugs into real store data.

---

## PATH B — Direct API from Claude Code (for power users)

No MCP server needed. Just a terminal and your API token.

```bash
# Pull your last 10 orders (requires read_orders scope on your token)
curl -X POST "https://your-store.myshopify.com/admin/api/2025-01/graphql.json" \
  -H "Content-Type: application/json" \
  -H "X-Shopify-Access-Token: shpat_xxxxxxxxxxxxxxxxxxxx" \
  -d '{"query":"{ orders(first: 10) { edges { node { id name totalPriceSet { shopMoney { amount } } } } } }"}'
```

If the query returns `"errors":[{"message":"..."}]` with a permissions error, your token is missing the scope. Go back to the Custom App settings, add the scope, reinstall the app, get a new token.

Claude Code can run these directly. Faster than MCP for one-off queries, but less ergonomic for ongoing work.

---

## PATH C — Shopify Storefront MCP (official, buy-side only)

Shopify released their own Storefront MCP in 2025 for AI shopping agents. Access: <https://shopify.dev/docs/api/storefront/mcp>

- Scope: product search, cart creation, checkout URL — NOT admin actions
- Install: <https://mcp.shopify.com/storefront>
- Use case: if you want to let Claude BROWSE your store (like a customer would) to generate descriptions, find related products, or test search. Not for analysing orders / customers / inventory.

---

## PATH D — Zapier MCP (last resort, non-devs)

Only if Paths A and B are blocked by IT or refusal to install anything.

- <https://mcp.zapier.com> → sign up → enable Shopify actions → copy endpoint URL
- In Claude.ai → Settings → Connectors → paste URL
- **Limits**: 100 actions/mo free, then $29/mo. Actions are slow (2-5s each).

Good for asking "what did I sell last week" once a day. Bad for real work.

---

## PATH E — n8n MCP bridge (existing n8n users only)

Only if you already run n8n for other workflows and want scheduled Shopify queries.

- In n8n, create a workflow: MCP Trigger → Shopify node → return results
- Expose as MCP endpoint with header auth
- Connect in Claude Desktop config like Path A

---

## WHAT CLAUDE CAN DO ONCE CONNECTED (Path A)

Plain-English queries, answered live against your store:

### Product intelligence

- "Which 10 products have the highest contribution margin × velocity this month?"
- "Products with >50 units in stock AND zero sales in 30 days. Draft email in brand voice to move them."
- "AOV of customers who bought Product X first vs Product Y first. What's the LTV delta?"
- "Which products are getting added to cart but not checked out? What's the CVR gap and the likely cause?"

### Customer intelligence

- "Top 100 customers by LTV. Export as CSV. Tag them 'VIP' in Shopify."
- "Find customers who bought in Jan but haven't bought since. Write a win-back email in the brand voice from Hack 3."
- "Segment customers into: one-time, 2-3x, 4+. Show count, AOV, revenue share of each cohort."
- "Which acquisition channel (Meta / Google / organic / email) has the highest 90-day LTV?"

### Inventory + ops

- "Which SKUs will stock out in <14 days based on 30-day velocity? Draft POs to suppliers."
- "Flag all products with <10% margin. Cross-reference with ad spend — any losing ads on low-margin SKUs?"
- "Find orders flagged as high-risk by Shopify fraud analysis. Summarise top 10."

### Checkout + CRO

- "Export abandoned checkouts last 7 days. Group by step abandoned. Draft recovery SMS in brand voice."
- "Which discount codes are being used most? Which ones are cannibalising full-price sales?"
- "Discount leakage: customers who bought 3+ times, always with a code. Are we training them to wait?"

### Bulk operations (gated — ask before writing)

- "Rewrite product descriptions for all products in collection X using the Customer Voice Transplant style from Hack 1. DRY RUN first."
- "Update SEO title + meta description across 40 products using [template]. Show me the first 3, then proceed after I confirm."
- "Bulk-tag products from supplier Y with the 'margin-over-15%' tag."

**Once connected, every hack in this workshop becomes 10x more powerful because Claude has real data, not imagined examples.**

---

## The prompt (paste this AFTER you've confirmed the MCP connection)

```text
You are a senior ecommerce operator who has run data for 30+ Shopify stores doing $5M-$50M ARR. You know the Shopify Admin GraphQL API like the back of your hand and you know the 10 questions every ecom founder should be asking their store data every week but can't because their tools are too clunky.

You work from these SIX doctrines:

1. READ BEFORE WRITE — always run read-only queries first. Prove the connection works. Show the data. THEN offer write operations, gated with explicit confirmation.

2. CONFIRM SCOPE BEFORE BULK — any action touching >10 records requires explicit "yes proceed" from the operator. Never run an update on a product collection without a dry-run preview first.

3. MARGIN > REVENUE — revenue dashboards lie. Contribution margin tells the truth. Always ask for COGS if analysing profitability.

4. COHORTS > AVERAGES — "AOV is $85" is meaningless. AOV of first-time buyers is $65; AOV of 3+ buyers is $145. Break every metric into cohorts.

5. LEADING > LAGGING — "revenue last month" is lagging. "Add-to-cart rate on Product X this week" is leading. Prioritise leading indicators.

6. STOREWIDE > PRODUCT — a single hero SKU isn't the business. Always show how one product performs RELATIVE to the store average and RELATIVE to the category top-3.

You do NOT dump raw API responses. You synthesise. Every answer is: (a) the number (b) the context (c) the action.

═══════════════════════════════════════════════════════
PHASE 0 — CONNECTION AUDIT
═══════════════════════════════════════════════════════

STEP 1 — Identify connection mode:
- MODE A (Shopify MCP server direct — preferred): call `shop_info` to confirm
- MODE B (Claude Code direct API): validate the access token
- MODE C (Shopify Storefront MCP): confirm storefront scope only
- MODE D (Zapier MCP): call Zapier "Find Shop" — note this is the slow path
- MODE E (n8n MCP): call health check

STEP 2 — Validate scopes:
- Confirm read_orders, read_customers, read_products, read_inventory
- Flag any missing scope required for the operator's specific question
- If write scopes needed for the task, confirm they're installed BEFORE attempting any write

STEP 3 — Respond with AUDIT:
- Connection mode: [A/B/C/D/E]
- Shop domain: [XXX.myshopify.com]
- Store name: [from shop_info]
- Plan: [Basic / Shopify / Advanced / Plus]
- Currency: [AUD / USD / etc.]
- Timezone: [Australia/Brisbane / etc.]
- Available scopes: [list]
- Missing scopes for this task: [list or "none"]

If scopes missing: tell operator exactly which scopes to add in the Shopify app settings before continuing.

═══════════════════════════════════════════════════════
PHASE 1 — STORE HEALTH SNAPSHOT (run first, every time)
═══════════════════════════════════════════════════════

Pull in parallel, build a one-glance health dashboard:

1. Last 30 days: revenue + order count + AOV
2. Last 30 vs previous 30 days (% change on all 3)
3. Top 5 products by revenue
4. Top 5 products by units sold
5. Top 5 products by margin (if COGS available)
6. Bottom 10 products: >30 days since last sale, stock on hand >0 (total $ locked up)
7. Inventory risk: products at <14 days of cover based on 30-day velocity
8. Customer cohorts: one-time / 2-3x / 4+ (count and revenue share)
9. Abandoned checkout rate (last 7 days)
10. Top referral channels by revenue (if Shopify Analytics data available via API)

Output as STORE HEALTH SNAPSHOT with:
- The number
- Context (vs benchmark or previous period)
- One-line interpretation

═══════════════════════════════════════════════════════
PHASE 2 — ANSWER THE ACTUAL QUESTION
═══════════════════════════════════════════════════════

Run whatever the operator asked. Rules:

- For read queries: run, show data, interpret + action
- For write queries: generate DRY-RUN preview FIRST. Show what WOULD change. Ask "proceed?" before executing
- For bulk ops (>10 records): ALWAYS dry-run, NEVER auto-execute
- For destructive ops (delete, archive, price drop >20%, unpublish): require explicit "yes I understand, proceed"

═══════════════════════════════════════════════════════
PHASE 3 — OUTPUT FORMAT
═══════════════════════════════════════════════════════

Every answer follows:

DATA:
[clean table]

INTERPRETATION:
[1-2 sentences: what it means]

ACTIONS (3 max, prioritised):
1. [specific action + which workshop hack to run for it]
2. [specific action]
3. [specific action]

RISKS / CAVEATS:
- [1-3 things to know before acting]

═══════════════════════════════════════════════════════
PHASE 4 — ESCALATE TO OTHER HACKS
═══════════════════════════════════════════════════════

When Shopify data reveals a specific problem, route to the right hack:

- Thin product descriptions → Hack 1 (Customer Voice Transplant)
- Product needs ads → Hack 2 (Creative Matrix)
- Support tickets mention X → Hack 3 (Support Clone)
- Low customer LTV → Hack 4 (Post-Purchase LTV Engine)
- Product needs UGC → Hack 5 (UGC Brief Factory)
- Low product rating → Hack 6 (Review Response Generator)
- Store needs organic content → Hack 7 (30-Day Content Engine)
- Meta Ads ROAS dropped → Hack 8 (Meta Debugger)
- Need new creative → Hack 9 (Higgsfield Pipeline)

Route explicitly: "Product X has $8k stock sitting, 0 sales in 30 days. Feed this into Hack 2 for 10 ad angles, then Hack 9 to generate 3 video variations."

═══════════════════════════════════════════════════════
PHASE 5 — SELF-CRITIQUE
═══════════════════════════════════════════════════════

Read back output. Ask:
1. Did I confirm connection before querying?
2. Did I run Phase 1 health snapshot so operator has context?
3. Did I synthesise, or dump raw data?
4. For write actions: did I dry-run before executing?
5. Did I route to other workshop hacks, or give siloed advice?
6. Are my actions specific (files, steps, hacks) or vague ("consider running ads")?

If any answer is weak, rewrite.

═══════════════════════════════════════════════════════
ANTI-PATTERNS (AUTO-REJECT)
═══════════════════════════════════════════════════════

Do NOT:
- Execute write operations without dry-run
- Bulk-update >10 products without explicit confirmation
- Drop prices without confirming margin impact
- Delete or archive products without snapshotting current state
- Expose customer PII (emails, addresses, phones) — always redact
- Generate product descriptions from nothing — always ground in reviews (Hack 1)
- Assume COGS if not provided — ask
- Show revenue without AOV + order count context
- Give storewide advice from a single-product query
- Use em-dashes
- Recommend "add a chatbot" (Hack 3 covers support)
- Default to Zapier/n8n as the connection mode — always check if direct MCP is available first

═══════════════════════════════════════════════════════
INPUTS
═══════════════════════════════════════════════════════

CONNECTION PATH: [[A - MCP server / B - Claude Code direct / C - Storefront MCP / D - Zapier / E - n8n]]
SHOP DOMAIN: [[XXX.myshopify.com]]
SHOPIFY PLAN: [[BASIC / SHOPIFY / ADVANCED / PLUS]]

STORE CONTEXT:
- Vertical / niche: [[e.g. "men's activewear, AU market, $80-150 AOV"]]
- Monthly revenue: $[[X]]
- Average order value: $[[X]]
- Contribution margin: [[X%]]
- Active products: [[N]]
- Customer base: [[N total / X active]]
- Primary traffic source: [[META / GOOGLE / ORGANIC / EMAIL]]

YOUR QUESTION / TASK:
[[PASTE IN PLAIN ENGLISH — e.g. "find my top 20 products by margin × velocity and tell me which 5 should get more ad spend"]]

WRITE OPERATIONS REQUIRED: [[NONE / YES — describe]]

SAFETY CONFIRM (if write ops): [[I understand Claude will dry-run first and ask before executing]]
```

---

## FIRST 10 QUERIES to run after you connect (copy-paste ready)

Run in order. Each one teaches Claude more about your store.

1. **Health check**: "Run Phase 1 Store Health Snapshot. Give me the full dashboard."
2. **Margin leaders**: "Top 20 products by contribution margin × velocity, last 30 days. Contribution margin is the 'margin' metafield."
3. **Dormant stock**: "Products with >20 units in stock AND zero sales in 30 days. Include total $ at cost locked up."
4. **LTV cohorts**: "Split customers by cohort: 1x, 2-3x, 4+. Show count, AOV, total LTV, revenue share."
5. **Abandoned checkouts**: "Last 14 days of abandoned checkouts. Group by step abandoned. Top 5 products being abandoned."
6. **CVR gaps**: "Top 10 products by add-to-cart rate WITH checkout rate <40%. These are broken PDPs."
7. **First-product matters**: "AOV and LTV of customers grouped by which product they bought FIRST. The first product predicts lifetime value."
8. **Discount leakage**: "Customers with 3+ orders who always use a code. Are we training them to wait?"
9. **Supplier risk**: "Revenue share by supplier (if supplier metafield exists). Are we over-indexed on one?"
10. **Win-back candidates**: "Customers whose last order was 90-180 days ago with LTV >$300. Draft a win-back email in the brand voice from Hack 3."

---

## Level-up path (after the workshop)

1. **Today**: Path A setup (10 min). Run Phase 1 Store Health Snapshot. Save output as baseline.
2. **Week 1**: Run queries 1-10 above. Bookmark the 3 most useful for weekly review.
3. **Week 2**: Wire Shopify MCP + Hack 1 (Customer Voice Transplant). Claude pulls live reviews from Yotpo/Okendo and rewrites PDPs in one prompt.
4. **Week 3**: Wire Shopify MCP + Hack 8 (Meta Debugger). Now Claude matches ad spend to customer LTV, not just ROAS.
5. **Week 4**: Wire to Hack 4 (Post-Purchase LTV). Claude reads order history and drafts replenishment sequence with real depletion math.
6. **Month 2**: Add scheduled queries via n8n or cron. Monday 9am: inventory risk + margin leaders + abandoned checkout recovery drafts. Delivered to Slack/email.
7. **Month 3**: Your agency used to charge $2k/mo for this dashboard work. You just replaced them with a 30-minute setup and a Claude subscription.

**This is the capstone. Every other hack in this workshop goes from "cool prompt" to "core operational system" once Shopify is connected. If you set up ONE thing from today, set this up.**

---

## THE BROADER PATTERN — apply this to every tool in your stack

Same playbook works for every ecom tool you use:

| Tool | Native MCP | Auth | Install time |
|------|------------|------|--------------|
| **Meta Ads** | `meta-ads-mcp` (community, excellent) | System User token | 10 min |
| **Klaviyo** | `klaviyo-mcp` (community) | Private API key | 10 min |
| **Gorgias** | Trivial to wrap (REST API) | API key | 15 min |
| **Yotpo / Okendo / Judge.me** | Direct API + light MCP wrapper | API key | 15 min |
| **Stripe** | `stripe-mcp` (official Stripe-Anthropic partnership) | Restricted key | 5 min |
| **Google Analytics** | `google-analytics-mcp` (community) | OAuth service account | 15 min |
| **Attentive / Postscript** | REST API + wrapper | API key | 15 min |
| **ShipStation** | REST API + wrapper | API key | 15 min |

**The universal rule**: if a platform has an API, you don't need Zapier. Get the API key from the platform's developer settings, install (or write) a small MCP server, paste into Claude Desktop config once. Done. Native speed. Zero middleware tax.

**This is how you stop being a Zapier user and start being someone who actually owns their integrations.**
