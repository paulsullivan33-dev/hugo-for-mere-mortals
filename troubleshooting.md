# Troubleshooting

Symptom first, cause second, fix last —
and the checks that tell you you're
right. Most of these the lab met in
person; the transcripts are named where
they exist.

## The build says "found no layout file"

**Symptom:** warnings at build time,
and the affected pages missing from
`public/`.

**Cause:** a kind of page has no
template Hugo can find. A brand-new
site does this out of the box
(transcript t02) — it is a notice, not
a crash.

**Fix:** give the kind its template at
its current address (chapter 6's
table). If you believe you already
did, run `hugo --templateMetrics` and
see which templates actually ran —
belief is not evidence, and Hugo is an
honest witness.

## A tag page looks like the tags index

**Symptom:** `/tags/moon/` shows the
list of *all* tags; the term's own
notes are nowhere.

**Cause:** the term template isn't
being used. In the lab, `term.html`
sat in `layouts/_default/`, a pre-0.146
address the current template system
does not consult for the taxonomy/term
split — so the taxonomy template
rendered both kinds (transcript t90).

**Fix:** move the templates to the
`layouts/` root with the current
names — `taxonomy.html` for the list
of terms, `term.html` for one term —
and re-check with `--templateMetrics`:
you want `term.html` running once per
term. This is the signature injury of
following pre-2025 tutorials; if your
site predates 0.146 and tag pages look
wrong after an upgrade, start here.

## My new page isn't on the site

**Symptom:** the file exists, the build
passes, the page doesn't.

**Causes, in the order the lab would
check them:**

1. **It's a draft.** `hugo new` makes
   drafts on purpose. `hugo list
   drafts` will name it (t06); remove
   `draft: true` to publish, or preview
   with `hugo server --buildDrafts`
   (t07).
2. **It's dated in the future.** Future
   pages wait for their date. `hugo
   list future` names them too.
3. **It's the wrong bundle name.**
   `index.md` makes a leaf; `_index.md`
   makes a list (chapter 5). A page
   that *became* a list is filed under
   its folder's address, not its own.
4. **You're looking at the server, or
   the build, stale.** The server
   rebuilds on save; the build is a
   command you must re-run. When in
   doubt, `hugo` fresh and read the
   summary table — the page count moves
   when a page joins.

## The deployed site has no styles, and its links are wrong

**Symptom:** the site works locally and
falls apart at its real address —
unstyled pages, links leading nowhere,
a feed pointing at a stranger's domain.

**Cause:** `baseURL` (chapter 9). On
GitHub Pages project sites the address
includes the repository path
(`/repo-name/`), and a `baseURL` set
to the bare domain builds every
absolute address one level too
shallow; a `baseURL` still saying
`example.org` sends the RSS feed and
sitemap to a fictional place.

**Fix:** set `baseURL` to the address
the site *actually answers at*,
trailing slash and path included,
rebuild, redeploy. Check locally first:
the `<loc>` lines of
`public/sitemap.xml` should begin with
that address (t04 shows the healthy
shape).

## Sass fails: "you need the extended version" (or the stylesheet is empty)

**Symptom:** a build error mentioning
Sass or `css.Sass`, or a site whose
`main.css` never changes.

**Cause:** the Hugo doing the building
is the regular build. `hugo version` is
the witness — no `+extended`, no Sass
(chapter 3). On a deployed site, this
also bites when the workflow installs
plain Hugo while your machine has the
extended one: local green, remote red.

**Fix:** install the extended build in
both places; if your SCSS predates the
deprecation, expect the libsass
warning of chapter 10 and plan the
Dart Sass step rather than being
surprised by it.

## `hugo: command not found`

**Symptom:** the shell denies all
knowledge of Hugo, usually right after
installing it.

**Cause:** the binary isn't on the
`PATH`, or the shell hasn't been told
to look again. Not a Hugo problem —
the file is wherever you put it.

**Fix:** run it by its full path once
(`~/bin/hugo version`); if that works,
the directory needs adding to the
`PATH` in your shell's startup file.
The lab sidestepped the whole question
by calling `./bin/hugo` — a legitimate
arrangement for a tool used in one
place.

## The server shows a page the build doesn't (or the reverse)

**Symptom:** a page exists at
`localhost:1313` but not in `public/`
— or the opposite, after an afternoon
of edits.

**Cause:** the two runs have different
rules (chapter 2). The server may be
showing drafts (`--buildDrafts` left
on), serving from disk with its
livereload tag (a server-only artefact
the lab caught in its own output), or
simply ahead of a `public/` nobody
rebuilt.

**Fix:** decide which one is lying
about your intent. The build is the
court of appeal: `hugo` fresh, then
compare. Anything that only exists
under the server is a preview, not a
publication.
