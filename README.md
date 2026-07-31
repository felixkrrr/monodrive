# Monodrive skill

Monodrive is a Brain: durable memory for whatever matters to you, held on a
server and reached over MCP. Your agent looks things up in it before answering
and writes things down as they land, without being asked each time.

This repo is the skill that teaches it how. Version 1.0.1.

## Install

```bash
git clone https://github.com/felixkrrr/monodrive-skill ~/.claude/skills/monodrive
```

Then sign in at https://app.monodrive.ai/login — a magic link, no password, and signing in for the
first time creates your Workspace — and connect your agent:

```bash
claude mcp add --transport http monodrive https://app.monodrive.ai/mcp
```

Run `/mcp`, pick Monodrive, approve in the browser. Or just ask your agent to
set up Monodrive once the skill is installed; it will walk you through it.

Don't set an `Authorization` header or paste an API key. The server uses OAuth,
and a hand-set header stops the sign-in flow from running at all.

## Updating

The skill does not update itself, on purpose — nothing changes under you.

```bash
git -C ~/.claude/skills/monodrive pull
```

Or ask your agent to check for a newer version.

## Removing it

```bash
rm -rf ~/.claude/skills/monodrive
```

Your Brain is untouched; it lives on the server. Delete the data itself from
your Workspace settings.

## What's in here

`SKILL.md` and three reference files, all prose you can read. An agent
instruction file you cannot inspect is one you have to take on trust, and this
one is entirely about your own notes.
