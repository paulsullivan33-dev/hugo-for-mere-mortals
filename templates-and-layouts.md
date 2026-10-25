# Templates and Layouts

Templates decide what every page looks
like. Hugo's templating is a language —
Go's `html/template`, with Hugo's own
functions added — but a small site needs
only a handful of its ideas, and this
chapter teaches exactly those, in the
order the lab met them. It also tells
the story of the lab's one real failure,
because the failure *is* the current
state of Hugo templating, and meeting it
in print beats meeting it alone.

## The system as it stands (since 0.146)

In April 2025, Hugo 0.146 replaced its
template system wholesale. The new rules
are simpler than the old — one template
name per kind of page — but they are
*different*, and the internet is full of
the old ones. Commit these to memory
before borrowing any example:

| Kind of page | Template |
| --- | --- |
| Home | `layouts/home.html` |
| A single page | `layouts/page.html` (older name `single.html` still works as a fallback) |
| A section list | `layouts/section.html`, else `layouts/list.html` |
| A taxonomy's list of terms (`/tags/`) | `layouts/taxonomy.html` |
| One term's page (`/tags/moon/`) | `layouts/term.html` |
| Not found | `layouts/404.html` |
| The frame around all of them | `layouts/baseof.html` |

And the two supporting folders, renamed
in the same release:

- reusable fragments go in
  `layouts/_partials/`;
- shortcodes (chapter 7) go in
  `layouts/_shortcodes/`.

The old arrangement — everything under
`layouts/_default/`, fragments in plain
`partials/` — still *mostly* works in
current Hugo, kept alive as a fallback
for older themes. "Mostly" is doing
heavy work in that sentence, as the
next section shows.

## The lab's trap, with the evidence

The lab wrote its first templates the
old way, in `_default/`, following the
shape of countless tutorials — and
almost everything worked. Home, pages,
lists, partials, shortcodes: all
rendered. Only later, inspecting the
output, did the lab look at a tag page
and find it wearing the wrong clothes:
`/tags/moon/` was rendered by the
*taxonomy* template (the list of all
tags, with the tag's own notes nowhere
to be seen), and the lab's `term.html`
had never run at all.

The receipts are transcript t90. Hugo's
own `--templateMetrics` flag — which
reports which templates ran, and how
often — showed `_default/taxonomy.html`
running 8 times (one terms list, seven
term pages) and no `term.html` anywhere.
Under the current rules the verdict is
plain: the underscore-folder fallback
does not carry the taxonomy/term split.
The two are separate kinds now, and a
`term.html` in `_default/` is not found
for either of them.

The fix took a minute and is the layout
this guide teaches: move the templates
to the `layouts/` root with the current
names, `_partials/` and `_shortcodes/`
for the fragments. Rebuilt, the metrics
showed `term.html` running 7 times and
`taxonomy.html` once, and `/tags/moon/`
listed its two notes under the heading
*Notes tagged "moon"*. Three lessons,
in order of importance:

1. **Inspect output, not vibes.** The
   site built without errors while a
   whole kind of page was wrong. The
   build succeeding is necessary, not
   sufficient — look at the pages.
2. **`hugo --templateMetrics` answers
   "which template made this page?"**
   When a page looks wrong, that is the
   first question, and this is its tool.
3. **Date every tutorial.** Hugo
   examples from before 0.146 teach a
   layout system that has been
   replaced. The older the example, the
   more carefully its file addresses
   should be checked against the table
   above.

## baseof: the frame, once

Every page shares a skeleton: the
`<head>`, the header, the footer. That
skeleton lives once, in
`layouts/baseof.html`, with a hole in
the middle:

```html
<body>
  {{ partial "header.html" . }}
  <main>
    {{ block "main" . }}{{ end }}
  </main>
  {{ partial "footer.html" . }}
</body>
```

Each kind's template then supplies only
its middle, wrapped in
`{{ define "main" }} … {{ end }}` — you
saw the shape in chapter 4. Change the
frame and every page changes; that is
the entire point of having one.

## Partials: fragments with names

A **partial** is a template fragment
other templates include:
`{{ partial "post-meta.html" . }}`. The
trailing dot hands the fragment the
current page, so it can print the page's
date and tags. The lab's `post-meta`
partial is used by both the single-page
template and the list template — write
the byline once, fix it once. Partials
are also how a hand-rolled theme stays
readable: when a template grows a lump
that has a name ("that's the post
byline"), the lump becomes a partial.

## What a template can reach

Inside a template, the dot (`.`) is the
page being built. The vocabulary the
lab actually used fits on an index
card:

- `.Title`, `.Content`, `.Date`,
  `.Summary` — the page's facts, from
  chapter 5's front matter and text.
- `.Pages`, `.Data.Terms` — a list
  page's contents; chapter 8 lives on
  these.
- `.Site.Title`, `.Site.Params.…`,
  `.Site.Menus.main` — the whole site's
  facts, from `hugo.toml` (chapter 9).
- `range` — do this for each item;
  `with` — do this if it's there;
  `first 3` — take the first three.
  Control flow wears the same `{{ }}`
  as everything else.
- Functions like `.Date.Format
  "2006-01-02"` — Hugo leans on Go's
  conventions, including its eccentric
  reference-date formatting, which is
  documented wherever dates appear and
  strange exactly once.

The home template shows most of it in
nine lines — the newest three notes,
found by asking the site for its
regular pages in the `notes` section:

```html
{{ range first 3 (where .Site.RegularPages "Section" "notes").ByDate.Reverse }}
<li><a href="{{ .RelPermalink }}">{{ .Title }}</a> — {{ .Date.Format "2 January 2006" }}</li>
{{ end }}
```

That is the honest size of Hugo
templating for a mortal site: an
afternoon to learn, a reference page
kept open for the function names, and —
since 0.146 — a firm habit of checking
which file a kind of page actually
reads.
