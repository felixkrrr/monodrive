# Monodrive skills

Monodrive is a Brain: durable memory for whatever matters to you, held on a
server and reached over MCP. Your agent looks things up in it before answering
and writes things down as they land, without being asked each time.

This repo holds the skills that teach it how.

| Skill | What it does |
| --- | --- |
| `monodrive-query` | Answers a question from the Brain, with citations |
| `monodrive-capture` | Writes something into the Brain so it survives the session |
| `monodrive-setup` | Walks you through connecting the MCP server and signing in |
| `monodrive-update` | Installs the skills, or updates them to the latest version |

## Install

Each folder is its own skill and goes in at the top level of a skills directory.
Install globally so they work in every project:

```bash
git clone --depth 1 https://github.com/felixkrrr/monodrive-skills /tmp/monodrive-skills && cp -R /tmp/monodrive-skills/monodrive-* ~/.claude/skills/ && rm -rf /tmp/monodrive-skills
```

To scope them to a single repo instead, use that repo's `.claude/skills/`.

That's the skills installed, not Monodrive connected. Start a new session and ask
your agent to set up Monodrive — `monodrive-setup` takes it from there: signing in,
connecting the MCP server, and checking it actually works.

## Updating

The skills don't update themselves, on purpose — nothing changes under you. Ask
your agent to update Monodrive and `monodrive-update` handles it: it finds where
the skills are installed, compares versions against this repo, and replaces only
what moved.

## Removing them

```bash
rm -rf ~/.claude/skills/monodrive-*
```

Your Brain is untouched; it lives on the server. Delete the data itself from your
Workspace settings.

## What's in here

Four `SKILL.md` files, all prose you can read. An agent instruction file you
cannot inspect is one you have to take on trust, and these are entirely about
your own notes.
