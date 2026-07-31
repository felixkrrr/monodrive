# Setup, help, and updates

## Work out where they are

1. Do you have Monodrive MCP tools at all? If not, they are not connected —
   go to **Connect**.
2. Call `connect_info`. An error or 401 means connected but not signed in —
   also **Connect**.
3. It returns the Workspace, the Brain, and links into the app. Report the
   Workspace name and hand them `ui.brain` so they can see their own data.
4. `pages_list {limit: 1}` — empty means a new Brain, go to **First pages**.

Report what you found in a sentence, not a table. One thing at a time.

## Connect

Sign in or create an account at <https://app.monodrive.ai/login>. It is a magic
link, no password, and signing in for the first time creates the Workspace too —
there is no separate signup.

**Then send them to Connections in the web app**, under Settings → Account →
Connections. It has per-agent instructions with the exact commands to copy, kept
current with whatever each client expects. Send them there rather than
reciting setup from here — this file cannot track a client changing its flags,
and that page can.

If you are already connected, `connect_info` returns the direct link as
`ui.connections`. If you are not, they can reach it from the app after signing
in.

For Claude Code the short version is `claude mcp add --transport http monodrive
https://app.monodrive.ai/mcp`, then `/mcp` → Monodrive → approve in the browser.
Tokens refresh themselves afterwards, and `/mcp` has a re-authenticate entry if
one lapses.

Never tell anyone to set an `Authorization` header or paste an API key. The
server uses OAuth, and a hand-set header stops the sign-in flow from happening
at all. Headless runs (`claude -p`) cannot authenticate — sign in once from an
interactive session first.

## First pages

An empty Brain is where people bounce. Don't explain the system — put something
real in it. Ask what it should remember for them, then write it. People and
organisations land properly typed straight away, so they look right immediately;
anything else still gets written, using their word for what it is.

Two or three pages is a good first session. Then say what happens next in one
line: mention it later and you will find it.

## CLAUDE.md (optional, and it helps)

The Brain works without this. It works better with it, because the agent is
reminded to reach for it in sessions where the skill hasn't come up.

Offer to add this to their global `CLAUDE.md` — usually `~/.claude/CLAUDE.md`.
**Ask first, never rewrite the file**, and append rather than replacing anything
already there:

```markdown
<!-- monodrive -->

## Monodrive

Monodrive is the general context store — durable memory that outlives any single
session, project, or repo. When you start work that might have history behind
it, look there first. When something surfaces that will still matter later,
write it down. What it holds grows over time; ask it what it knows rather than
assuming. To read or write it, use the `monodrive` skill.

<!-- /monodrive -->
```

It names no tools and no kinds of page on purpose. This is the one file nobody
can push a fix to, so anything perishable written here stays wrong.

Two things to check before adding it. If there is already a Monodrive section,
show it to them and offer to replace it rather than ending up with two. If
another memory or notes system has its own "check this first" rule in there, say
so plainly — two such rules compete, the agent follows whichever it read last,
and the user sees the Brain work intermittently. Offer to split them by subject.

Checking for a newer version of this skill is in `SKILL.md` — it needs no
setup context and should not cost a read of this file.
