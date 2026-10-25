# Taxonomies

A **taxonomy** is a controlled
vocabulary for sorting your own site:
a set of words, assigned to pages, that
Hugo then turns into an index of its
own — a page listing every word, a page
per word listing its pages, and a feed
per word for anyone who follows just
that thread. **Tags** are the taxonomy
everybody meets first, and the only one
the lab exercised end to end. It is
enough to learn the whole mechanism,
because every taxonomy works this way.

## The words go in front matter

Nothing is registered or declared per
page. A note simply carries its words:

```yaml
tags: ['beginners', 'binoculars', 'moon']
```

Four notes in the lab produced seven
tags between them. From those lines
alone, the build made fifteen files
under `public/tags/` (transcript t03):
the terms list, seven term pages, and
seven term feeds. Hugo's default
configuration already defines two
taxonomies — `tags` and `categories` —
which is why even the empty site in
chapter 4 had a `tags/` folder waiting.
You can switch one off or rename the
address it lives at in the config
(chapter 9 shows the lab's explicit
entry); the mechanism doesn't change.

## The three things Hugo makes

**The terms list** — `/tags/` — is
rendered by `layouts/taxonomy.html`,
where `.Data.Terms` offers each term
with its count. The lab's template
turns it into the club's index:

```html
{{ range .Data.Terms.Alphabetical }}
<li><a href="{{ .Page.RelPermalink }}">{{ .Page.LinkTitle | lower }}</a> ({{ .Count }} {{ if eq .Count 1 }}note{{ else }}notes{{ end }})</li>
{{ end }}
```

which built (transcript t04/t05, with
the counts checked against the files):

```
beginners (1 note)    moon (2 notes)
binoculars (1 note)   observing (2 notes)
maintenance (1 note)  planets (1 note)
telescopes (1 note)
```

**One page per term** — `/tags/moon/` —
is rendered by `layouts/term.html`,
whose `.Pages` are the notes carrying
that word, and `.Data.Term` is the word
itself. The lab's page:

```
Notes tagged "moon"
  Moonwatch evening: ... — 10 October 2026
  First light: the Moon ... — 3 October 2026
```

That this page exists at all is the
subject of chapter 6's cautionary tale:
under the pre-0.146 layout the term
template was silently never used, and
term pages wore the taxonomy template
instead. If your tag pages look like
the index, that chapter is your fix.

**A feed per term** — `/tags/moon/
index.xml` — falls out of Hugo's
built-in RSS output, no template of
yours involved. Anyone who cares about
the club's Moon notes and nothing else
can subscribe to exactly those.

## Tags turn up in the byline, too

A taxonomy's other half is displaying
the words *on* the page they describe.
The lab's `post-meta` partial does it
with `.GetTerms`, which returns the
page's terms as links rather than bare
strings:

```html
{{ with .GetTerms "tags" }}
· tagged
{{ range $i, $t := . }}{{ if $i }}, {{ end }}<a href="{{ $t.RelPermalink }}">{{ $t.LinkTitle | lower }}</a>{{ end }}
{{ end }}
```

Because the same partial serves the
single page and the section list, every
note's byline — on its own page and in
the `/notes/` index — links each tag to
its term page. One definition, no
drift: change how tags are shown in
one file and the whole site agrees.

## A taxonomy of your own

Tags are a default, not a limit. A
site that wanted *telescopes* as a
first-class sort — this club's notes
reviewed by instrument — would declare
it in config:

```toml
[taxonomies]
  tag = 'tags'
  instrument = 'instruments'
```

and then write `instruments: ['8-inch
Dobsonian']` in front matter. Hugo
would build `/instruments/` on the same
machinery, with the same two templates
unless you give the new taxonomy its
own. The lab did not build this — it is
described from the documentation, and
chapter 9 shows the config entry the
lab *did* run. One honest caution, from
the lab's small numbers: a taxonomy
earns its keep when several pages share
each term. Seven tags over four notes
is already near the frivolous edge; had
every tag named exactly one note, the
index would be a list of singletons
telling the reader nothing the notes
list doesn't.
