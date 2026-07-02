# journal

A Claude Code plugin that captures **development history** - the *why*, *what was tried*, and
*what was decided* that fades from the code and from memory within weeks. Code answers *what*;
the journal answers the rest.

It is a **dated record**: low-friction to write, grown by new entries that reference old ones
rather than by rewriting the past. Eight entry kinds, with a light per-project configuration so
it adapts to how you already work.

## Why

Working with an AI agent is a constant fight for good context. A year ago I added fifteen lines
to `CLAUDE.md`: summarise each session into a dated file under `docs/journal/`. Those files
turned out to be ready-to-load context that brought the agent back on track - the best thing I
found that month. A year of daily use grew it into this skill: decisions with their rejected
alternatives, dead-ends nobody walks twice, lessons with the cost that earned them. Plain
Markdown, versioned in git - so the history is readable not just by my agent, but by my
coworkers and their agents too.

## What it captures

| kind | write this when... |
|---|---|
| `decision` | a committed choice with a *named loser* |
| `research` | an options or feasibility investigation that ends in a verdict |
| `tombstone` | an approach abandoned, or work deliberately *not* done |
| `lesson` | a standing rule and the cost that motivated it |
| `source` | a verbatim external artifact, *received not authored* |
| `summary` | a session recap: commits consolidated, open threads named |
| `reminder` | a known issue deliberately parked: what it is and why now is not the time |
| `draft` | in-flight thinking, too big for context, not yet a spec |

By default the journal writes only when you ask; a project can widen that to record chosen
moments automatically.

## Install

Three ways, one repo. Whichever you use, the whole skill folder travels - `SKILL.md` and `kinds/`.

**`npx skills` (any agent)** - installs to a universal `.agents/skills/journal/` that Codex,
Copilot, OpenCode, and others read, symlinked into Claude Code:

```
npx skills add kobylinski/journal
```

**Claude Code plugin** - managed install with updates. The repo doubles as its own
marketplace named `kobylinski`, so the install id is `journal@kobylinski`:

```
/plugin marketplace add kobylinski/journal
/plugin install journal@kobylinski
```

**Manual** - copy the folder into an agent's skills directory:

- Claude Code: `~/.claude/skills/journal/` (all projects) or `<project>/.claude/skills/journal/` (one repo)
- Other agents: `<project>/.agents/skills/journal/`

```
cp -r skills/journal ~/.claude/skills/
```

## Configure (optional)

Two things a project can set, in plain prose in its agent-instructions file (`CLAUDE.md`, or
`AGENTS.md` for Codex) - no schema required:

- **journal root** - where entries are written, if not the default `docs/journal/`.
- **when to act** - named conditions under which the agent may journal on its own, beyond
  waiting to be asked.

See [`skills/journal/SKILL.md`](skills/journal/SKILL.md).

## Layout

```
.claude-plugin/plugin.json   plugin manifest
skills/journal/
  SKILL.md                   the skill: preflight (act / date / user / path) then compose
  kinds/*.md                 one file per kind: what is worth capturing
```
