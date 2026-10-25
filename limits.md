# Limits

What Hugo can't do, or doesn't do the
way a newcomer expects — collected in
one place, because a tool's edges are
part of its description.

**No dynamic anything.** The built site
cannot react to a visitor: no comments,
no accounts, no search of its own, no
forms that go anywhere, no "recently
viewed". Each of those has a known
workaround — an outside comment
service, a search index queried by
JavaScript in the browser, a form
handled by a third party — and each
workaround is another service to
choose, trust, and eventually replace.
Sites whose *purpose* is interaction
should not start here (chapters 1, 13).

**The authoring is files, full stop.**
No browser editor, no draft autosave in
a cloud, no colleague leaving comments
in the margin. For some authors that is
the appeal — versioned, greppable,
owned — and for others it is a veto.
Know which author you are before the
site is nine months old.

**The ground has moved once, and may
again.** Hugo overhauled its template
system in version 0.146 (chapter 6) and
deprecated its built-in Sass compiler
shortly after (chapter 10). Both
changes were announced and defensible;
both silently altered what existing
sites and older advice *mean*. Hugo
releases quickly and evolves in the
open, which is a virtue with a price:
pin your build version, read release
notes when you upgrade, and expect an
old site's first rebuild on a new Hugo
to be an event, not a formality.

**Speed has a shape.** Hugo's famous
millisecond builds are real — this
guide's lab measured them — and they
scale well, but the number is for
*building*. It buys the author a tight
edit–look loop; it says nothing about
the visitor's experience, which is
decided by your images and your
hosting, not your generator. A site
with a 4 MB photograph is slow in
every tool ever written; chapter 10's
resizing exists because of it.

**One language per idea, mostly.**
Templating is Go's template language,
with its conventions (the reference-
date formatting of chapter 6 is the
famous one), and configuration is
TOML/YAML/JSON. None of it is hard;
all of it is *specific*, and examples
from other generators do not translate
by resemblance.

**Themes are other people's systems.**
This guide dodged the question by
writing its own templates. The
ecosystem's big themes are powerful
and popular, and each is effectively a
second tool to learn — its own config
vocabulary, its own upgrade cadence,
its own opinions — riding on the
first. That trade is often worth it.
It is never free, and a theme's
documentation, not Hugo's, is where
its behaviour lives.

**The extras are somebody else's
problem.** Analytics, comments, contact
forms, e-commerce: Hugo neither
provides nor blesses any of them. The
static-site world has answers for
each, all external. A reader tallying
requirements that start with "visitors
must be able to…" should count how
many of them end outside the tool
before choosing it.
