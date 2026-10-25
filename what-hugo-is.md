# What Hugo Is

Hugo builds **static websites**. A static
website is a folder of finished files —
one HTML page per page of the site, plus
its pictures and stylesheets — that a
web server hands out exactly as they
sit. Nothing is computed when a visitor
arrives. All the computing happened
earlier, once, on the builder's machine,
when Hugo ran.

That one decision — *build everything in
advance* — is the whole subject of this
guide, so it is worth seeing clearly what
it buys and what it costs.

**What it buys:**

- **Speed at serving time.** The server
  does the dumbest possible job: file
  requested, file sent. A Hugo site stays
  fast on the cheapest hosting there is,
  including free tiers, because there is
  almost nothing to go slow.
- **Nothing to attack.** There is no
  database to break into, no admin login
  to guess, no server-side program with
  bugs to exploit. The site that can't
  run code can't be made to run the
  wrong code.
- **A site you can hold.** The entire
  website is a folder. You can copy it,
  archive it, move it to another host in
  an afternoon, or open its pages
  straight off the disk. Your content
  lives in plain Markdown files in a
  folder you own, not inside somebody's
  database.
- **A build you can watch.** Running
  Hugo on the guide's lab site — 27
  pages, a compiled stylesheet, a
  resized image — took it 379
  milliseconds the first time and 88
  milliseconds once warm (transcript
  t03, and the rebuild in t90). Speed of
  building sounds like a luxury until
  you are editing: it makes the loop
  *change something, look at the result*
  effectively instant.

**What it costs:**

- **Nothing dynamic.** No comments, no
  accounts, no shopping basket, no
  "pages people like you read". Anything
  that must react to a visitor needs
  either an outside service or a
  different kind of site. Chapter 14 is
  blunt about this.
- **The author needs the tools.** There
  is no friendly web form for writing
  pages. You edit text files, on a
  machine with Hugo installed. For a
  club secretary who only ever uses a
  browser, that is a real cost, honestly
  weighed in chapter 13.

## The shape of the work

A Hugo project is one folder with a
predictable anatomy (chapter 2 walks it
part by part):

- your writing, as Markdown files, in
  `content/`;
- templates — HTML with placeholders —
  in `layouts/`, describing how each
  kind of page should look;
- one configuration file, `hugo.toml`,
  naming the site and its settings;
- and, when you ask, an output folder,
  `public/`, holding the finished site.

You run `hugo`, and the folder of text
becomes the folder of website. You run
`hugo server` while you work, and Hugo
rebuilds on every save and serves the
result on your own machine so you can
look at it. When you are happy, the
`public/` folder is what gets published
(chapter 11).

Nothing in that story requires Hugo to
phone home, an account, or a network.
The lab did the whole build offline
from the internet's point of view except
the initial download.

## What Hugo is not

- **Not a content management system.**
  WordPress and its kin store your pages
  in a database and assemble them per
  visit, with an editing screen in a
  browser. Hugo is the opposite bet on
  both counts (chapter 13 compares them
  fairly).
- **Not a web framework.** It does not
  run your program for visitors. If your
  idea needs a server thinking, Hugo is
  the wrong tool, full stop.
- **Not a host.** Hugo makes the folder;
  putting the folder where the world can
  see it is a separate, smaller job.
- **Not a theme with a tool attached.**
  Hugo is often met through a big
  downloaded theme, and many people
  never learn which parts are Hugo and
  which are the theme's. This guide
  deliberately writes its own small
  templates instead, so the boundary is
  never in doubt.
