# The Schema

The Schema is the kinds of page this Brain knows and how each should be written.
It starts small — people, organisations, and a plain page for everything else —
and grows from what the user actually writes rather than from what we guessed.

## Two levers, in order

**Change the words.** Every type carries `instructions`, plus a description per
property and for its body and timeline. That text is what agents follow when
they write, so when pages of a type keep coming out wrong, this is almost always
the fix — not the shape of the type, and never an edit to this skill. "Stop
putting today's status in person bodies." "We call them accounts." Those are
`instructions` edits. It is also the only guidance that can differ per Brain.

**Change the shape.** Adding a type, property, or relationship. Heavier: it
changes what validates for everyone in the Workspace.

## Reviewing

Read-only. Look, rank, report, ask — never repair as a side effect of a review.

- `pages_list {limit: 100}` for the spread of types. Say when you are sampling;
  there are no totals.
- **Untyped pages grouped by their Suggested Type** — the most valuable thing
  here, and what a new type gets made from.
- Untyped pages carrying no Suggested Type at all: nothing records what they
  were meant to be. A trend to report, not a repair.
- Entity pages missing whatever their type resolves identity on. Without it they
  resolve by name, which is where duplicates come from.
- Orphans — no links, no backlinks. Sample rather than fetching everything.

Lead with what costs something. If nothing does, say the Brain is healthy in one
line and stop.

## When untyped pages have earned a type

| How many             | Do                                                              |
| -------------------- | --------------------------------------------------------------- |
| A handful            | Nothing. A type is permanent; three pages is not evidence.      |
| Enough to be a habit | Add the type, or an alias if they are really an existing thing. |
| Already a category   | Add the type, with the properties those pages already share.    |

Prefer an **alias** when the pages are the existing thing under another word —
`contact` for `person`. Prefer a **new type** when they need their own
properties or instructions.

Promotion is retroactive and cheap: declaring a type absorbs matching untyped
pages the moment it lands. Nothing is migrated, nothing is rewritten. That is
why waiting is safe and guessing early is not.

Design the type from the pages, not from ideas. A property goes in because
several pages already carry that fact — a required property half the corpus
lacks makes half the corpus invalid. Then write its `instructions` properly:
where pages live, what resolves identity, what belongs in the body versus the
timeline.

## Changing it safely

- `schema_get` first, always. `schema_put` replaces the whole Schema, so build
  from the current one or you will silently drop what you did not know about.
- `schema_lint` before `schema_put`. It is free.
- `expected_hash` on `schema_put`, from `schema_get`'s `content_hash`.
- Needs `brain:manage` and Workspace Admin. Not an admin is a permission, not a
  failure — say which and stop.
- Describe the change in plain language and get a yes first. "Meetings become a
  real kind of note, and the seven you already have get picked up
  automatically" — not a JSON diff.
- `schema_revisions_list` and `schema_revisions_restore` undo it. Say so when
  proposing; reversible is much easier to agree to.

Removing a type is rare and rarely right. If the goal is "we don't use this any
more", leaving it alone costs nothing.
