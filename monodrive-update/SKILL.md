---
name: monodrive-update
version: 1.0.0
description: Install or update the Monodrive skills from https://github.com/felixkrrr/monodrive-skills. Use when the user asks to update Monodrive, check for a newer version, install the skills, or when a Monodrive skill is missing or out of date.
---

# Install or update the Monodrive skills

Source of truth: <https://github.com/felixkrrr/monodrive-skills>. The skills never
update themselves — this only runs when the user asks.

## 1. Find where they are installed

Look for `monodrive-*/SKILL.md` in the usual places:

```bash
ls -d ~/.claude/skills/monodrive-* ./.claude/skills/monodrive-* 2>/dev/null
```

Nothing there? Go to **Install**. Found in more than one place? Tell the user and
ask which to update. Some folders present but not all four (`monodrive-query`,
`monodrive-capture`, `monodrive-setup`, `monodrive-update`) — update what's there
and install the rest alongside it.

## Install

Only when they aren't installed yet. Default to a global install at
`~/.claude/skills/` so the skills work in every project. Confirm the location
with the user first — mention that a project-local `.claude/skills/` is the
alternative if they want it scoped to one repo.

```bash
git clone --depth 1 https://github.com/felixkrrr/monodrive-skills /tmp/monodrive-skills-latest
```

Copy each `monodrive-*` folder from the clone into the chosen skills directory —
the folders go in at the top level, one `SKILL.md` per folder, not nested inside a
wrapper directory. Clean up `/tmp/monodrive-skills-latest`, then skip to
**Report**, and point them at the `monodrive-setup` skill to connect the MCP
server and sign in.

## 2. Compare versions

Each skill carries its own `version:` in its `SKILL.md` frontmatter. Read the
installed one, and fetch the same line from `main` — for example:

```bash
curl -fsSL https://raw.githubusercontent.com/felixkrrr/monodrive-skills/main/monodrive-query/SKILL.md | head -5
```

All versions match? Say so in one line and stop. Otherwise note which skills moved.

## 3. Update

If the install directory is a git checkout (`.git` present), pull:

```bash
git -C <dir> pull --ff-only
```

Otherwise fetch a fresh copy and replace the skill folders in place:

```bash
git clone --depth 1 https://github.com/felixkrrr/monodrive-skills /tmp/monodrive-skills-latest
```

Then, for each installed `monodrive-*` folder, copy the matching folder from the
clone over it. Copy folders that exist locally plus any new `monodrive-*` folders in
the clone; never delete a folder the user has that upstream dropped — mention it
instead. Clean up `/tmp/monodrive-skills-latest` when done.

If the user has local edits to a skill file, stop and say so rather than overwriting.

## 4. Report

One or two lines: what was installed or updated (old version → new version), which
folders changed, and that they need to start a new session before the skills load.
