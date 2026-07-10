---
name: seo-research
description: Research trending questions and score keyword competition for a niche or website, using only free built-in search tools and already-connected catalog integrations (no paid SEO API). This is stage 1 of the SEO Opportunity Finder pipeline. Use when the user wants raw content-opportunity research — trending questions, People Also Ask style queries, forum/Reddit signals, and low-competition keyword candidates — for a niche or a specific website. Hands its output to the keyword-clustering skill.
metadata:
  author: robort.zo.computer
---

# SEO Research

Produces the raw research a content calendar is built from: trending questions and heuristically-scored low-competition keyword candidates for a niche or website. Free-only — never requires a paid keyword-data API or third-party sign-up.

## Inputs

- `niche_or_website` (required): a topic/niche (e.g. "AI automation for solopreneurs") OR a domain the user owns/is analyzing (e.g. `coding180.com`).

## Workflow

### Step 1 — Establish scope

Determine whether the input is a niche (topic only) or a specific website:

- **Niche only** → focus on external research: trending questions + keyword gaps in the space.
- **Website provided** → also check whether `google_search_console` is connected (check current capabilities before assuming). If connected and the site is verified there, pull top queries to find underperforming pages worth targeting.

### Step 2 — Research trending questions

Run 3-4 differently-worded queries per niche across `web_search` (use `topic="news"` when recency matters), `web_research`, and `x_search` for live discourse. Look specifically for:

- "People Also Ask"-style questions
- Reddit/Quora/forum threads signaling real user questions
- Recent news/announcements creating new search demand

Record the raw list of questions/keyword phrases with source URLs.

### Step 3 — Score competition (heuristic only, never a paid API)

Zo has no built-in keyword-volume/difficulty database, and this skill must never call one — no Ahrefs, SEMrush, or any paid third-party SEO API, since those require the user to sign up and pay. Score each candidate Low/Medium/High using SERP-quality signals visible in the search results themselves, with a one-line reason:

- **Low competition signals**: forums/UGC/Reddit ranking on page 1, few dedicated authoritative articles, long-tail phrasing (4+ words), question-based queries, no dominant brand.
- **High competition signals**: top 10 results are exclusively major publishers/brands, single-word or "best X" head terms.

Always label scores as heuristic estimates. Never state an exact search-volume or difficulty number that was not actually retrieved from a real, already-connected data source.

If a website was provided and Google Search Console is connected and verified for it, pull top queries and flag ones with high impressions + low position/CTR — these are validated existing demand that's cheap to move up. Skip this entirely (don't fabricate GSC data) if it isn't connected/verified.

### Step 4 — Save raw research output

Slugify `niche_or_website` and write `Content/SEO-Opportunities/<slug>/<YYYY-MM-DD>/raw-research.md`:

```markdown
# Raw Research — <Niche or Website>

Generated: <YYYY-MM-DD>
Source: niche | website

## Candidate Keywords / Questions

| Keyword / Question | Source | Competition | Reason |
|---|---|---|---|
| <phrase> | <url> | Low | <one-line reason> |

## Search Console Signals (only if GSC connected and verified)

| Query | Impressions | Position | CTR | Note |
|---|---|---|---|---|
```

No extra spaces inside table separator rows — downstream skills parse these tables.

### Step 5 — Handoff

Report the output file path and a 2-3 sentence summary (how many candidates found, rough Low/Medium/High split). Tell the user (or the orchestrating automation) to run the `keyword-clustering` skill next, pointing it at this `raw-research.md` file.
