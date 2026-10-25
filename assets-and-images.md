# Assets and Images

Chapter 2 drew the line: files Hugo
should *work on* live in `assets/`;
files to hand over untouched live in
`static/`. This chapter works both
sides of it, on the three assets the
lab actually shipped: a Sass
stylesheet, a photograph, and a badge.

## A Sass stylesheet, compiled

The site's styles are written in
**SCSS** — CSS with variables, nesting,
and arithmetic — in `assets/scss/
main.scss`:

```scss
$sky: #16264a;
$accent: #c98a2d;

header {
  border-bottom: 3px solid $sky;

  nav ul {
    display: flex;
    gap: 1rem;
  }
}
```

Browsers can't read that; Hugo's
**asset pipeline** compiles it. The
base template asks for the file and
pipes it through the compiler:

```html
{{ $css := resources.Get "scss/main.scss" | css.Sass }}
<link rel="stylesheet" href="{{ $css.RelPermalink }}">
```

The built site contains `public/scss/
main.css` — checked in transcript t04:
the variables are gone, `$sky` has
become `#16264a` in four places, a
`lighten()` call has been computed into
a colour, and not one `$` survives.
That is the pipeline's whole personality:
*source in `assets/`, product in
`public/`, the template holding the
address of the product.*

Three honest footnotes, all from the
lab's own build:

- **This needs the extended build.**
  Sass compilation is precisely what
  `+extended` adds (chapter 3). The
  regular build cannot run that line of
  template; sites that don't use Sass
  never miss it.
- **The built-in compiler is living on
  borrowed time.** Every lab build
  warned, verbatim: *"css.Sass: libsass
  was deprecated in Hugo v0.153.0 and
  will be removed in a future release.
  Use dartsass instead."* The lab kept
  the transcript rather than hiding it.
  In plain terms: the extended build's
  bundled Sass (libsass) still works
  today and is deprecated; the
  successor, Dart Sass, is a separate
  program you install, which
  `css.Sass` then uses. A site written
  now should expect to make that small
  migration, and the SCSS itself — the
  part you wrote — carries over
  unchanged.
- **The pipeline does more than Sass.**
  The same `resources.Get` machinery
  concatenates, minifies, and
  fingerprints files (a fingerprint —
  the content's hash in the file name —
  is how sites make browsers fetch the
  new stylesheet instead of a cached
  old one). The lab used none of those
  steps and says so; they are one pipe
  segment each when a site grows into
  needing them.

## A photograph, resized by Hugo

The telescope-cleaning note is a leaf
bundle (chapter 5), so its `mirror.png`
is a *page resource* — a file the page
owns. The single-page template finds it
by name and asks for a smaller copy:

```html
{{ with .Resources.GetMatch "mirror.png" }}
  {{ $small := .Resize "300x" }}
  <img src="{{ $small.RelPermalink }}" width="{{ $small.Width }}" height="{{ $small.Height }}" alt="{{ .Title }}">
{{ end }}
```

The build's output directory tells the
story (transcript t04): beside the
page sit **two** images — `mirror.png`,
the original 640×400, published because
bundle files are, and `mirror_hu_….png`,
Hugo's generated 300×188 copy, which is
the one the page displays. The original
never left the project in its display
role; the resize happened at build
time, on the author's machine, once —
not per visitor, not by hand in an
editor. `.Resize "300x"` reads as
*300 wide, height in proportion*;
`"300x200"` would crop to fit, and the
same machinery converts formats and
strips metadata. For a site of club
photographs, this is the difference
between a photo workflow and a photo
chore.

## The badge, copied untouched

The club's badge is an SVG drawn once
and never processed. It lives in
`static/images/badge.svg`, and the
build copied it to `public/images/
badge.svg` byte for byte — the build
summary counts it as the site's one
static file (transcript t03). The
footer references it by address. That
is `static/`'s whole contract: *what
you put there is what ships*, paths
preserved. Favicons, a PDF of the
club's constitution, a `robots.txt`
you've written by hand — anything that
is already in its final form belongs
here, and anything that isn't, doesn't.
