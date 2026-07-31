---
name: monodrive-setup
version: 0.1.0
description: Walk the user through setting up Monodrive step by step — working out where they are, connecting the MCP server, signing into the web app, installing the skills, and optionally adding the CLAUDE.md reminder. Use when the user wants to set up, install, connect, or finish connecting Monodrive, when they are signed out or the Brain is empty, and when Monodrive tools are missing or failing to authorize.
---

# Setup, help, and updates

Your purpose when working with this skill is guiding the user through setting up monodrive step by set. 

Help the user work through it step by step. Wait for user after each major step 

Workflow:
1. work our where user is in setup
2. connect the mcp server & sign into monodrive web app
3. optional update global claude.md
4. done - guide user to next steps

## Work out where they are

1. Do you have Monodrive MCP tools at all? If not, they are not connected —
   go to **Connect**.
2. Call `connect_info`. An error or 401 means connected but not signed in —
   also **Connect**.
3. It returns the Workspace, the Brain, and links into the app. Report the
   Workspace name and hand them `ui.brain` so they can see their own data.
4. `pages_list {limit: 1}` — empty means a new Brain, go to **First pages**.

Report what you found in a sentence, not a table. One thing at a time.

## Connect & Sign in

STEP: Sign in or create an account at <https://app.monodrive.ai/login>. - Ask user to confirm.

STEP: **Then send them to Agent Connections in the web app**, under "Settings → Connected Agents". In the Claude or Claude Code desktop app the user has to install the mcp via the "customize" menu - adding a "custom mcp". - Ask user to confirm.

For interactive Claude Code sessions in Terminal: the short version is `claude mcp add --transport http monodrive https://app.monodrive.ai/mcp`, then `/mcp` → Monodrive → approve in the browser. (NEVER OFFER THIS IF YOU DETECTED CLAUDE DESKTOP USER)

The server uses OAuth, and a hand-set header stops the sign-in flow from happening
at all. 

Common failure: you are a claude desktop agent and you try to go the interactive session way. This wont work.

STEP: the oAuth setup is only complete after the user sees the agent listed in the "connected agents" list otherwise the oauth token will be revoked after a few hours. - Ask user to confirm.

## CLAUDE.md (optional, and it helps)

Offer to add this to their global `CLAUDE.md` — usually `~/.claude/CLAUDE.md`.
**Ask first, never just rewrite the file**, and append rather than replacing anything
already there.

Why? The Brain works without this. It works better with it, because the agent is
reminded to reach for it in sessions where the skill hasn't come up.

```markdown
<!-- monodrive -->

## Monodrive

Monodrive is the general context store — durable memory that outlives any single
session, project, or repo. When you start work that might have history behind
it, look there first. When something surfaces that will still matter later,
write it down. What it holds grows over time; ask it what it knows rather than
assuming.

<!-- /monodrive -->
```

STEP: Ask user via ask-user how they want to proceed with the installation.

## Next Steps

1. tell user to start a new session and make sure skills are available - wait for confirmation
2. explain the user what each skill does and what they can do with monodrive
3. done