# Output File Templates

All files below are written to the same folder as the input `clusters.md` (i.e. `Content/SEO-Opportunities/<slug>/<YYYY-MM-DD>/`). Follow the table formatting exactly (no extra spaces inside separator rows) so downstream tooling can parse these reliably.

## editorial-calendar.md

```markdown
# Editorial Calendar — <Niche or Website>

Generated: <YYYY-MM-DD>

| Week | Title | Primary Keyword | Cluster | Competition | Status |
|---|---|---|---|---|---|
| 1 | <title> | <keyword> | <cluster name> | Low | planned |
| 2 | <title> | <keyword> | <cluster name> | Medium | planned |
```

## blog-outlines.md

```markdown
# Blog Outlines — <Niche or Website>

## <Cluster Name>

**Title:** <title>
**Primary keyword:** <keyword>
**Supporting keywords:** <kw1>, <kw2>, <kw3>
**Intent:** informational | commercial | navigational
**Competition:** Low | Medium | High — <one-line reason>

### Outline
1. <H2 section> — <one-line description>
2. <H2 section> — <one-line description>
   - <H3 sub-section>
...
```

## titles.md

```markdown
# Suggested Titles — <Niche or Website>

1. <title 1>
2. <title 2>
...
```

## internal-linking.md

Only generate this file when a website was provided and existing content was actually found. Do not invent links.

```markdown
# Internal Linking Recommendations — <Website>

## <Cluster Name / New Piece Title>

**Link to (from the new piece):**
- <existing page title> — <url or path>

**Link from (add a link on these existing pages, pointing to the new piece):**
- <existing page title> — <url or path>
```
