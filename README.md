# Claude for Shopify Ecom — 10 Elite Hacks

**From the Paul Waddy community workshop, 20 April 2026.**
Ten battle-tested prompts + one capstone setup that connects Claude directly to your Shopify store — no Zapier, no n8n, no middleware.

Built by [Luke Heka](https://selrai.com.au), Selr AI — we build AI agents for Australian businesses.

---

## How to use this repo

1. Open any prompt file in the `prompts/` folder
2. Copy the fenced ` ```text ` block into Claude (Claude.ai for prompts 1-7, Claude Desktop for 8 + 10)
3. Fill in the `[[INPUTS]]` at the bottom
4. Run it

That's it. Every prompt is self-contained.

---

## ★ Start here: Hack 10 — connect Claude to your Shopify store

**This is the capstone.** Once Claude can see your real store data, every other hack in this workshop becomes 10x more powerful.

- [10 — Shopify Connection (direct MCP)](prompts/10-shopify-connection.md) ★

10 minutes, one-time setup. Free forever. The real answer.

---

## The 10 hacks

| # | Hack | What it does | Paste into |
|---|------|--------------|------------|
| 01 | [Customer Voice Transplant](prompts/01-customer-voice-transplant.md) | Rewrites product pages in your customers' own words | Claude.ai |
| 02 | [Creative Matrix](prompts/02-creative-matrix.md) | 10 fundamentally different ad angles from one product | Claude.ai |
| 03 | [Support Clone](prompts/03-support-clone.md) | Trains Claude to reply in your brand voice from 500+ real tickets | Claude.ai + Projects |
| 04 | [Post-Purchase LTV Engine](prompts/04-post-purchase-ltv.md) | 8-12 behaviourally-triggered emails/SMS from order to replenishment | Claude.ai |
| 05 | [UGC Brief Factory](prompts/05-ugc-brief-factory.md) | Creator-ready briefs grounded in your real customer reviews | Claude.ai |
| 06 | [Review Response Generator](prompts/06-review-response-generator.md) | Public replies that convert the next browser reading them | Claude.ai |
| 07 | [30-Day Organic Content Engine](prompts/07-organic-content-engine.md) | 30 platform-native posts in founder voice, 2hr/week | Claude.ai |
| 08 | [Meta Ads MCP Debugger](prompts/08-meta-ads-debugger.md) | Claude reads your live Meta Ads account, pinpoints spend leaks | Claude Desktop + MCP |
| 09 | [Higgsfield Creative Pipeline](prompts/09-higgsfield-creative-pipeline.md) | One product → 4 testable video ads, brand-consistent via Soul ID | Claude.ai + Higgsfield |
| 10 | [★ Shopify Direct Connection](prompts/10-shopify-connection.md) | The capstone. Claude reads your live Shopify admin data. | Claude Desktop + MCP |

Full handout (intro + "if you only do one thing" hierarchy + level-up stack): [HANDOUT.md](HANDOUT.md)

---

## The big idea

Most people think AI is chatbots and prompts. Elite operators wire Claude straight into their Shopify, Meta, Klaviyo, Gorgias, and Stripe via the Model Context Protocol (MCP).

**The universal rule**: if a platform has an API, you don't need Zapier. API key → MCP server → Claude. Same playbook works for every tool in your stack.

That's what Hack 10 teaches. Everything else plugs into it.

---

## Requirements

- A Shopify store (any plan)
- Claude.ai account — free tier works for most hacks, Pro recommended ($20/mo)
- For Hacks 8 + 10: Claude Desktop (free — [download](https://claude.ai/download))
- For Hack 9: Higgsfield Ultra ($49/mo) for Soul ID training
- A terminal (macOS: Cmd+Space → "terminal")

---

## The stack this assumes

```text
Your tools (Shopify, Meta, Klaviyo, Gorgias…)
        ↓  API key
MCP server (one per tool)
        ↓
Claude Desktop / Claude Code
        ↓
You, asking questions in plain English
```

No Zapier. No n8n. No middleware tax. Same playbook for every tool you use.

---

## Support

These prompts are shared as-is for workshop attendees. I don't run ongoing helpdesk or weekly Q&A on them — they work out of the box if you follow the inputs.

If you want to go beyond prompts and build **actual AI agents that run this stuff 24/7**, I run 2-day in-person workshops in Sydney. Details: [selrai.com.au/workshops](https://selrai.com.au/workshops)

Or DM me on LinkedIn / Instagram — I reply personally.

---

## License

MIT. Use commercially, modify, share. Attribution appreciated but not required.

---

**Built in Australia 🇦🇺 by [Selr AI](https://selrai.com.au).**
