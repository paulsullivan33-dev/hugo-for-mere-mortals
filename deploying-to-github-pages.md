# Deploying to GitHub Pages

Everything so far happened on one
machine. Deployment is the step where
the finished folder goes to live
somewhere public — and for a static
site it is refreshingly small, because
there is nothing to install at the far
end. This chapter describes the shape
of it, using GitHub Pages as the
example host. The build command it all
hangs on was run, timed, and inspected
by the lab; the upload itself was not —
the lab machine has no public address
and this guide does not pretend it
performed one. What follows is the
documented pattern, labelled as such.

## What deployment is, for a static site

Strip it down and there are only two
moves:

1. **Run `hugo`** on a machine that has
   the project — yours, or a CI
   machine — producing `public/`.
2. **Put `public/` where a web server
   can hand it out**, under the address
   in `baseURL`.

No runtime to start, no database to
migrate, no environment at the far end
beyond "a folder of files, served".
That is the entire operational content
of chapter 1's bet. If the site breaks
after deploying, it is nearly always
one of three things, all checkable
beforehand: the build that ran wasn't
this build (an old `public/` shipped),
the `baseURL` doesn't match the real
address (chapter 9 — feeds and
sitemaps point at the wrong place), or
something in `public/` never got
uploaded.

## The Actions pattern, generically

GitHub Pages' usual arrangement runs
those two moves itself. In outline —
this is the shape of the thing, from
GitHub's and Hugo's documentation, not
a transcript:

- The project lives in a GitHub
  repository, and Pages is switched on
  for it with **GitHub Actions** as the
  source.
- A workflow file in
  `.github/workflows/` says, in effect:
  *on every push to the main branch —
  check out the project, install Hugo
  (the **extended** build, at a pinned
  version, if the site uses chapter
  10's pipeline), run `hugo`, upload
  the `public/` folder as the Pages
  artifact, and deploy it.*
- A minute or so later the site at
  `https://<account>.github.io/
  <repository>/` is the new build.

Two details in that outline earn their
keep. **Pin the Hugo version** in the
workflow: chapter 6 is the story of
what a silent version change can do to
templates, and the build machine should
run the version the site was written
against until a human decides
otherwise. And note the **address
shape**: a project site lives under a
path (`/repository/`), so its
`baseURL` must include that path —
the mismatch between a root address
and a path address is the single most
common first-deploy breakage, and it
shows up as a page that loads without
styles, every link leading one folder
too shallow.

## Custom domains, in one paragraph

Pointing your own domain at Pages is a
DNS record at your registrar plus
telling GitHub the name (a `CNAME`
file in the site, or the repository
settings), after which `baseURL`
becomes the domain, root and all, and
GitHub arranges the HTTPS certificate.
The lab did none of this; it is a host
setting, not a Hugo feature, and it is
listed here so the map has no blank
corner where readers usually meet
their first `404`.

## The hand-carried alternative

Nothing about the two moves requires
GitHub. `hugo` on your own machine,
then copy `public/` to any web space —
a club's shared hosting, a home server,
a €3 VPS — with whatever file-copying
tool you already trust. Several of this
series' readers will find that *more*
legible than a CI pipeline: the build
is a command they ran, the upload is a
folder they can see. Hugo also ships a
built-in `hugo deploy` for certain
cloud buckets; the lab never ran it,
and a plain copy has the advantage of
being exactly what it looks like.
