# The Neighbours

Hugo is one answer to "how does a
website get made", and not the only
one worth respecting. The honest
comparisons, by what each tool *is*
rather than by feature lists:

## MkDocs

The closest neighbour in spirit: a
folder of Markdown in, a finished site
out, with the same build-it-all-in-
advance model and the same plain-folder
portability. The difference is intent.
MkDocs is built for **documentation** —
its themes, navigation, and search are
shaped for manuals and project docs out
of the box, with very little templating
asked of you. Hugo is a **general**
site builder: blogs, club sites,
portfolios, docs too — but you supply
more of the shape yourself, starting
with templates like chapter 6's. If
the site is documentation and nothing
else, MkDocs is the shorter path; if
it might grow a blog, a photo section,
and opinions, Hugo's generality is the
point. (This very series is published
with MkDocs, and says so in its own
volume — the two tools are colleagues
in these pages, not rivals.)

## Jekyll

The elder of the family, written in
Ruby and long the default behind GitHub
Pages, where it still runs natively —
a Jekyll site can be built *by* GitHub
with no workflow file at all, which
remains its neatest trick. Its template
language (Liquid) is gentler than
Hugo's Go templates, its plugin and
theme culture is deep, and its builds
are slower by orders of magnitude —
a difference a five-page site never
feels and a five-thousand-page site
feels daily. Choose it for the Pages
integration and the ecosystem; choose
Hugo for speed and the single binary.

## Eleventy

A JavaScript static generator, beloved
for flexibility: many template
languages in one project, data from
anywhere, very little imposed shape.
That looseness is its trade — where
Hugo gives you one strong opinion
(sections, taxonomies, the pipeline,
all built in), Eleventy gives you the
parts and wishes you well. Sites whose
authors are fluent in JavaScript often
prefer it; sites maintained by a
rotating cast of mortals often prefer
Hugo's guardrails.

## WordPress and the managed builders

The other continent entirely: a program
*runs* the site — database, admin
screens, editing in a browser, comments
and accounts built in, and a bill (in
money or in maintenance) for keeping it
patched and safe. For a site that must
be edited by people who will never open
a text editor, or that needs members
and a shop, that trade can be right,
and chapter 1 weighed it honestly.
What the static tools buy back is
everything WordPress spends: no
patching treadmill, no database to
protect, hosting that costs nothing
because there is nothing to host but
files. The question is never "which is
better" but "who edits it, and what
must it *do* at 2 a.m. when nobody is
watching" — WordPress does things at
2 a.m.; a Hugo site, gloriously, does
nothing at all.

## A folder of hand-written HTML

The zero-tool option, and not a joke:
for three pages that change once a
year, a generator is machinery without
a job, and the honest advice is a text
editor and the `static` bargain applied
to the whole site. The generator earns
its install the day a fourth page
repeats the header by hand, or a menu
must change in nine places. Hugo's own
cost accounting (chapter 1) runs both
ways.
