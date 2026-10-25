# Your First Site

This chapter makes a site the way the
lab made its: from an empty folder, in
the open, including the part where the
first build has almost nothing to show.
The lab's site is the **Hilltop
Astronomy Club** — a fictional club with
a hall, a flask shortage, and opinions
about the Moon. Its finished source is
kept at `hugo-lab/site/` in this repo,
and every step below is a transcript.

## The skeleton

```console
$ hugo new site hilltop
Congratulations! Your new Hugo project was created in ...
```

Check: a folder appears holding less
than you might expect (transcript t01):
a `hugo.toml`, an `archetypes/` folder,
and empty directories Hugo doesn't
bother to list because they hold
nothing. The default config is three
lines:

```toml
baseURL = 'https://example.org/'
locale = 'en-us'
title = 'My New Hugo Project'
```

That is all a Hugo site *is*, at birth.
Everything else — pages, looks, menus —
is added by you, which is precisely why
this guide adds them one at a time.

## The honest first build

Run the build now, before adding
anything:

```console
$ hugo
WARN  found no layout file for "html" for kind "taxonomy": ...
WARN  found no layout file for "html" for kind "home": ...
 Pages            │  4
Total in 103 ms
$ ls public/
categories  index.xml  sitemap.xml  tags
```

(transcript t02 keeps the whole run.)

Read that result carefully, because it
teaches the model better than any
diagram:

- Hugo found **4 pages** to make — the
  home page, the two default taxonomy
  lists (`tags`, `categories`), and
  their feeds — even with no content at
  all.
- With **no templates**, it could render
  none of the HTML. It said so, twice,
  in warnings worth reading rather than
  fearing: *found no layout file*.
- What it *could* make without
  templates, it made: an RSS feed
  (`index.xml`) and a `sitemap.xml`.
  Those come from machinery inside Hugo,
  not from your layouts.

A new site is not broken when it does
this. It is waiting for the two things
only you can supply: something to say,
and a decision about how it looks.

## Something to say

Content is a Markdown file in
`content/` (chapter 5 gives it the full
treatment). The home page's own content
lives in a file with a special name,
`content/_index.md`:

```markdown
---
title: 'Welcome to the Hilltop Astronomy Club'
---

We are a small club of people who like
looking at the night sky.
```

The block between the `---` lines is
**front matter** — facts about the page,
for the templates to use. The rest is
the writing.

## A first template

One file gives the home page a shape.
Since version 0.146 the home page's
template is `layouts/home.html`, at the
top of `layouts/` (chapter 6 explains
the system, and why the address
matters):

```html
{{ define "main" }}
<h1>{{ .Title }}</h1>
{{ .Content }}
{{ end }}
```

Two ideas hide in those four lines, and
both recur everywhere:

- `{{ .Title }}` and `{{ .Content }}`
  are the page's own facts, dropped into
  the HTML. Templates are HTML with
  holes, and the holes are filled from
  the page being built.
- The `{{ define "main" }}` wrapper
  means *this is the middle of the
  page*; a shared outer frame — the
  `baseof.html` of chapter 6 — supplies
  the head, the header, and the footer
  around it, so no page repeats them.

## The loop

With content and a template present,
the two runs from chapter 2 become your
whole working life:

```console
$ hugo            # build into public/
$ hugo server     # ...or serve it and watch
Web Server is available at http://localhost:1313/
```

Open the address, and there is the site:
your title, your words, the club badge,
the menu. Edit a content file, save, and
the served page rebuilds itself before
you can switch windows. The lab served
its finished site and interrogated it
with `curl` (transcript t05): every real
page answered `200`, and a made-up
address answered `404` with the lab's
own not-found page — small checks, but
they are the difference between *it
built* and *it works*.

From here the chapters stop walking in
a line. Content gets its own chapter
(5), templates theirs (6), and the
site grows the way real sites do: a
piece at a time, each piece checkable.
