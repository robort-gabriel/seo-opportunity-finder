---
name: content-planner
description: Turn topic clusters into an editorial calendar, blog outlines, suggested titles, and internal linking recommendations. This is stage 3 (final) of the SEO Opportunity Finder pipeline. Use when the user has clustered keyword topics (e.g. a clusters.md file produced by the keyword-clustering skill) and wants a ready-to-execute content calendar. Also hands off to content-plan-builder/content-plan-editor for turning a chosen cluster into a tracked, published post.
metadata:
  author: robort.zo.computer
---

# Content Planner

Turns topic clusters into a ready-to-execute editorial calendar: titles, blog outlines, and internal linking recommendations, paced into a schedule.

## Inputs

- `clusters_file` (required): path to a `clusters.md` file produced by the `keyword-clustering` skill (e.g. `Content/SEO-Opportunities/<slug>/<date>/clusters.md`).
- `cadence` (optional, default weekly): how the editorial calendar should be paced (e.g. one piece/week for 4 weeks).
- `website` (optional): the site to check for internal linking opportunities, if this pipeline is analyzing a website the user owns rather than a bare niche.

## Workflow

### Step 1 — Read the clusters

Read each cluster from `clusters_file` (already sequenced lowest-competition/most-foundational first).

### Step 2 — Generate per-cluster outputs

For each cluster produce:

- **Suggested title** — SEO-friendly, matches the primary keyword naturally.
- **Blog outline** — H2/H3 structure, 5-8 sections, one line per section describing its content.
- **Internal linking** — only if `website` was provided: search the site's existing published content (its own repo/CMS, or `Content/` if it's this workspace's own site) for related pages and recommend 2-3 internal links per new piece, plus 1-2 links from existing pages back to the new piece. Omit this field entirely if no content library is available — do not invent links.

### Step 3 — Sequence into a calendar

Assign each cluster to a week/slot per `cadence`, preserving the cluster file's existing lowest-competition-first ordering.

### Step 4 — Save outputs

Write these files in the same folder as `clusters_file`:

- `editorial-calendar.md`
- `blog-outlines.md`
- `titles.md`
- `internal-linking.md` (omit entirely if Step 2's internal linking was skipped)

See `references/templates.md` for exact file formats — follow them precisely (table separators, no extra spaces) so the output stays consistently parseable.

### Step 5 — Report back

Summarize in chat: number of pieces planned, the top 3 highest-priority (lowest competition + highest relevance), and the output folder path. If running as a scheduled/unattended automation, keep the summary to 3-5 bullet points since it may be delivered via SMS/email/Slack.

## Handoff to other skills

- To turn a chosen cluster into a fully tracked post (`metadata.md`/`caption.md`/`resource-brief.md`/`STATUS.md`), use `content-plan-builder`.
- To add an entry to the public content-plan dashboard, use `content-plan-editor`.
- To draft the full article once a topic is chosen, use `website-article-writer` or `ai-tutorial-guide`.

## Notes

This skill produces calendar structure, not finished articles.
