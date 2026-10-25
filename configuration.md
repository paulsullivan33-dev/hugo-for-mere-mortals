# Configuration

One file — `hugo.toml`, in the project
root — holds the facts that belong to
the whole site rather than to any page.
This chapter takes the lab's file
exactly as built and reads it top to
bottom; it is short, because the lab
kept it short on purpose, and that is
the first lesson.

```toml
baseURL = 'https://hilltop-astronomy.example.org/'
locale = 'en-gb'
title = 'Hilltop Astronomy Club'

[taxonomies]
  tag = 'tags'

[params]
  strapline = 'A friendly club for looking up'
  meetingPlace = 'The Old School Hall, Church Lane'
  meetingNight = 'the first clear Friday of the month'

[[menu.main]]
  name = 'Home'
  url = '/'
  weight = 1
# (... three more menu entries)
```

## The three lines that matter most

**`baseURL`** is the address the site
*will* live at, and Hugo builds it into
everything absolute: the sitemap's
addresses, the RSS feed's links, the
canonical URLs. The lab's build shows
the fingerprints (transcript t04) —
every `<loc>` in `sitemap.xml` begins
with it. Two consequences:

- While you are still building, the
  default `https://example.org/` is
  harmless: pages are written with
  relative links, and the site browses
  fine. The address only becomes load-
  bearing when the site ships (chapter
  11) — but a feed or sitemap shipped
  with the placeholder in it is broken
  in a way visitors *will* meet, so
  setting it is on the pre-flight list
  in chapter 12.
- `hugo server` overrides it locally,
  which is why the lab's server answered
  at `localhost:1313` while the built
  files kept the real address.

**`title`** is the site's name, quoted
by the header partial on every page and
by the feed. **`locale`** tells Hugo
the language and region (`en-gb` here),
which steers dates and the built-in
vocabulary; older guides call this
`languageCode` — the same fact, a
renamed key.

## [taxonomies]: saying the quiet part

The lab's entry declares only what
Hugo would have assumed anyway:

```toml
[taxonomies]
  tag = 'tags'
```

Read it as: *the taxonomy whose front-
matter key is `tag` lives at the
address `/tags/`*. Stating it costs two
lines and buys two things — the next
reader learns the mechanism is
configurable from the file itself, and
adding a second taxonomy later
(chapter 8) is an edit, not a mystery.
Deleting the `categories` default
every Hugo site is born with is the
same table's other household chore:
leave the key out and the taxonomy is
gone. (The empty `categories/` folder
in chapter 4's first build is the
default, caught in the act.)

## [params]: your own facts

Anything under `[params]` is yours.
Templates read them as `.Site.Params.
meetingPlace` and friends; the lab
keeps the club's strapline and meeting
details there so the header, the
footer, and the `meetup` shortcode all
quote one source. The discipline is the
feature: facts that appear in several
places belong in config *once*, and a
change of hall becomes a one-line edit
instead of a search through every page.

## [[menu.main]]: the navigation, declared

Menus can be assembled three ways —
from config, from front matter, or
automatically from sections. The lab
declares its four entries in config,
each a name, an address, and a
`weight` for ordering:

```toml
[[menu.main]]
  name = 'Observing Notes'
  url = '/notes/'
  weight = 2
```

The header partial then simply walks
`.Site.Menus.main` in weight order.
What you gain over writing the links
into the header by hand is the same as
with params: one list, everywhere
consistent, editable without touching a
template. Sites whose navigation should
*mirror* their sections often generate
menus from front matter instead (`menu`
and `weight` per page); the lab's site
is small enough that the declared list
is the honest choice, and the guide
says which it picked rather than
pretending the choice doesn't exist.

## What the lab left alone

Hugo's configuration surface is much
larger than this file — output formats,
image-processing defaults, build
caches, per-environment overrides (a
`config/production/` folder beside the
main file, for settings that should
differ when the site ships). The lab
changed none of it, and the guide
inventories rather than teaches it for
one reason worth keeping: **every line
of config is a decision the next reader
must reverse-engineer.** A small site
with a small config can be understood
in one reading, which — for a club
website maintained by whoever holds the
folder this year — is worth more than
any individual setting.
