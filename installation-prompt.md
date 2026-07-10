# SEO Opportunity Finder — Installation Prompt

Paste everything below the line into a **new Zo chat** and send it. It's self-contained — the AI reading it has no memory of how this project was built, so it spells out every step. Swap the repo URL first if you're installing from a fork.

---

Fetch and install the "SEO Opportunity Finder" Zo automation from this public GitHub repo:

`https://github.com/robort-gabriel/seo-opportunity-finder`

Do the following, in order. Steps marked **(confirm)** must not proceed until I explicitly approve — don't treat silence or a prior approval as blanket permission.

### 1. Fetch the repo

- Target folder: `/home/workspace/Zo-Automations/seo-opportunity-finder/`.
- **(confirm)** If that folder already exists, tell me what's in it and ask whether to overwrite before touching anything.
- Clone or download the repo (it's public, no auth needed) into that folder, preserving its structure exactly:
  ```
  README.md
  installation-prompt.md
  persona.md
  automation-prompt.md
  starter-prompts.md
  Skills/seo-research/SKILL.md
  Skills/keyword-clustering/SKILL.md
  Skills/content-planner/SKILL.md
  Skills/content-planner/references/templates.md
  ```

### 2. Verify the skills

- Confirm each of `Skills/seo-research/SKILL.md`, `Skills/keyword-clustering/SKILL.md`, `Skills/content-planner/SKILL.md` exists and has valid frontmatter (`name` matching its folder, non-empty `description`).
- These skills are project-local by design. Do not copy them into the global `Skills/` folder or any other project — this automation only ever reads/writes inside `/home/workspace/Zo-Automations/seo-opportunity-finder/` and its output folder `/home/workspace/Content/SEO-Opportunities/`.

### 3. Create a dedicated persona

- **(confirm)** the name and scope with me before creating anything.
- Read `persona.md` in the repo and use its content verbatim: the `Name` field as the persona name, the `Prompt` field as the persona's system prompt. Do not paraphrase or shorten it.
- Create the persona (via the persona-creation tool) with that exact name and prompt text.
- After creating it, ask me whether to switch to it now (set it active) or leave it available to select later.

### 4. Offer to set up recurring automation

- **(confirm)** Ask me for: `niche_or_website` (required — a topic/niche or a domain I own), `pieces` (optional, default 5), `cadence` (optional, default weekly — this doubles as the run frequency).
- Do not create the scheduled agent until I explicitly confirm the niche/website and frequency.
- Explain plainly what the automation will do (run the 3-skill pipeline and write files under `Content/SEO-Opportunities/`), how often it will run, and that each run is a full Zo session — without inventing a specific cost figure.
- If I confirm, create a scheduled agent using the instructions in `automation-prompt.md` (filled in with my values) as its prompt, on the frequency I gave.
- If I decline or want to think about it, skip this step — ad hoc usage still works without it.

### 5. Report back

- Confirm: the install path, whether the folder was overwritten or created fresh, which persona was created (and whether it's active), and whether a recurring automation was set up (with its schedule) or left for later.
- Give me one ready-to-run example prompt from `starter-prompts.md` so I can try the pipeline ad hoc right away.

Throughout all of this, do not read, write, or modify any files outside `/home/workspace/Zo-Automations/seo-opportunity-finder/` and `/home/workspace/Content/SEO-Opportunities/`, and do not call any paid or external API — this automation is built to run entirely on free, built-in Zo tools and already-connected catalog integrations.
