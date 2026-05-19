---
name: cf0-docs
description: Style and content rules for any agent editing docs.cf0.ai
---

# AGENTS.md — docs.cf0.ai editing rules

This file is read by Mintlify's Agent (and by any other AI editor pointed at this repo) before writing or modifying pages.

## Voice and tone

- **Sentence case everywhere.** Page titles, H2s, H3s, table headers, button labels. Never Title Case. "Lab" not "Lab Feature". "Get started" not "Get Started".
- **Analyst-first.** Lead with what an analyst at a family office or hedge fund cares about — speed, citations, defensibility, trust. Avoid generic "AI-powered" language.
- **Editorial-finance register.** Borrow from Barron's and The Economist, not SaaS marketing sites. Specific, restrained, declarative.
- **No marketing puffery.** Never publish a quantitative or temporal claim that isn't grounded in the actual system. "30 years of structured financials" was deck copy, not reality.
- **Marketable framing over inventory counts.** Use categorical lists ("DCF, LBO, comps, IC memos") not specific numbers ("22 workflows"). The brand book itself never exposes counts.

## Page titles and frontmatter

- **`title:` is 1–3 words, noun-form.** Mintlify renders it as both the H1 and the sidebar item. Examples: `Lab`, `Reports`, `Overview`, `Account setup`, `Authentication`. Never full sentences. Never em-dash subtitles. Never "with cf0" tails.
- **`description:` is one declarative sentence, 130–160 chars.** Powers SEO meta-description, search snippet, sidebar hover, and llms.txt. Distinct from the title. Sentence case. Never the same as title.
- **Verb-led titles only for `examples/`** — walkthrough pages can use gerund or imperative form ("Building a watchlist", "Run a head-to-head"). Concept pages stay noun-form.

## Components

- **`<Frame>` every screenshot.** Always with a `caption=` that names what the surface is and what's notable about it.
- **`<Steps>` for sequential setup or walkthrough flows.** Each step has a `title=` (sentence case verb phrase) and one paragraph of body.
- **`<CardGroup>` for parallel options.** Never nest cards. Don't overload a card with more than one short paragraph + at most one list.
- **`<Note>`, `<Tip>`, `<Warning>`, `<Info>` callouts** — match the semantic. Use `Note` for caveats, `Tip` for analyst time-savers, `Warning` for irreversible actions, `Info` for context that's true but not the page's main point.
- **`<CodeGroup>` for multi-language API examples.** Always include `bash curl` + `javascript fetch` + `python requests` at minimum.
- **`<Update>` for changelog entries.** Always include `label="<date>"` and `description="<short tag line>"`. Use `tags=` array to categorise.

## Brand

- **Wordmark is `cf0`, lowercase, always.** Never `CF0`, never `Cf0`. JetBrains Mono in product UI; in body text it's regular type.
- **One blue voltage: `#1d4ed8`** (Blue 700). Used scarcely. Primary CTAs, focus rings, links. Never as a decorative accent.
- **Three-layer story: Data → Brain → Lab.** Not "Inputs → Brain → Lab" (the brand book deck used "Inputs" but customer docs use "Data").
- **Light-mode first, sharp corners, hairline borders.** No drop shadows in flow chrome.

## Numbers and claims

For every quantitative or temporal claim in customer-facing copy, ground it in a real system **before publishing**:

| Claim type | Where to verify |
|---|---|
| Skills count | `find backend/sandbox/skills -name SKILL.md | wc -l` |
| SEC market count | `_COUNTRY_TO_SOURCE` in `backend/routers/global_filings.py` |
| Filings covered | Filings DB / S3 inventory |
| File types | `ALLOWED_TYPES` in `backend/routers/documents.py` |
| Settings tab list | `apps/web/src/pages/SettingsPage.tsx` |

When in doubt, drop the number and use categorical framing.

## File and page naming

- **File names**: short, kebab-case, slug-style. `streaming.mdx` not `streaming-and-rendering-explained.mdx`. `head-to-head.mdx` not `head-to-head-comparison.mdx`.
- **URL slugs match file names.** Don't override via frontmatter unless renaming for SEO with a corresponding `redirects[]` entry in docs.json.

## Don'ts

- Don't add backwards-compatibility hacks (kept-around old titles, dual filenames).
- Don't write multi-paragraph docstrings or planning comments inside MDX.
- Don't add screenshots without first checking they actually load at the right resolution.
- Don't QA Mintlify pages by desktop screenshot alone — always check mobile sidebar wrap at ≤640px.
- Don't rename pages without adding a permanent redirect.
- Don't put brand-name tails in page titles ("X with cf0"). The brand is implicit.
