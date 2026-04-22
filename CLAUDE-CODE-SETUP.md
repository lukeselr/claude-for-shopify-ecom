# Claude Code + Shopify — Build & Edit Your Store With Plain English

**What this unlocks:** edit your Shopify site the way a developer would — but you just talk to Claude in plain English. No drag-and-drop builders. No slow admin UI. No "is this even saved yet?"

**This is the second path.** [HACK 10](prompts/10-shopify-connection.md) (Claude Desktop + MCP) is for *reading* your store data. **This doc is for *building and editing* your site itself** — homepage, product pages, checkout, theme — via Claude Code, a terminal-based AI coding tool.

Shopify released an **official AI Toolkit for Claude Code on April 9, 2026**. It gives Claude direct, schema-aware access to your store's theme, APIs, and documentation. Setup is one command.

---

## What you can do with this setup

- "Add a reviews carousel above the add-to-cart button on every product page"
- "Make the homepage hero full-bleed and change the CTA to 'Shop the drop'"
- "Add a free shipping bar at the top of the site, hide it on the checkout page"
- "Rewrite the footer so the payment icons are centred and add the TikTok link"
- "Preview the site on my laptop before I push anything live"

Claude edits the theme files directly. You see the changes live in a browser preview before anything hits your real store.

---

## Prerequisites

- A Shopify store, any plan. You need **staff / owner access** or an API token.
- A Mac or Windows laptop with a terminal. (Mac: Cmd+Space → type "terminal". Windows: Start → type "PowerShell".)
- About 20 minutes the first time. After that, zero — Claude Code just opens.

---

## One-time install (run these commands once, ever)

Copy-paste each block into your terminal and press enter. If a command asks for your password, type your Mac/Windows password (it won't show characters — that's normal).

### 1. Install Node.js (if you don't have it)

Check if you already have it:
```bash
node --version
```
If you see `v18.x` or higher, skip to Step 2. Otherwise download the **LTS** version from [nodejs.org](https://nodejs.org) and install it, then re-run the check.

### 2. Install Claude Code

```bash
npm install -g @anthropic-ai/claude-code
```

First time you run it, it will ask you to log in with your Anthropic account. Done.

### 3. Install the Shopify CLI

```bash
npm install -g @shopify/cli
```

Verify:
```bash
shopify version
```

### 4. Install Shopify's official AI Toolkit (the magic bit)

Open Claude Code:
```bash
claude
```

Inside Claude Code, paste these two commands one after the other:
```
/plugin marketplace add Shopify/shopify-ai-toolkit
```
```
/plugin install shopify-plugin@shopify-ai-toolkit
```

That's it. Claude now understands Shopify's entire API, theme structure, and documentation natively.

### 5. Connect Claude Code to your store

Still inside Claude Code, in your terminal:
```bash
shopify auth login
```
A browser opens. Log in to your Shopify account.

Then authenticate against your specific store (replace `your-store-name` with your real store subdomain — the bit before `.myshopify.com`):
```bash
shopify store auth --store your-store-name.myshopify.com --scopes read_themes,write_themes,read_products,write_products,read_orders,read_customers
```

Approve in the browser. You're in.

---

## Your first theme edit — end to end in 5 minutes

### Pull your live theme down to your laptop

```bash
mkdir ~/my-shopify-site
cd ~/my-shopify-site
shopify theme pull --store your-store-name.myshopify.com
```

This downloads every file that makes up your site into a folder on your laptop. Pick the **live** theme when it asks.

### Start a live preview

```bash
shopify theme dev --store your-store-name.myshopify.com
```

It opens a URL like `http://127.0.0.1:9292` — your **real site, running on your laptop**. Any edit you make refreshes instantly. Nothing is live to your customers yet.

### Tell Claude Code what to change

In a separate terminal window (or tab), from the same folder:
```bash
claude
```

Now just talk to it. Examples that work out of the box:

> "Change the announcement bar background to black and make the text say FREE SHIPPING OVER $100."

> "Add a sticky Add To Cart button on mobile that shows on the product page after the user scrolls past the main image."

> "Show me what the homepage looks like now and recommend three conversion improvements."

Claude reads the theme files, makes the edit, and your preview browser updates live. If you don't like it, say "undo that". If you love it, say "that's good, let's push it live".

### Push your changes to the real store

When you're happy:
```bash
shopify theme push --store your-store-name.myshopify.com
```

Choose whether to push to the live theme or a new unpublished copy. Go with **unpublished** the first few times so you can preview the full result in Shopify admin before going live.

---

## The skills folder — drop these into your setup

This repo includes ready-made Claude Code skills (instructions that teach Claude how to work with specific tools). They live in the `skills/` folder of this repo.

**To install them:**

```bash
mkdir -p ~/.claude/skills
cp -r skills/* ~/.claude/skills/
```

That copies them into Claude Code's skill folder. Restart Claude Code and they'll be auto-detected. No more pasting long prompts — just say "use the shopify-theme-workflow skill" and Claude knows exactly what to do.

---

## "What if I get stuck?"

Claude Code debugs itself. Paste any error message straight into Claude and it walks you through the fix.

Example:
> "I just ran `shopify theme pull` and got this error: [paste error]. What do I do?"

Claude reads the error, tells you the root cause, and gives you the exact command to fix it. This is the self-service support — you don't need a helpdesk.

For genuinely new Shopify questions, the toolkit searches Shopify's live developer docs for you. Just ask.

---

## What to do AFTER this is working

1. **Run [START_HERE.md](START_HERE.md)** — Claude will orient around your store and recommend the 3 highest-impact hacks from this repo based on your actual pains.
2. **Set up [HACK 10](prompts/10-shopify-connection.md)** — adds data ops (products, orders, customers) to Claude Desktop. Pairs with this setup. Different use case, same philosophy.
3. **Build your first real change** — pick one thing on your site that's been bugging you for months, and fix it tonight.

---

## The big picture

You are now one of a very small number of Shopify operators who can edit their site by talking to an AI, with a live preview, version history, and zero middleware. The same pattern works for every platform with an API — Meta Ads, Klaviyo, Gorgias, Stripe. See [HANDOUT.md](HANDOUT.md) for the full stack.

**Your site, your laptop, your control.** No subscription. No vendor lock-in. The toolkit is free and open-source — Shopify maintains it.

---

Built in Australia by [Selr AI](https://selrai.com.au).
