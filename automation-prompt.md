# SEO Opportunity Finder — Automation Prompt

## Objective

Discover content worth creating for `{{NICHE_OR_WEBSITE}}` and produce a ready-to-execute editorial calendar, by running the three project-local skills in sequence: `seo-research` -> `keyword-clustering` -> `content-planner`.

## Inputs

- `niche_or_website` (required): `{{NICHE_OR_WEBSITE}}` — a topic/niche (e.g. "AI automation for solopreneurs") or a domain you own/are analyzing (e.g. "coding180.com").
- `pieces` (optional, default 5): `{{PIECES}}`
- `cadence` (optional, default weekly): `{{CADENCE}}`

## Steps

1. Run the `seo-research` skill (`Skills/seo-research/SKILL.md`) for `niche_or_website`. It researches trending questions and heuristically scores keyword competition using only `web_search`, `web_research`, `x_search`, and (if connected/verified) Google Search Console — never a paid SEO API. Output: `Content/SEO-Opportunities/<slug>/<date>/raw-research.md`.
2. Run the `keyword-clustering` skill (`Skills/keyword-clustering/SKILL.md`) on that `raw-research.md`, targeting `pieces` clusters. Output: `clusters.md` in the same folder.
3. Run the `content-planner` skill (`Skills/content-planner/SKILL.md`) on that `clusters.md`, paced at `cadence`. Output: `editorial-calendar.md`, `blog-outlines.md`, `titles.md`, and `internal-linking.md` (only if a website with existing content was analyzed) in the same folder.
4. Do not fabricate keyword volume, difficulty, or Search Console numbers at any stage — only report data that was actually retrieved from a real, already-connected source.

## Outputs

Saved under `Content/SEO-Opportunities/<niche-or-site-slug>/<YYYY-MM-DD>/`:

- `raw-research.md`
- `clusters.md`
- `editorial-calendar.md`
- `blog-outlines.md`
- `titles.md`
- `internal-linking.md` (only when a website with existing content was analyzed)

Plus a short chat/report summary: total opportunities found, top 3 priority picks (lowest competition + highest relevance), and the output folder path.

## Error handling

- If `niche_or_website` is missing or empty, stop and report that rather than guessing a topic.
- If Google Search Console isn't connected/verified for the given website, skip GSC-based steps in `seo-research` — don't fail the whole run over it.
- If research turns up fewer usable topics than `pieces`, report what was actually found rather than inventing filler topics.
- If any stage's required input file is missing (e.g. `keyword-clustering` can't find `raw-research.md`), stop and report which stage failed rather than guessing its contents.
