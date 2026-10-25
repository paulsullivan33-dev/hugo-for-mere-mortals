# Hugo for Mere Mortals

A website does not have to be a program
that runs. It can be a pile of finished
pages, written once and then simply
served, the way a noticeboard is served
by standing there. **Hugo** is the tool
that makes the pile: you write pages in
Markdown, describe how they should look
with templates, and Hugo — a single
program, no database, no runtime, no
plugins to speak of — turns the lot into
a complete website in a fraction of a
second. This guide explains how Hugo
works in those terms: how to install it,
how a site is organised, how the
templating language fits together, how
tags and menus and RSS feeds fall out of
the build, and how the finished site
gets published — with the limits stated
plainly, including one the lab walked
straight into.

The lab behind this guide ran the real
thing: **Hugo 0.168.0, the extended
build**, downloaded from the project's
own GitHub releases and checked against
its published SHA-256 sums before it was
run. With it the lab built a complete
small website — the Hilltop Astronomy
Club, a fictional club invented for the
purpose — from an empty folder: the
configuration written by hand, the
templates written by hand as a small
theme inside the project (no downloaded
theme), four pieces of content including
a page bundle carrying a photograph,
tags with their own pages, an RSS feed
and a sitemap inspected line by line, a
Sass stylesheet compiled by the extended
build, an image resized by Hugo itself,
and the whole site served over HTTP and
asked real questions with `curl`.

What the lab could not do, it did not
fake. The lab machine is a small Linux
sandbox with no screen and no public
address, so two things are taught from
the documentation and labelled as such
wherever they appear: **deploying to a
real host** (the build that deployment
runs was verified; the upload was not)
and **the features the lab never
exercised** — multilingual sites and
Hugo Modules among them. The lab also
earned one genuine scar: Hugo's template
system was overhauled in version 0.146,
and the lab's first set of templates,
laid out the way older tutorials teach,
silently rendered every tag page with
the wrong template. Chapter 6 tells that
story with the evidence kept, because
every reader following an older book
will meet the same wall. `criteria.md`
keeps the full ledger of what was run
and what was only read.

## What this guide covers

- [**What Hugo is**](what-hugo-is.md) —
  the mental model: a machine that turns
  a folder of text into a finished
  website; what "static" buys and what
  it costs; what Hugo is not (a content
  management system, a web framework, a
  host)
- [**The moving parts**](the-moving-parts.md) —
  the one binary, the project folders
  (`content`, `layouts`, `assets`,
  `static`, `archetypes`), the config
  file, and the two ways Hugo runs: the
  build and the server
- [**Installing Hugo**](installing-hugo.md) —
  the extended build and why it matters,
  the release download with its checksum
  checked, the package routes, and
  `hugo version` as the receipt
- [**Your first site**](your-first-site.md) —
  `hugo new site`, the honest warnings
  an empty site earns, a first page, a
  first template, and the build–serve
  loop you will live in
- [**Content and front matter**](content-and-front-matter.md) —
  sections, pages, the two kinds of
  bundle, the block of facts at the top
  of every file, drafts and future
  dates, and `hugo new` with archetypes
- [**Templates and layouts**](templates-and-layouts.md) —
  the template system as it stands since
  version 0.146: `baseof` and blocks, one
  template per kind of page, partials,
  and the tag-page trap, diagnosed from
  the lab's own transcripts
- [**Shortcodes**](shortcodes.md) —
  small templates called from inside
  your writing: the two the lab defined,
  when a shortcode is the right tool,
  and when it is a mess waiting to
  happen
- [**Taxonomies**](taxonomies.md) —
  tags end to end: the words in front
  matter, the list of all tags, one page
  per tag, a feed per tag, and adding a
  taxonomy of your own
- [**Configuration**](configuration.md) —
  `hugo.toml` taken line by line: the
  base URL and why it matters, your own
  parameters, menus built in config, and
  the settings the lab left alone on
  purpose
- [**Assets and images**](assets-and-images.md) —
  the pipeline: a Sass stylesheet
  compiled by the extended build (and
  its deprecation, faced honestly),
  images resized by Hugo, and the
  `static` folder's simpler bargain —
  files copied untouched
- [**Deploying to GitHub Pages**](deploying-to-github-pages.md) —
  what deployment actually is for a
  static site: one build command and a
  folder of files; the Actions pattern,
  described generically; custom domains
  and the base URL, again
- [**Recipes**](recipes.md) — starting a
  new note the club way, previewing
  drafts before the world sees them,
  checking a site before it ships, and
  tidying tags with `hugo list`
- [**The neighbours**](the-neighbours.md) —
  MkDocs, Jekyll, Eleventy, WordPress
  and a folder of hand-written HTML:
  what each one trades, and why "which
  generator" is a smaller question than
  it looks
- [**Limits**](limits.md) — no database
  and no dynamic anything, no built-in
  search or comments, a template system
  that changed under its users once and
  may again, stated plainly
- [**Troubleshooting**](troubleshooting.md) —
  the page that isn't there, the draft
  that hides, the tag page wearing the
  wrong clothes, broken links after
  publishing, and the traps this guide's
  lab fell into so you don't have to
- [**Glossary**](glossary.md) — the
  terms, collected in one place

## What it doesn't cover

Running the website once it exists —
hosting, servers, and keeping a machine
safe on the internet are subjects of
their own, and chapter 11 stops at
handing over the finished folder.
Themes written by other people get a
warning and a pointer, not a tour: this
guide teaches you to write your own
small one, because that is where the
understanding is. Multilingual sites,
Hugo Modules, and Hugo's deployment
targets beyond the pattern in chapter
11 are likewise pointed at, not taught —
the lab never ran them, and the guide
says so where they come up.

## How to use this guide

Read chapter 1 for the model and chapter
2 before installing anything — knowing
which folder holds what turns later
confusion into a named problem. Chapter
4 builds the first site in the same
sitting as the install; do it with the
commands actually typed, because Hugo
is learned by watching it answer.
Chapter 6 is the one not to skip even
if your first site seems to work: the
template rules changed in 2025, and a
site can be quietly wrong in exactly
the place chapter 6 dissects. The lab's
transcripts live in
`hugo-lab/transcripts/`, the lab's own
site — the worked example throughout —
is `hugo-lab/site/`, and its notes are
`examples/lab-notes.txt`.

---

## Part of the series

This guide is one of the [For Mere Mortals](https://paulsullivan33-dev.github.io/mere-mortals/) guides: plain-language guides to the tools programmers and makers use.

Related guides:

- [MkDocs for Mere Mortals](https://paulsullivan33-dev.github.io/mkdocs-for-mere-mortals/)
- [Markdown for Mere Mortals](https://paulsullivan33-dev.github.io/markdown-for-mere-mortals/)
- [GitHub Actions for Mere Mortals](https://paulsullivan33-dev.github.io/github-actions-for-mere-mortals/)

## License

The writing in this guide is licensed under [CC BY 4.0](https://github.com/paulsullivan33-dev/hugo-for-mere-mortals/blob/main/LICENSE). Code examples and lab scripts are licensed under the [MIT License](https://github.com/paulsullivan33-dev/hugo-for-mere-mortals/blob/main/LICENSE-CODE).
