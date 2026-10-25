# Recipes

Four small jobs, each done the way the
lab did them, with the transcript that
proves the moving parts. A recipe's
value is its checks: each one ends by
looking at the result.

## Start a new note the club way

```console
$ hugo new content notes/comet-watch.md
Content "/.../content/notes/comet-watch.md" created
```

The archetype (chapter 5) has already
filled in today's date and a title
guessed from the file name, and —
deliberately — marked the file a
draft, so a half-written note cannot
reach the site. Write the note, then
preview it as a member of the site:

```console
$ hugo server --buildDrafts
```

Check: the draft's address answers
`200`, and it appears in the notes list
among the published notes (transcript
t07). When it is ready, remove
`draft: true` from its front matter
and build as usual; the first ordinary
build is the one that publishes it.

## Check a site before it ships

Three questions, three commands, run
from the project root:

```console
$ hugo list drafts       # anything still hidden on purpose?
$ hugo list future       # anything dated ahead, waiting?
$ grep -o '<loc>[^<]*</loc>' public/sitemap.xml | head -3
```

Check: the drafts list contains only
what you *mean* to withhold; the
future list is empty, or holds only
what you meant to schedule; and the
sitemap's addresses start with the
site's real `baseURL` — not
`example.org`, which is the fingerprint
of a config nobody updated (chapter
9). The lab's own answers are in
transcripts t06 (lists) and t04
(sitemap). Ninety seconds, and the
three commonest publishing
embarrassments are all behind you.

## Tidy the tags

Tags rot quietly: synonyms creep in
("moon" beside "Moon"), one-offs pile
up. The terms list is the audit:

```console
$ hugo            # then read public/tags/index.html
```

— or simply open `/tags/` under
`hugo server`. Every term shows its
count (chapter 8). The fixes are front-
matter edits, and the counts are the
check that they took: rename a tag in
the notes that carry it, rebuild, and
watch the old term's page disappear
from the list while the new one's
count grows by exactly the number of
notes you touched. A term with a count
of one that will never grow is a
candidate for deletion — a tag that
names a single page organises nothing.

## Take the site somewhere on a stick

The whole project — content, templates,
config, and this guide's lab — is one
folder, and the built site is one
subfolder of it. To rehearse a move to
a new machine (the club's laptop dies;
the folder changes hands):

1. Copy the project folder.
2. Install Hugo there (chapter 3) —
   the *extended* build, at the version
   the site was written against.
3. Run `hugo` and compare the summary
   with the old machine's: same page
   count, same totals.

Check: the two builds' summary tables
agree (the lab's was 27 pages, one
processed image, one static file —
transcript t03). A static site has no
state beyond its folder, which makes
this recipe less a migration plan than
a description of an ordinary Tuesday —
and that is the advantage, stated
without embroidery.
