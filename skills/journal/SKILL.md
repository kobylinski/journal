---
name: journal
description: >-
  Capture development history into the project's journal - decisions, research verdicts,
  tombstones, lessons, external sources, session summaries, reminders, and drafts. Use when the
  user asks to journal, save, log, keep, or record one of these (e.g. "save this decision",
  "keep this email", "note this dead-end"). It writes only on the user's request. Not for
  durable docs or specs, nor cross-session memory.
---

# Journal

The journal is **development history**, captured as the work happens. Code answers *what*;
the journal answers *why*, *what was tried*, and *what was decided*.

## Know when to act

The **gate** opens on the user's go - when the user asks to create or update an entry. The agent
may notice a worthy moment (a decision reached, an approach abandoned, an artifact received) and
**offer** to journal it, but never writes without a yes. A project may authorise autonomous
writes for named conditions in its agent-instructions file (`CLAUDE.md` or `AGENTS.md`); absent
that, offering is as far as the agent goes.

## Know the current date and time

Before writing, determine the current date and time from the system (run `date`). Never
assume, infer, or reuse a remembered value - it drives the day-folder and `created`.

## Know the user

Before writing, determine the repository user from git (`git config user.name`, which falls back
to global config). This is the entry's `author`; never guess or free-type it. If git is
unavailable or comes back empty, ask the user once and use their answer - do not block, and do
not invent a name.

## Know where to store the entry

Write under `docs/journal/` unless project-specific instructions set a different journal root;
follow the most specific applicable instruction. Within the root, nest entries in per-day
folders: `<root>/YYYY-MM-DD/<kind>-<slug>.md` - one folder per calendar day.

The journal is a **dated record**, and the day-folder structure guards it: today's entries can
still be refined, but once a day has passed its entries are settled. Do not rewrite the past -
correct or extend it with a new dated entry that references the old. A `status` demotion to
`archived` is the one exception: metadata, not a rewrite.

## Compose the entry

1. **Classify** - decide which kind the entry is from the catalog below, then open that kind's
   file for what is worth capturing. No catch-all: if nothing fits, do not force an entry (see
   [Out of scope](#out-of-scope)).
2. **Name the file** - `<path>/<kind>-<slug>.md`. Create the day folder if it does not exist.
   Slug the title: transliterate to ASCII, drop punctuation and emoji, lowercase, kebab-case, cap
   ~60 chars. Never overwrite - if the name is taken, append `-2`, `-3`, and so on.
3. **Stamp the frontmatter** - agent-filled, never asked; one rule per attribute:
   - `type` - always `journal`.
   - `kind` - the kind chosen in step 1.
   - `title` - short and specific.
   - `status` - `confirmed` (settled, trustworthy) or `provisional` (tentative: a proposal,
     hypothesis, or unfinished draft). Superseded is *derived* from the reference graph;
     `archived` is set only by a later **demotion**, a status-only change that never rewrites the body.
   - `author` - the git user (from Know the user).
   - `created` - date and time, with UTC offset.
   - `tags` - keywords for retrieval.
   - any extra keys the kind file names (e.g. `source` adds `medium`, `origin`, `received`).
   - reference keys (optional) - before stamping these, search existing entries by tag and title
     for ones on the same matter (most recent first; a handful is enough - do not scan
     exhaustively) and link the ones this entry genuinely touches. Each is a forward reference to
     a prior entry, valued
     with its path relative to the journal root; the journal grows forward - past entries are extended by new
     references, not rewritten - and reverse links are derived by the index. Keys:
     - `sourced-from` - derived from a `source` (or other entry)
     - `consequence-of` - records a consequence of a prior entry
     - `follows-up` - continues / updates a prior entry
     - `resolves` - closes a prior `reminder` (or other open item); open/closed is derived from this
     - `supersedes` - replaces a prior entry (forward-only; old entry untouched)
4. **Write the body** - the shape is the agent's; the kind file lists what is worth including,
   not a fixed form. Do not interrogate for completeness - capture what is there. But if the
   piece that makes the kind valid is missing (a `decision` with no rejected alternative,
   `research` with no verdict, `lesson` with no cost), reclassify to a kind that fits rather than
   ask; if none fits, do not force an entry.
5. **Confirm** - report the path back to the user.

Example frontmatter:

```yaml
---
type: journal
kind: decision
title: Pin Carrier 411 debounce to 750 ms
status: confirmed
author: Marek Kobylinski
created: 2026-06-30T14:32:00+02:00
tags: [carrier-411, debounce]
sourced-from: 2026-06-29/source-fmcsa-rate-limit.md   # optional reference key
---
```

### decision

A choice between real options that you commit to, with a named rejected alternative - the
loser. Use it to record the path taken and why the loser lost.
Read `kinds/decision.md` for more details.

### research

An investigation of options or feasibility that ends in a verdict. Use it to keep the
comparison and the recommendation, which the code never shows.
Read `kinds/research.md` for more details.

### tombstone

Marks non-existence: an approach tried and abandoned, or work deliberately not done. Use it so
the path-not-taken and the reason survive, since code cannot show what is absent.
Read `kinds/tombstone.md` for more details.

### lesson

A durable rule or convention and the cost that earned it. Use it when "from now on, always or
never X" crystallises from real pain.
Read `kinds/lesson.md` for more details.

### source

A verbatim external artifact - email, transcript, incoming spec, feedback, task - received,
not authored. Use it to keep the original so other entries can cite it; it is the root of the
reference graph.
Read `kinds/source.md` for more details.

### summary

A session recap that consolidates many commits into one thread and names the open ends. Use it
to carry the narrative and the forensic detail worth keeping - a bug's root cause and the
trails that failed.
Read `kinds/summary.md` for more details.

### reminder

A known issue you deliberately park. Use it to note what it is and why now is not the time - a
record, not a task to schedule.
Read `kinds/reminder.md` for more details.

### draft

In-flight thinking too big to leave in the conversation but not yet a committed spec. Use it to
park a design you are still shaping, before it graduates to a doc or dies as a tombstone.
Read `kinds/draft.md` for more details.

## Out of scope

These are not journal entries: finished implementation specs or plans, committed
design/architecture docs, API/event reference, operational runbooks, and cross-session memory.
When asked to journal one of these, do not journal it and do not silently move it - say it is
not a journal entry and ask the user where it should go. An *incoming* spec the user works from
is not a doc; it is a `source`.
