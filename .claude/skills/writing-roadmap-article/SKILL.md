---
name: writing-roadmap-article
description: Use when adding, filling in, or reordering a topic in the Hard Way Hacking and Coding cybersecurity roadmap (content/roadmap/) — writing a new roadmap article, completing a draft stub topic, or adding a new curriculum level.
---

# Writing a Roadmap Article

## Overview

The roadmap (`content/roadmap/`) is organized as real nested Hugo sections, one folder per curriculum level: `foundational-knowledge/`, `intermediate-knowledge/`, `applied-security/` (and eventually `advanced-knowledge/`). A topic's level is simply which folder it lives in — there is no `level` front-matter field. Each topic's `topics`/`milestones`/`knowledge_check`/`certifications` front matter drives an auto-rendered two-column summary card shown both on the outline page and at the top of the topic's own page — never hand-write that block into the Markdown body, it will duplicate what the template already renders.

## Steps

1. **Find the right level folder**. List levels in curriculum order: `foundational-knowledge` → `intermediate-knowledge` → `applied-security` → `advanced-knowledge`. If a topic doesn't fit an existing level, that's a bigger call (new level folder + `_index.md` with `title`/`weight`) — check with a human before doing that.
2. **Check for an existing draft stub first.** Several topics already exist as placeholders (`draft: true`, body `TODO: write this section.`) with front matter already filled in — e.g. under `intermediate-knowledge/`. Run with `hugo server --buildDrafts` to see them; if one matches, fill in its body and flip `draft: false` rather than creating a new file.
3. **New topic file**: `content/roadmap/<level-folder>/<slug>.md`. Front matter:
   - `title`: the topic name.
   - `weight`: position within its level, not globally — existing topics in a level are usually spaced by 100 (100, 200, 300...) to leave room to insert between them later.
   - `topics` (list, aim for **4-6 items**): high-level subject headings covered — keep these short (a phrase, not a sentence); this is what "General Topics" shows in the summary card.
   - `milestones` (list): a **few good hands-on projects or exercises** — concrete, checkable things a learner should be able to *do*, not just know. Prefer "build/exploit/configure/write X" over "understand X".
   - `knowledge_check` (list, aim for **4-6 items**): terms/concepts a learner should recognize before moving on.
   - `certifications` (list): a **short list of the most relevant** industry certs — don't list every tangentially-related cert, or `None` if there genuinely isn't one worth naming.
   - `learning_resources` (list): learning resources for the topic, rendered as a table — see step 5.
   - All fields are optional and independently omitted if empty — a topic doesn't need all of them (e.g. `applied-security/_index.md` has none, just intro prose). The 4-6 count targets are a guideline for a normal topic, not a hard rule — a level-overview page like `applied-security/_index.md` is the exception, not the pattern to copy.
4. **Write the body** as the full article prose below the front matter — this is what only shows on the topic's own page, not in the outline.
   - Use **simplified technical English**: short sentences, plain everyday words over jargon, one idea per sentence, active voice. Spell out or briefly define any acronym or term of art on first use.
   - Unlike a FAQ answer, a roadmap article should give a **general overview** of the topic — enough for a learner to understand what it is, why it matters, and how it fits with neighboring topics, before they go deepen their knowledge elsewhere. It doesn't need to be exhaustive or replace dedicated documentation.
   - Don't write a "Resources" section into the body — it's front matter (step 5), not prose.
5. **Learning Resources**: unlike Topics/Milestones/etc., this is *not* part of the top summary card — it's rendered as a table in its own `## Resources` section at the very bottom of the topic's own page only (not in the outline, not in the summary card), via `learning_resources` front matter. Every article uses this same table shape — Title / Cost / Time / Link / Notes:
   ```yaml
   learning_resources:
     - title: "Google Scholar"
       cost: "Free"
       time: "Varies"
       url: "https://scholar.google.com"
       link_text: "Google Scholar"
       notes: "Free access to academic, peer-reviewed papers"
     - title: "Complete CompTIA Network+ Training"
       cost: "$20"
       time: "19 Hours"
       url: "https://www.udemy.com/course/kevin-netplus/"
       link_text: "Udemy"
       notes: "Full CompTIA Network+ course"
   ```
   - `cost`: the actual price where known (`Free`, `$20`, `$129`) rather than just a Free/Paid label — that's the existing convention (see `foundational-knowledge/hardware.md` for a real example) and it's more useful to a learner deciding what to spend.
   - `time`: a real estimate if you know it, `Varies` if you don't. Don't invent a specific number you're not confident in.
   - `link_text` is optional — it's the link's visible text (e.g. `Udemy`, `YouTube`, the site name), not the resource title; defaults to "Link" if omitted.
   - Include a mix of free and paid resources where reasonable options exist for both — don't skip a category just because the first resource you thought of was free.
6. **Level ordering**: to reorder levels themselves (not topics within one), edit that level's `_index.md` `weight`. Don't touch a topic's `weight` to influence its level — that only reorders siblings.
7. **Preview**: `hugo server --buildDrafts --bind 0.0.0.0 --port 1313` from `roadmap/`. Check the topic renders under the right level on `/roadmap/`, appears in the correct sidebar position, the summary card looks right in two columns (Topics/Milestones left, Knowledge Check/Certifications right), and the Resources table shows up at the bottom of the topic's own page.
8. Before committing: a human must review the full written article text — see the repo's `CLAUDE.md` content review requirement.

## Common Mistakes

- Adding a `level` front-matter field — it doesn't exist anymore; move the file into the right folder instead.
- Hand-writing a "General Topics / Milestones / ..." block into the article body — this used to be the pattern but is now entirely front-matter-driven and template-rendered; a hand-written block will just show twice.
- Using a global weight scale across levels — weight only orders siblings within the same folder.
- Writing `topics`/`knowledge_check` as a sprawling list of 10+ items instead of the 4-6 that keep the summary card scannable.
- Writing a "Resources" section as Markdown prose or a hand-written table in the body instead of `learning_resources` front matter — it won't render (the template only reads it from front matter).
- Using a vague `cost: "Paid"` label instead of the real price when you know it (e.g. `$20`) — match the existing convention of naming the actual cost.
- Only including free resources, or only paid, when good options exist for both.
