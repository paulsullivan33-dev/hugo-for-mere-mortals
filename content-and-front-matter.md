# Content and Front Matter

Everything a visitor reads starts as a
Markdown file in `content/`. This
chapter covers how those files are
organised, the facts pinned to the top
of each one, and the files Hugo treats
as special — because organisation here
*is* the site's structure: the folders
you make are the addresses you get.

## Sections: folders with meaning

A folder directly under `content/` is a
**section**, and it gets a page of its
own that lists its contents. The lab's
site has one section, `notes/` — the
club's observing notes:

```
content/
  _index.md                 the home page
  about.md                  a single page
  notes/
    first-light-binoculars.md
    moonwatch-evening.md
    jupiter-at-opposition.md
    telescope-cleaning/
      index.md
      mirror.png
```

The build turns that into (transcript
t03): a list page at `/notes/`, and one
page per note at `/notes/<name>/`. A
file outside any section, like
`about.md`, is a page of the whole site
and lands at `/about/`. No configuration
made any of that happen; the tree *is*
the configuration.

## Front matter: the facts at the top

Every content file opens with a block
of facts between markers:

```markdown
---
title: 'First light: the Moon through borrowed binoculars'
date: 2026-10-03
tags: ['beginners', 'binoculars', 'moon']
---
```

Hugo's own vocabulary for the common
fields:

| Field | Meaning |
| --- | --- |
| `title` | The page's name, for templates and feeds |
| `date` | When it's from; sorts lists and fills the RSS feed |
| `draft` | `true` hides the page from builds (below) |
| `tags` | Words for the taxonomy (chapter 8) |
| `description` | A summary, if you don't want Hugo's automatic one |
| `slug` | Overrides the last piece of the address |
| `weight` | A nudge for ordering within a list |

Front matter can be written in TOML
(between `+++`), YAML (between `---`),
or JSON. The lab used YAML for content
and TOML for the config; pick one per
project and be consistent, because a
file with the wrong fences fails in ways
that read like riddles. Anything you
invent beyond the standard fields is
yours: templates can read custom fields
through `.Params`, which is how sites
grow *author*, *venue*, or *telescope*
without Hugo's permission.

Two fields deserve their reputation
known early:

- **Summaries.** List pages show each
  page's `.Summary` — Hugo takes the
  first stretch of the text (70 words by
  default) or everything before a
  `<!--more-->` marker if you place one.
  The lab's lists show these summaries;
  they are why a note's opening
  paragraph does double duty.
- **Dates in the future.** A page dated
  tomorrow is not published today. Not
  a bug — a scheduling feature — but it
  is also the classic "my page is
  missing" scare, and chapter 15 lists
  it among the usual suspects.

## The two bundles

A single Markdown file is a **page**.
Hugo also lets a page be a folder, in
two flavours whose names differ by one
underscore and whose behaviour differs
by more:

- **Leaf bundle** — a folder with an
  `index.md` in it. The folder is *one
  page*, and any other files in it are
  that page's own belongings: its
  pictures, its downloads. The lab's
  `telescope-cleaning/` note is one;
  its `mirror.png` belongs to the page,
  is published beside it, and — chapter
  10 — can be resized by the page's
  template because Hugo knows the two
  belong together.
- **Branch bundle** — a folder with an
  `_index.md` in it. The folder is a
  *list* page — the home page, a
  section page — and the file gives that
  list a title and some words of its
  own. The site's home page is a branch
  bundle of the root.

The underscore is the whole distinction,
which is either elegant or a trap
depending on your afternoon. If a page
publishes as a list when you wanted a
leaf, check which of the two names you
typed.

## Drafts: written, not published

Set `draft: true` and the page exists
for you but not for visitors: the build
skips it, the server skips it. Drafts
are how a note can live in the project
half-written. `hugo list` is the
inventory that keeps them honest:

```console
$ hugo list drafts
path,...,draft,...
content/notes/comet-watch.md,...,true,...
```

(transcript t06.) To *look* at a draft
as a page, preview it deliberately —
`hugo server --buildDrafts` adds drafts
to the served site (transcript t07:
the draft note answers `200` and joins
the notes list) while the plain build
still excludes it. Publishing day for a
draft is a one-word edit: `draft:
false`, or deleting the line.

## Archetypes: the starter file

Nobody should type the same front
matter skeleton daily. An **archetype**
is a template for new content files,
and `hugo new` stamps one out:

```console
$ hugo new content notes/comet-watch.md
Content "/.../content/notes/comet-watch.md" created
$ cat content/notes/comet-watch.md
+++
date = '2026-10-25T02:18:53Z'
draft = true
title = 'Comet Watch'
+++
```

Two kindnesses to notice: the title is
guessed from the file name, and the new
file is born a **draft** — a fresh page
cannot leak onto the site half-written
by accident. The skeleton it used is
`archetypes/default.md`, a file in your
project that you own outright. A project
with several kinds of content keeps
several archetypes (the archetype is
chosen by the section you are writing
into, when one exists with that name)
— the lab kept the default, and chapter
12 shows it earning its keep.
