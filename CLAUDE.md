# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository summary

Static site for "Hard Way Hacking and Coding" (a cybersecurity learning community), built with Hugo and the Hextra theme (loaded as a Hugo Module, not vendored). The Hugo project root is `roadmap/`, not the repository root — always `cd roadmap/` before running Hugo commands.

## Commands

Run from `roadmap/`:

```bash
hugo mod get                          # resolve/update theme module (writes go.mod/go.sum — see note below)
hugo server --bind 0.0.0.0 --port 1313   # dev server, drafts hidden
hugo server --buildDrafts --bind 0.0.0.0 --port 1313   # dev server, drafts visible (needed to preview roadmap stub pages)
hugo --gc --minify                    # production build (matches CI), outputs to roadmap/public/
```

There is no lint/test suite; correctness is verified by building and checking rendered output in `public/`, or via the dev server.

**Theme version care**: `go.mod` pins `github.com/imfing/hextra`. Plain `hugo mod get` (no args) silently upgrades to latest and rewrites `go.mod`/`go.sum` — if that happens unintentionally, `git checkout -- go.mod go.sum` to revert. Only bump the version deliberately.

CI (`.github/workflows/pages.yml`) builds with a pinned Hugo release (currently 0.147.7) and deploys `roadmap/public/` to GitHub Pages on push to `main`. The devcontainer/local Hugo may be newer — if a template feature depends on the Hugo version, check it works with the CI-pinned release too.

## Architecture

### Two content sections, two different data models

Content lives under `roadmap/content/`. The two sections deliberately use different structures, chosen for what each needed:

- **`content/faq/`** — flat sibling pages (no subfolders). Each FAQ entry is one file with `category`, `also_asked` (alternate phrasings), and optional `weight` front matter. The `/faq/` list page groups entries by `category` (sorted alphabetically) and renders each via the `faq-entry` partial as a collapsible `<details>` accordion.
- **`content/roadmap/`** — real nested Hugo sections, one folder per curriculum level (`foundational-knowledge/`, `intermediate-knowledge/`, `applied-security/`, and eventually `advanced-knowledge/`), each with its own `_index.md` (`title` + `weight` control level order, `sidebar: {open: true}` keeps it expanded in the left nav). A page's "level" is simply which folder it's in — there is no `level` front-matter field. Individual topic pages carry `topics`, `milestones`, `knowledge_check`, `certifications` (all optional lists) plus `weight` for ordering within their level. `content/roadmap/introduction.md` (weight 10) and `content/roadmap/special-thanks.md` (weight 900) are standalone pages that exist solely so they appear as their own entries in the sidebar tree, at the top and bottom respectively — the root `/roadmap/_index.md` also duplicates the full "Introduction" text inline by design.

This split exists because the sidebar/TOC only reflect real Hugo page structure, not custom front matter — flat-with-front-matter works for FAQ's non-hierarchical accordion, but the roadmap's left-hand tree navigation required actual nested sections.

### Layout overrides (`roadmap/layouts/`)

Nothing here replaces the Hextra theme wholesale — everything is an additive override or a new partial, following Hugo's module-mount lookup (site files with the same relative path win over the theme's). Read the theme's own template at the matching path in the Hugo module cache (`$(go env GOPATH)/pkg/mod/github.com/imfing/hextra@<version>/layouts/...`) before changing one of these, to keep parity with upstream markup/classes:

- `layouts/faq/list.html` — overrides the FAQ section's list page: groups entries by category, sorts within category by weight then title.
- `layouts/roadmap/list.html` — overrides every roadmap section-index page (root outline *and* each level's `_index.md`, since Hugo's page `type` defaults to the top-level section for nested sections too). Branches on `eq .Parent site.Home` to tell the root outline (renders every level + all its topics) apart from a single level's own page (renders just that level's topics).
- `layouts/roadmap/single.html` — overrides individual roadmap topic pages; injects the `roadmap-summary` partial above `.Content`.
- `layouts/partials/faq-entry.html` / `layouts/partials/roadmap-summary.html` — the actual "unified look" templates: they render a page's front-matter fields (category/also_asked for FAQ; topics/milestones/knowledge_check/certifications for roadmap, laid out as two columns) instead of each page hand-formatting its own summary block. Both are reused in more than one place (e.g. `roadmap-summary` renders identically whether linked from the outline or shown atop the topic's own page), so front matter is the single source of truth — don't reintroduce hand-written duplicate summaries in a page's Markdown body.
- `assets/json/search-data.json` — overrides the theme's FlexSearch index template so a FAQ page's `also_asked` aliases get folded into its indexed text (otherwise the site search can't find an entry by an alternate phrasing). If you touch this, note that Hugo's `merge` takes precedence from its *first* argument — `merge $data (dict "" newValue)` overwrites, `$data | merge (dict "" newValue)` does not (the piped value becomes the trailing/losing argument).
- `archetypes/faq.md` — front-matter scaffold for `hugo new faq/<slug>.md`.

### Draft stub pages

Several roadmap topics referenced in the curriculum don't have real content yet (e.g. under `intermediate-knowledge/`). These exist as real content files with full front matter (topics/milestones/etc.) and `draft: true`, with a `TODO: write this section.` body. They're excluded from normal builds and from the sidebar/outline automatically by Hugo's draft handling — use `--buildDrafts` to see and edit them in place.

## Content review requirement

Any content authored by Claude (FAQ answers, roadmap topic write-ups, or edits to existing prose) must be reviewed in full by a human before it is committed and pushed. This applies to the substance of the writing, not just template/code changes — Claude should flag newly-written or substantively-edited content for review rather than committing it unprompted.
