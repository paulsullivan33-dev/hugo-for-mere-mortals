# Writing Criteria

Every guide in this repo is written to the same
standard. If you're adding or editing a guide —
human or AI — hold it to these.

1. **Plain words, real ideas.** Simple language,
   never dumbed-down concepts. Explain jargon on
   first use; collect terms in the glossary.
2. **No hype.** No marketing adjectives, no
   "revolutionary," no promises about what
   something will do for the reader.
3. **Honest about limits.** Say what the thing
   *can't* do. State uncertainty instead of
   smoothing it over. Validation notes include
   what remains unverified.
4. **No invented numbers.** Benchmarks, defaults,
   and specs are either measured or qualified with
   "depends on your setup." If it wasn't tested,
   say so.
5. **Checkable.** Commands are meant to be run,
   with "Check:" blocks showing what success looks
   like. Sources are linked, not asserted.
6. **Respect the reader's setup.** Call out
   Windows/Mac/Linux differences. Don't assume a
   GPU, a budget, or prior experience.
7. **Safety isn't skipped.** Real risks get
   stated plainly, not buried.
8. **Scoped.** Each guide says what it covers and
   points elsewhere for the rest. No guide
   pretends to be the whole subject.
9. **Structure over prose.** Tables, before/after
   examples, symptom → fix. Scannable beats essay.

## Verification notes for this guide

Built and verified 2026-10-24/25 against
**Hugo 0.168.0, extended build**
(`hugo v0.168.0-…+extended linux/amd64`,
built 2026-10-13), downloaded as the
official release tarball from the
project's GitHub releases and verified
against the project's published
checksums (transcript t00: SHA-256 of
`hugo_extended_0.168.0_linux-amd64.tar.gz`
answered `OK`), on a small Ubuntu Linux
sandbox. No Hugo was installed from any
package manager; the single binary ran
from a work folder.

**Primary sources read, not remembered:**
Hugo's official documentation for the
new template system (the v0.146.0
overhaul notes — `_default` removed,
`_partials`/`_shortcodes` renamed, the
taxonomy/term template split) and the
template lookup order; the project's
forum discussion confirming that a
`term.html` left in `_default/` is not
consulted for term pages; documentation
for front matter, bundles, taxonomies,
the asset pipeline and `css.Sass`
(including the libsass deprecation
notice the binary itself prints), and
GitHub Pages' Actions deployment
pattern (chapter 11, documented only).

**The fixture site.** The Hilltop
Astronomy Club: invented whole — club,
hall, members, and observing notes are
generic fixtures, modelled on no real
person, organisation, or event. Its
complete source is kept in
`hugo-lab/site/` (config, content,
hand-written layouts, archetype,
assets, statics); its one photograph is
a 640×400 PNG the lab generated. No
third-party theme was downloaded at any
point; every template in the lab was
written for the guide.

**Ran for real** (transcripts in
`hugo-lab/transcripts/`):

- t00 — the release download and its
  checksum verification (`OK`).
- t01 — extraction, `hugo version`
  (0.168.0 +extended), `hugo new site`,
  and the three-line default config it
  writes.
- t02 — a build attempted before any
  layouts exist: the "found no layout
  file" warnings for the home and
  taxonomy kinds, 4 pages counted, and
  an output folder holding only
  `index.xml`, `sitemap.xml` and the
  empty taxonomy folders.
- t02b — the finished site's source
  tree (24 files), as committed.
- t03 — the full build of the finished
  site: 27 pages, 1 non-page file, 1
  static file, 1 processed image,
  **Total in 379 ms**; the complete
  `public/` file listing.
- t04 — output inspection: all 15
  sitemap addresses on the configured
  baseURL; the RSS feed's channel and
  first item; the `skynote` shortcode's
  `<aside>` present in a built note;
  the `meetup` shortcode's sentence on
  the home page; the bundle image
  published at 640×400 beside Hugo's
  300×188 resized copy; the compiled
  stylesheet with `$sky` resolved to
  `#16264a` throughout and zero `$`
  characters remaining.
- t05 — `hugo server` answering over
  HTTP: `/`, `/notes/`, a note, `/tags/`,
  a term page, `/about/` and the
  compiled CSS all `200`; an invented
  address `404`; the home page's real
  `<title>`. (One grep in this pass
  returned nothing because the pattern
  omitted the `</a>` between a term's
  name and its count — the page was
  right, the pattern was wrong; the
  correction is appended to the
  transcript and the counts were
  verified against the built files:
  moon 2, observing 2, five terms at 1.)
- t06 — the stock archetype's contents;
  `hugo new content notes/comet-watch.md`
  creating a file born `draft: true`
  with a guessed title; `hugo list all`
  (7 rows) and `hugo list drafts`
  (exactly the new note).
- t07 — `hugo server --buildDrafts`:
  the draft note answers `200` and
  appears in the notes list while the
  plain build still excludes it.
- t90 — the template-system trap,
  diagnosed and fixed for real: with
  templates in the pre-0.146
  `layouts/_default/`, `--templateMetrics`
  showed `taxonomy.html` rendering all
  8 taxonomy-kind pages and `term.html`
  never running; the term page's HTML
  showed the wrong template's body.
  After moving to the current layout
  (`layouts/` root, `term.html`,
  `taxonomy.html`, `_partials`,
  `_shortcodes`), metrics showed
  `term.html` ×7 and `taxonomy.html` ×1,
  and `/tags/moon/` listed both its
  notes. Rebuild time 88 ms.

**Two deprecations met and kept:** an
early template used `.Site.LanguageCode`,
which Hugo warns is deprecated since
v0.158.0 in favour of
`.Site.Language.Locale` — fixed, and
the warning's disappearance verified by
the rebuild in t04. And every build of
the finished site warns that `css.Sass`
(libsass) was deprecated in v0.153.0
and will be removed in favour of Dart
Sass; the lab kept the warning in its
transcripts and chapter 10 explains
what it means rather than hiding it.

**Documented only, and labelled as such
in the chapters:** deploying to GitHub
Pages or anywhere else (the build that
deployment runs was verified end to
end; no upload was performed — the lab
machine has no public address);
custom domains and HTTPS arrangement;
multilingual sites; Hugo Modules;
themes written by third parties and
the theme ecosystem; Hugo's built-in
shortcodes beyond naming them;
pagination of long lists; the asset
pipeline's minify/fingerprint steps
(the pipeline itself was exercised
through Sass and image resizing);
`hugo deploy`; Windows and macOS
installs beyond naming their routes.
The `hugo server` checks ran against
the lab machine's own loopback
interface, which is the server's
intended use.
