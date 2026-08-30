---
name: writing-faq-entry
description: Use when adding, splitting, or rephrasing a question on the Hard Way Hacking and Coding FAQ page (content/faq/) — creating a new FAQ entry, adding an alternate phrasing of an existing question, or reorganizing FAQ categories.
---

# Writing a FAQ Entry

## Overview

FAQ entries in this repo are flat page-bundle files, not a hand-written Q&A list. Each question is its own Markdown file whose front matter drives the accordion UI on `/faq/` — the rendering (grouping, ordering, "also asked as" aliases, search indexing) is entirely generated from that front matter by `layouts/partials/faq-entry.html` and `layouts/faq/list.html`. Never hand-format a Q&A block inline in `_index.md`; it will not render the same way.

## Steps

1. **Pick a slug and scaffold it**: `cd roadmap && hugo new faq/<slug>.md` (uses `archetypes/faq.md`). Files live flat in `content/faq/` — no subfolders.
2. **Fill in front matter**:
   - `title`: the question, phrased exactly as most people would ask it.
   - `category`: an existing category (`Hacking Questions`, `Programming Questions`) to group under, or a new one — any category with at least one page appears as its own heading, sorted alphabetically. Don't invent a category for a single one-off entry unless it's genuinely a new topic area.
   - `also_asked`: list of alternate phrasings of the *same* question (not related-but-different questions). These show inline under the title in the collapsed accordion and are folded into the site search index — use this instead of creating duplicate entries with the same answer.
   - `weight` (optional): controls order within the category; omit to default to 100, with ties broken alphabetically by title.
   - `draft: false` once ready to publish (archetype defaults to `true`).
3. **Write the answer** as the page body (plain Markdown, below the front matter):
   - Use **simplified technical English**: short sentences, plain everyday words over jargon, one idea per sentence, active voice. Spell out or briefly define any acronym or term of art on first use.
   - Answer the question **succinctly** first — lead with the direct answer, not a wind-up.
   - Then add just enough context to head off the most common immediate follow-up questions or objections a reader would have (a "why", a caveat, or a "but what about X" — whichever applies). Don't pad beyond what's needed for that; this isn't a roadmap article.
   - GitHub-style admonitions render natively, e.g.:
     ```markdown
     > [!CAUTION]
     > Scammers will claim they can recover a hacked account. They can't — don't pay them.
     ```
4. **Preview**: `hugo server --bind 0.0.0.0 --port 1313` from `roadmap/`, check `/faq/` — the entry should appear collapsed under the right category heading, with any aliases visible before expanding.
5. Before committing: a human must review the full written answer text (not just the diff shape) — see the repo's `CLAUDE.md` content review requirement.

## Common Mistakes

- Adding a Q&A block directly to `content/faq/_index.md` — it won't render as an accordion; `_index.md` is just the page intro now.
- Creating a second entry for a reworded version of an existing question instead of adding it to `also_asked` — this duplicates the answer and splits search relevance.
- Forgetting `category` — the entry still renders, but lands under a generic "Uncategorized" heading instead of a meaningful group.
