# Shortcodes

Markdown is good at paragraphs and poor
at everything else. A **shortcode** is
Hugo's answer: a small template with a
name, called from inside your writing
with a line like `{{< skynote >}}`, and
replaced in the built page by whatever
the template produces. It is how a
Markdown file gains a callout box, an
embedded video, a figure with a caption
— any lump of HTML too rich or too
repeated for prose.

## The two the lab defined

Shortcodes you define live in
`layouts/_shortcodes/`, one file per
name. The lab's site has two, and they
show the two shapes shortcodes take.

**With an inside.** `skynote` wraps a
passage in a styled box — an aside for
"worth knowing, not the main thread":

```
{{</* skynote */>}}
Next time we will try the same view with
the club's 15x70 pair and compare notes.
{{</* /skynote */>}}
```

Its template is three lines; `.Inner`
is the wrapped text:

```html
<aside class="skynote">
  <strong>Sky note:</strong> {{ .Inner | markdownify }}
</aside>
```

The built page (transcript t04) carries
the `<aside class="skynote">` in place
of the call. The `| markdownify` matters:
writing inside a shortcode is still
Markdown, and the pipe is what turns it
into HTML rather than leaving asterisks
lying around.

**Standing alone.** `meetup` takes no
inside and no arguments; it prints a
fact the site keeps in one place:

```
{{</* meetup */>}}
```

```html
<div class="meetup">
  <p><strong>Next meeting:</strong> {{ .Site.Params.meetingNight }},
  at {{ .Site.Params.meetingPlace }}. ...</p>
</div>
```

The home page's call became *"Next
meeting: the first clear Friday of the
month, at The Old School Hall, Church
Lane."* — words assembled from
`hugo.toml` (chapter 9), so when the
club changes halls, one line of config
updates every page that carries the box.
That is the honest reason for a
parameterless shortcode: not cleverness,
but a single source of truth with a
short name.

## Arguments

A shortcode can take values, named or
positional — `{{< figure src="moon.png"
caption="The October Moon" >}}` is the
shape, read inside the template as
`.Get "caption"`. Hugo ships a shelf of
built-in shortcodes (for embedding
videos, posts, and the like); the lab
used none of them, and this guide
doesn't pretend otherwise. Define your
own when the lump is *yours*; reach for
the built-ins by their documentation
when it isn't.

## Care and feeding

Shortcodes are the sharpest tool in
the content drawer, and they cut in two
directions worth knowing before the
collection grows:

- **They are invisible in plain
  Markdown.** A note full of shortcodes
  still reads fine in an editor, but it
  only *renders* through Hugo. Move the
  file to another system and the calls
  come along as litter. For content you
  may someday take elsewhere, keep
  shortcodes few and meaningful.
- **They fail at build time, loudly.**
  A misspelled shortcode name stops the
  build with the file and line named —
  the good kind of failure. A shortcode
  that *exists* but misbehaves produces
  wrong pages quietly, which is why
  chapter 6's rule applies: after adding
  one, look at a page that uses it.
- **The `{{% %}}` variant.** Writing a
  shortcode call with percent signs
  instead of angle brackets makes Hugo
  run the *inner* text through the
  Markdown renderer before the template
  sees it. The lab used the angle form
  with an explicit `markdownify`, which
  does the same job in the open; know
  that both spellings exist before
  someone else's example confuses you.
