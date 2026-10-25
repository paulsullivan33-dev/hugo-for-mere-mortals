# Glossary

**Archetype** — a starter file for new
content. `hugo new` copies it, fills in
the date and a guessed title, and
leaves you a draft (chapter 5).

**Asset pipeline** — Hugo's machinery
for processing files at build time:
compiling Sass, resizing images,
minifying, fingerprinting. Fed from
`assets/`, it writes the results into
the output (chapter 10).

**baseof** — the base template: the
page frame (`<head>`, header, footer)
that every other template plugs its
middle into, via `{{ block "main" }}`
(chapter 6).

**baseURL** — the configuration setting
naming the address the site will live
at. Baked into sitemaps, feeds, and
absolute links (chapter 9).

**Branch bundle** — a folder whose
`_index.md` makes it a list page: the
home page, a section page (chapter 5).

**Build** — the plain `hugo` run: the
whole site, written to `public/`, then
the program stops (chapter 2).

**Content** — the writing: Markdown
files in `content/`, one per page
(chapter 5).

**Draft** — a page whose front matter
says `draft: true`; built only when
you ask (`--buildDrafts`), never by
default.

**Extended build** — the Hugo binary
with the Sass compiler and extra asset
features aboard; its version string
says `+extended` (chapter 3).

**Front matter** — the block of facts
at the top of a content file: title,
date, tags, draft, and anything else
your templates want to know (chapter
5).

**Kind** — Hugo's classification of a
page: home, page, section, taxonomy,
term, and a few more. Each kind has
its template (chapter 6).

**Leaf bundle** — a folder whose
`index.md` makes it a single page,
owning the other files in the folder —
its photographs, above all (chapter
5).

**Locale** — the config setting naming
the site's language and region
(`en-gb`); steers dates and built-in
words. Older guides call it
`languageCode`.

**Partial** — a reusable template
fragment, included with
`{{ partial "name.html" . }}` from
`layouts/_partials/` (chapter 6).

**public/** — the output folder: the
finished website, and the only thing
deployment ships (chapters 2, 11).

**Regular page** — an ordinary content
page, as opposed to a list page; what
`.Site.RegularPages` collects.

**Resource (page resource)** — a file
belonging to a bundle page, findable
from its template with `.Resources`
(chapter 10).

**Section** — a top-level folder of
`content/`, which gets a list page of
its own and gives its pages their
address prefix (chapter 5).

**Shortcode** — a named template
called from inside the writing, like
`{{< skynote >}}`; Hugo's way of
putting rich or repeated HTML into
Markdown (chapter 7).

**Static site** — a website built in
advance into finished files, served
as they sit; no program runs when a
visitor arrives (chapter 1).

**Taxonomy** — a controlled vocabulary
for sorting a site: terms assigned in
front matter, turned by Hugo into a
terms list, a page per term, and a
feed per term (chapter 8).

**Term** — one word in a taxonomy
("moon" among the tags), and also the
name of the page listing everything
carrying that word.

**Template metrics** — the report from
`hugo --templateMetrics`: which
templates ran, how often, how long.
The first witness to call when a page
renders wrong (chapters 6, 15).
