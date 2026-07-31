# Writing to the Brain

## Capture, and what shape to capture it in

Capture anything that might be useful later. The bar is low on purpose — the
cost of a fact you never need again is nearly nothing, and the cost of one you
needed and did not keep is the whole point of having a Brain.

The real judgement is not _whether_ to capture but _where_ it goes:

- **A whole subject gets its own page.** A person, an organisation, a decision,
  a meeting, a project — anything you would expect to accumulate more about
  later, and anything you would want to link to from elsewhere.
- **Everything smaller becomes a line on a page that already exists.** A detail
  about someone, how a decision turned out, what came of a commitment. Borderline
  usually means a line in an existing page, not a new page.

When you genuinely cannot tell — whether it is worth keeping at all, or which
page it belongs on — ask. One short question costs less than a wrong page, and
the user knows things about what matters to them that you cannot infer.

## The sequence

1. `query` for the subject. You are looking for a page to extend.
2. Pick the type. `schema_get` lists what this Brain knows; invent the word if
   none fits.
3. `schema_type_get <type>` and follow its `instructions` exactly — per Brain,
   changing, and they beat anything here. Skip this and you will file a person
   by name in a Brain that resolves on email.
4. Draft it as prose. Not bullet soup.
5. `pages_lint` if unsure of the shape — it validates without storing.
6. `pages_put`.

## Types

Use the Brain's type if one fits. If none does, **still write your own word for
it**: `type: meeting`, `type: decision`, `type: jtbd`. The page stores under the
fallback type and keeps your word as its Suggested Type, which is the only
record of what it was meant to be and the raw material the Schema grows from.

The `unknown_page_type` warning that comes back means exactly that worked. It is
a receipt. It wants no action, and no explanation to the user beyond describing
the page as filed with a label on it.

When you update a page that already carries a Suggested Type, carry it through
unchanged.

## Shape of a page

Frontmatter: `title`, `type` (your word), plus `date` when it happened at a
moment and `source` when it came from somewhere specific.

Ref: a plural folder and a descriptive slug, date-prefixed for events —
`meetings/2026-07-27-pricing-review`, `decisions/per-seat-pricing`. Lowercase
ASCII with hyphens; fold ä→ae, ö→oe, ü→ue, ß→ss, since non-ASCII refs are
rejected.

Body: prose someone would want to read, opening with what this is and when.
Headings once it runs long.

Links: `[[people/dana-reyes]]` for every person and organisation the page is
really about. Backlinks are what turn an entity page into a history nobody
maintained by hand. A page with no links is an orphan.

## Updating

`pages_get` for the current markdown and its `hash`, edit, then `pages_put` with
that hash as `expected_hash`. Without it you overwrite blind and can discard
someone else's edit. On a mismatch, re-read and reapply — never retry with the
stale hash.

When what you learned is that something _happened_, add a dated line to the
timeline rather than rewriting the body. Bodies hold what stays true.

**Never recompute a ref.** When someone changes their name or an organisation
rebrands, update the title and leave the ref alone — a moved ref breaks every
link pointing at it. Moving one is a deliberate `pages_move`.

## Afterwards

Name the page and where it went, in one sentence. If it failed, say so and pass
the error's own remediation through — never describe an intention as an outcome.
