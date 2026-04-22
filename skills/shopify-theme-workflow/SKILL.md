---
name: shopify-theme-workflow
description: Use this skill when the user wants Claude Code to edit, preview, or push their Shopify theme. Handles the full pull → edit → preview → push loop using the Shopify CLI. Complements Shopify's official AI Toolkit plugin.
metadata:
  category: Ecommerce
  tags:
    - shopify
    - theme
    - liquid
    - claude-code
    - frontend
  pairs-with:
    - skill: shopify-connector
      reason: Use shopify-connector for store data operations (products, orders, customers). Use this skill for editing the theme files themselves.
---

# Shopify Theme Workflow (for Claude Code)

## When to use this skill

The user wants to build or edit their Shopify storefront — homepage, product pages, collection pages, cart, announcement bars, footers, CSS, custom sections. Anything visual on the site.

**NOT for:** pulling reports, editing products/inventory/customers, running ad data analysis. Use `shopify-connector` or Claude Desktop + Shopify MCP for those.

## Assumed setup

Before running this workflow the user should already have:

1. Node.js 18+ installed
2. Claude Code installed (`npm install -g @anthropic-ai/claude-code`)
3. Shopify CLI installed (`npm install -g @shopify/cli`)
4. Shopify AI Toolkit plugin added inside Claude Code (`/plugin marketplace add Shopify/shopify-ai-toolkit` + `/plugin install shopify-plugin@shopify-ai-toolkit`)
5. Authenticated against their store (`shopify auth login` + `shopify store auth --store <store>.myshopify.com --scopes read_themes,write_themes`)

If any of those are missing, walk the user through `CLAUDE-CODE-SETUP.md` first. Do not try to edit a theme without the toolkit plugin — Claude will make uninformed edits against stale API assumptions.

## Core workflow — every session

### 1. Orient in the theme folder

```bash
cd ~/my-shopify-site   # or wherever the theme lives
ls
```

The theme should contain folders like `layout/`, `sections/`, `snippets/`, `templates/`, `assets/`, `config/`. If not, run `shopify theme pull --store <store>.myshopify.com` first.

### 2. Start a live preview (always)

```bash
shopify theme dev --store <store>.myshopify.com
```

This gives a local URL (usually `http://127.0.0.1:9292`). Every edit hot-reloads. **Never edit a theme without the preview running** — you lose the tight feedback loop that makes this workflow fast.

### 3. Understand before editing

When the user describes a change, read the relevant theme files first:

- Homepage content → `templates/index.json` and the sections it references
- Product page → `sections/main-product.liquid`, `templates/product.json`
- Announcement bar → search `sections/` for `announcement`
- Header/footer → `sections/header.liquid`, `sections/footer.liquid`
- Styles → `assets/*.css`, `assets/*.scss.liquid`
- Colours + fonts → `config/settings_data.json` and `config/settings_schema.json`

Use Grep and Read. Do not guess file paths.

### 4. Edit using the Shopify AI Toolkit

The Toolkit gives you live access to:
- Shopify's GraphQL Admin and Storefront schemas
- Liquid template linting
- Current Shopify developer docs
- Polaris UI components (for admin extensions)

Call on those tools when:
- You're about to write a Liquid tag → lint it with the Toolkit first
- You're about to fetch data → validate the GraphQL query against the live schema
- You're unsure of a syntax → search the docs, don't guess

### 5. Test in the preview

After every edit, tell the user which preview URL to check and what to look for:

> "Refresh http://127.0.0.1:9292 — the announcement bar should now be black with white text saying 'FREE SHIPPING OVER $100'. Check on mobile view too (browser DevTools → mobile toggle)."

### 6. Push to the store

**Default to an unpublished copy first:**

```bash
shopify theme push --store <store>.myshopify.com --unpublished --json
```

This creates a new theme in Shopify admin that the merchant can preview and publish manually. Safer than pushing straight to live.

**To push to the live theme (only after confirmation):**

```bash
shopify theme push --store <store>.myshopify.com --live
```

Ask the user: "Push to live now? This will overwrite the theme your customers currently see." Wait for an explicit yes.

## Safety rules

1. **Never push to live without explicit user confirmation.** The `--live` flag overwrites the customer-facing theme.
2. **Never run `shopify theme pull` on top of uncommitted edits.** It can overwrite local changes. Git-init the theme folder at the start of every project and commit after every push.
3. **Check `config/settings_data.json` changes carefully.** This file holds ALL theme settings — colours, fonts, section order. A bad edit can blank the site visually.
4. **Liquid is not HTML.** Tags like `{% if %}`, `{{ product.title }}`, `{%- assign -%}` are Liquid. Validate with the Toolkit before asserting they're correct.
5. **Mobile-first.** Always verify edits on mobile viewport before pushing — Shopify traffic is 60%+ mobile.

## Common tasks

### Add a new section to the homepage

1. Create `sections/<new-section-name>.liquid` with a `schema` block at the bottom
2. The merchant can now add it via Shopify admin → Customise theme → Add section
3. Preview locally first

### Change global colours

Edit `config/settings_data.json` → `current` → colour group. OR update the colour variables in the main CSS file. The Toolkit can tell you which pattern your specific theme uses.

### Fix a bug the merchant reports

1. Ask for a screenshot and the exact page URL
2. Read the relevant template file and its referenced sections
3. Reproduce in the local preview first, then fix

### Add a third-party embed (YouTube, TikTok, reviews widget)

Put embed code in a new snippet: `snippets/embed-<name>.liquid`. Then include it with `{% render 'embed-<name>' %}` in the relevant template. Never inline third-party JS directly in a section — it breaks under Shopify's async loader.

## Anti-patterns

- **Do not edit themes via the Shopify admin code editor while also editing locally.** They desync. Pick one channel.
- **Do not push on every save.** Preview locally → push once per logical change.
- **Do not hardcode prices, product titles, or IDs** in the theme. Pull them from Liquid objects (`{{ product.price }}`, `{{ product.title }}`).
- **Do not turn the whole site into an app.** Shopify themes are Liquid-first. Use apps/Hydrogen only when the theme can't do what's needed.

## If the user gets stuck

- Paste the error output back into Claude Code. The Toolkit knows 95% of Shopify errors by name.
- Common fixes: re-run `shopify auth login`, re-run `shopify store auth` with missing scopes, restart the `shopify theme dev` preview.
- If a push fails with an API error, the Toolkit can validate the theme against Shopify's schema and tell you which file has the issue.

---

This skill pairs with the full setup walkthrough in [CLAUDE-CODE-SETUP.md](../../CLAUDE-CODE-SETUP.md) at the repo root.
