<p align="center">
  <img src="images/banners/cf0-banner-readme.png" alt="cf0 — the financial intelligence stack" width="100%" />
</p>

<p align="center">
  <a href="https://docs.cf0.ai">docs.cf0.ai</a>
  ·
  <a href="https://cf0.ai">cf0.ai</a>
  ·
  <a href="https://status.cf0.ai">status</a>
  ·
  <a href="https://x.com/cf0ai">@cf0ai</a>
</p>

---

This repository is the source for [docs.cf0.ai](https://docs.cf0.ai) — the public customer-facing documentation for cf0, the financial intelligence stack for analysts. Pages are MDX with YAML frontmatter; configuration lives in `docs.json`. The site is built and hosted by [Mintlify](https://mintlify.com).

## What's here

| Path | Purpose |
|---|---|
| `docs.json` | Mintlify config — navigation, theme, SEO, footer, banner, feedback |
| `index.mdx` | Landing tile grid (custom layout, `mode: frame`) |
| `introduction.mdx` | Product overview, the three layers, filings coverage |
| `quickstart.mdx`, `account-setup.mdx` | Onboarding |
| `features/` | Lab, Reports, SEC + global filings, Documents, Skills, Knowledge |
| `workspace/` | Organisations, Settings, Dashboard |
| `data/` | Overview, SEC + global filings, Integrations |
| `security/` | Data governance, observability, guardrails, citations, audit |
| `examples/` | Head-to-head, DCF walkthrough, IC memo, published research |
| `changelog.mdx` | Dated releases |
| `images/` | Screenshots + brand previews |
| `style.css` | Custom CSS overrides |

## Local development

```bash
nvm use            # picks up .nvmrc
npm i -g mint      # one-time
mint dev           # http://localhost:3000
mint broken-links  # check internal links
```

`mint` is the Mintlify CLI. See [Mintlify CLI commands](https://www.mintlify.com/docs/cli/commands.md).

## Editing rules

- **Sentence case** for headings. Sentence case everywhere in product UI — never Title Case in buttons or labels.
- **Mintlify page titles are 1–3 words** — they double as sidebar items and wrap on mobile if long. Use noun-form for concept pages; verb-led only for examples/walkthroughs.
- **Every page must make sense to a financial analyst.** Customers are analysts, not developers. No API reference, no SDK docs, no programmatic-integration content — there's no user-level API key surface today and analysts use the app, not endpoints. If a page would only make sense to an engineer, it doesn't belong here.
- **Production-only content** — no beta features, no staging-only surfaces, no feature-flagged-off surfaces. Brain / Coverage / Billing are hidden in production (`HIDE_*=1`), so don't add new references to them.
- **Marketable framing > specific counts** — use "DCF, LBO, comps, IC memos" not "22 workflows."
- **Verify every quantitative or temporal claim** against the real system before publishing. Numbers carry through, and customers fact-check.

## Voice and tone (from the cf0 brand book)

The brand book canonises the voice every cf0 surface follows — including these docs.

- **Posture**: editorial publishing × institutional finance × computed precision. Modest, not bold. Credibility through substance — citations, traceability, sourced numbers — not through marketing polish.
- **Reference brands**: Barron's, The Economist, Financial Times, IBM Carbon, Stripe, Vercel.
- **Anti-references**: Notion, Linear, ChatGPT consumer UI, Material Design, generic SaaS dashboards, fintech startup color explosions.
- **Sentence shape**: short, periodic. The long sentence earns its length when a precise qualification is required and the rhythm of the paragraph supports it.
- **In voice**: *"Apple's Q4 cash conversion improved 240 basis points year over year, driven by a 3-day reduction in days inventory outstanding."*
- **Out of voice**: rocket emoji, `CRUSHED`, `INSANE`, exclamation marks, marketing superlatives.
- **Active voice, second person.** One idea per sentence. Bold for UI elements (`Click **Settings**`), inline code for file names and commands.

## AI-first surfaces

Every page is exposed as Markdown for LLMs:

- `/llms.txt` — the page index, optimised for an LLM's first read.
- `/llms-full.txt` — the entire site concatenated.
- `/<page>.md` — single-page Markdown export for ChatGPT / Claude / Cursor / Perplexity.
- The **contextual menu** in the docs UI offers one-click "copy to Claude / ChatGPT / Cursor" on every page (configured in `docs.json` → `contextual.options`).

Mintlify maintains an authoritative index of its own platform features and components for LLMs at [https://www.mintlify.com/docs/llms.txt](https://www.mintlify.com/docs/llms.txt). Read it before adding new components or wiring new `docs.json` knobs — it reflects the current free-plan surface area.

## Mintlify features wired in this repo

`docs.json`:

- `theme: "luma"` with custom primary / light / dark colour tokens.
- Custom logo (light + dark) and favicon.
- `fonts` — Source Serif 4 (headings) and Inter Tight (body), self-hosted from Google Fonts via `format: "woff2"`.
- `styling.eyebrows: "breadcrumbs"`.
- `appearance.default: "system"` (light / dark follows OS).
- `contextual.options` — copy, view, claude, chatgpt, cursor, mcp, add-mcp.
- `metadata.timestamp: true` for last-updated stamps.
- `seo.indexing: "all"` with full Open Graph and Twitter meta tags.
- `search.prompt` — branded search placeholder.
- `navigation` — guides / examples / API reference / changelog tabs, plus a Status anchor in the global navigation.
- `redirects` for moved pages.
- `errors.404` — custom 404 with quick links to the most-visited pages.
- `footer.socials` + `footer.links` (Product, Resources, Trust, Company).
- `banner` — dismissible top banner for headline announcements.
- `feedback.thumbsRating`, `feedback.suggestEdit`, `feedback.raiseIssue` — per-page feedback widgets.

Components used in `.mdx`:

- `Card` / `CardGroup` — surface gallery and feature overviews.
- `Frame` — branded screenshots with captions.
- `Steps` / `Step` — sequential procedures.
- `Tabs` / `Tab` — switchable content panels.
- `Accordion` / `AccordionGroup` — FAQs and expandable content.
- `Note` / `Tip` — callouts.
- `Tooltip` — inline jargon definitions (DCF, WACC, IC, MD&A, etc.).
- `Tree` / `Tree.Folder` / `Tree.File` — filesystem visualisation.
- `Expandable` — long JSON / trace payloads.
- `Update` — dated changelog entries.
- ` ```mermaid ` — themed flowcharts and sequence diagrams (cf0 brand colours).
- `Icon` — Lucide icons inline with brand-colour styling.

## Brand assets

The cf0 brand book — colours, typography, system rules, surface previews, chart canon — lives at [`cf0.ai/docs/design/`](https://github.com/CF0ai/cf0/tree/main/docs/design). Rendered previews are in `docs/design/previews/*.html`. PNG snapshots ship into this repo under `images/brand/` for use in docs.

## Conventions

- **Don't add `README.md` content into a docs page.** This file is for repo contributors; Mintlify auto-ignores it via `.mintignore`.
- **Don't commit drafts.** `drafts/` and `*.draft.mdx` are ignored.
- **Status page is canonical.** Don't surface incident details in docs — link to [status.cf0.ai](https://status.cf0.ai).

## Contact

- Customer questions — [filippo@cf0.ai](mailto:filippo@cf0.ai)
- Bugs in this repo — file an issue on the repo

---

<p align="center">
  <sub>cf0 — the financial intelligence stack. Built for analysts who put their name on the output.</sub>
</p>
