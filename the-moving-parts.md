# The Moving Parts

A Hugo site has few parts, and each one
holds exactly one kind of thing. Learn
which part holds what, and every later
problem has an address.

## The binary

Hugo is **one program**. There is no
daemon to start, no database to keep
alive, no runtime to install first: the
file you download *is* the tool. It
comes in two builds:

- the **regular** build, which does
  everything in this guide except
  compile Sass stylesheets;
- the **extended** build, which adds
  the Sass compiler and a few asset
  tricks. Chapter 3 installs the
  extended one, and chapter 10 shows
  what it earns you.

Everything Hugo knows about your site it
learns by reading the project folder
when it runs. Delete the program and
your site is untouched; delete the
folder and there is nothing for any
program to rebuild. The folder is the
site.

## The project folders

`hugo new site` makes the skeleton
(transcript t01). The folders that
matter:

| Folder | Holds | Hugo's treatment |
| --- | --- | --- |
| `content/` | Your writing: Markdown files | Read, rendered through templates |
| `layouts/` | Templates: HTML with placeholders | Read; never copied to the output |
| `assets/` | Files the pipeline should process (Sass, images to resize) | Transformed, then published |
| `static/` | Files to publish as they are (a badge, a PDF) | Copied to the output untouched |
| `archetypes/` | Starter files for `hugo new` | Read when you create content |
| `data/` | Data files (YAML, JSON, TOML) templates can draw on | Read; not used by the lab |
| `themes/` | Downloaded themes live here | Read if the config names one |
| `public/` | **The output**: the finished website | Written by the build; safe to delete |

The `assets`/`static` distinction is the
one beginners blur, and it is simple:
if Hugo should *work on* the file —
compile it, shrink it, resize it — it
belongs in `assets/`. If Hugo should
*hand it over unchanged*, it belongs in
`static/`. Chapter 10 exercises both.

## The configuration file

One file, `hugo.toml` at the project's
root, holds the site's settings: its
title, its eventual web address, its
menus, and whatever facts about your
site your templates want to quote (the
lab's club keeps its meeting place
there, so the footer can print it).
Chapter 9 takes the lab's file line by
line. Hugo also accepts the same
settings as `hugo.yaml` or `hugo.json`;
the name of the game is one config
file, not three.

## The two runs

Hugo is used two ways, and confusing
them causes real bewilderment:

- **`hugo`** — the build. Writes the
  finished site into `public/` and
  stops. This is the run that counts;
  its output is what gets published.
- **`hugo server`** — the workshop.
  Builds the site in memory (or to
  disk, as the lab's log honestly
  showed), serves it on your machine —
  `http://localhost:1313/` by default —
  watches the project, and rebuilds on
  every save, with the browser
  refreshing itself. Drafts stay hidden
  here too unless you ask otherwise
  (chapters 5 and 12).

The server's conveniences are for the
author only. Nothing about it ships:
when the lab's server wrote a
`livereload` script tag into the pages
it served from disk, that tag existed
only in the server's copy — a plain
`hugo` build of the same project has no
such line. If a page looks right under
the server, the build is the court of
appeal, and it takes a tenth of a
second to consult.

## Where the truth lives

Three habits follow from the parts
above, and the rest of the guide leans
on them:

1. If a page is *missing*, look in
   `content/` and its front matter
   (chapter 5) — the build only makes
   pages from files it is allowed to
   publish.
2. If a page looks *wrong*, look in
   `layouts/` (chapter 6) — appearance
   is entirely the templates' doing.
3. If the *whole site* is wrong —
   wrong address in every link, wrong
   title everywhere — look in
   `hugo.toml` (chapter 9).
