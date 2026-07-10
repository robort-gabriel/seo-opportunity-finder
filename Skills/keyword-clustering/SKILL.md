---
name: keyword-clustering
description: Cluster a raw list of researched keywords/questions into topic groups by shared search intent. This is stage 2 of the SEO Opportunity Finder pipeline. Use when the user has raw keyword/question research (e.g. a raw-research.md file produced by the seo-research skill) and needs it grouped into content clusters with a primary keyword, supporting long-tail variants, intent, and competition per cluster. Hands its output to the content-planner skill.
metadata:
  author: robort.zo.computer
---

# Keyword Clustering

Groups raw keyword/question research into a fixed number of coherent topic clusters, each ready to become one piece of content.

## Inputs

- `raw_research_file` (required): path to a `raw-research.md` file produced by the `seo-research` skill (e.g. `Content/SEO-Opportunities/<slug>/<date>/raw-research.md`).
- `pieces` (optional, default 5): number of clusters to produce.

## Workflow

### Step 1 — Read the raw research

Read the `Candidate Keywords / Questions` table (and `Search Console Signals` table, if present) from `raw_research_file`.

### Step 2 — Group by shared intent

Group the raw list into `pieces` topic clusters by shared search intent — not just superficial keyword overlap. For each cluster capture:

- **Primary keyword** — the single best-fit head phrase for the cluster.
- **Supporting variants** — 3-5 related long-tail keywords/questions from the raw list that belong under this cluster.
- **Search intent** — informational, commercial, or navigational.
- **Competition** — roll up the cluster's competition score from its member keywords (use the lowest/best score present, but note if the cluster is mixed).

If Search Console signals were present in the raw research, prioritize clusters that include a high-impression/low-position query — flag these as "validated demand" in the cluster notes.

### Step 3 — Save clusters output

Write `clusters.md` in the same folder as `raw_research_file`:

```markdown
# Topic Clusters — <Niche or Website>

Generated: <YYYY-MM-DD>
Source: <raw-research.md path>

## Cluster 1: <Cluster Name>

- **Primary keyword:** <keyword>
- **Supporting variants:** <kw1>, <kw2>, <kw3>
- **Intent:** informational | commercial | navigational
- **Competition:** Low | Medium | High — <one-line reason>
- **Notes:** <validated demand / GSC flag, if any>

## Cluster 2: <Cluster Name>

...
```

Sequence clusters by competition (lowest first) and topical logic (foundational topics before advanced ones) — this ordering becomes the editorial calendar's default pacing.

### Step 4 — Handoff

Report the output file path and the cluster count. Tell the user (or the orchestrating automation) to run the `content-planner` skill next, pointing it at this `clusters.md` file.
