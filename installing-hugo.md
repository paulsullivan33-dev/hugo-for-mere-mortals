# Installing Hugo

Hugo installs like a tool from a simpler
time: one file, copied somewhere your
shell looks for programs. This chapter
does it the way the lab did — the
official release, checksummed — and then
names the packaged routes honestly.

## Which build: extended

Get the **extended** build unless you
have a reason not to. The difference is
narrow and real: the extended build
carries a Sass compiler (chapter 10),
which a good many themes and habits
assume. It costs nothing extra in size
that matters, and discovering you needed
it means installing again. The version
string tells you which you have — the
lab's ends in `+extended`, and chapter
10's stylesheet is the proof it works.

## The release route, with the checksum

The lab downloaded Hugo **0.168.0** from
the project's GitHub releases page
(`github.com/gohugoio/hugo/releases`),
taking the file named
`hugo_extended_0.168.0_linux-amd64.tar.gz`
— read the name as *extended*, version,
operating system, processor family. Pick
the row that matches your machine; the
wrong processor family simply will not
run, which is at least a clear failure.

Alongside the downloads, the project
publishes a checksums file. Use it. A
checksum is a fingerprint of the file;
if the fingerprint of what arrived
matches the fingerprint the project
published, the download is the file the
project shipped — not a corrupted copy,
not a substituted one.

```console
$ curl -LO https://github.com/gohugoio/hugo/releases/download/v0.168.0/hugo_extended_0.168.0_linux-amd64.tar.gz
$ curl -LO https://github.com/gohugoio/hugo/releases/download/v0.168.0/hugo_0.168.0_checksums.txt
$ grep extended_0.168.0_linux-amd64.tar.gz hugo_0.168.0_checksums.txt | sha256sum -c -
hugo_extended_0.168.0_linux-amd64.tar.gz: OK
```

(The `curl` lines are reconstructed into
command form; transcript t00 keeps the
actual run, in which the archive's
fingerprint — `787f1000…` — was compared
and answered `OK`.)

Then unpack and place the one file:

```console
$ tar -xzf hugo_extended_0.168.0_linux-amd64.tar.gz
$ ls
LICENSE  README.md  hugo
```

The archive holds three files; only
`hugo` matters. Copy it somewhere on
your `PATH` — a personal `~/bin` folder
is fine and needs no administrator
rights — or simply call it by its path
while you follow this guide. The lab
kept it in a work folder and ran it as
`./bin/hugo`; nothing about Hugo minds.

## The receipt

```console
$ hugo version
hugo v0.168.0-e27a6760c5547237f87d353aebe0580feadb20f4+extended linux/amd64 BuildDate=2026-10-13T16:42:50Z VendorInfo=gohugoio
```

Check: the command answers one line,
naming the version (`0.168.0`), the
commit it was built from, `+extended`,
and your platform. If the shell instead
says the command is not found, the file
is not on your `PATH` — the commonest
install failure, and a shell problem,
not a Hugo one (chapter 15).

## The packaged routes

Your system's package manager probably
offers Hugo too — `apt`, `brew`,
`winget`, and friends all carry it.
That route is one command and updates
ride along with everything else, which
is a genuine convenience. Two honest
cautions, both illustrated by this very
guide:

- **Packages lag.** Hugo releases often,
  and distributions trail by months.
  Chapter 6 turns on a template-system
  change in version 0.146 (April 2025);
  an older packaged Hugo would not
  merely lack a feature, it would lay
  out this guide's templates by
  different rules. Know which version
  you have before borrowing anyone's
  examples — including this book's.
- **Extended may be a separate choice.**
  Some packages ship the regular build
  only, or name the extended one
  differently. Check the version string
  for `+extended` before chapter 10.

On Windows and macOS the story is the
same shape — one binary, a releases page
with your platform's archive, package
managers that carry it (`winget`,
Homebrew, Chocolatey). The lab ran on
Linux and says so; nothing in the later
chapters depends on the platform except
the shape of file paths.

## A note on versions, once

Hugo is a living project and its
documentation online describes the
*current* version, whatever that is
when you read it. This guide pins
everything to 0.168.0 and keeps its
transcripts. When a command here
disagrees with your Hugo, believe your
Hugo, check its version, and then check
whether the feature moved — the Hugo
site's release notes are candid about
breaking changes, and chapter 6 shows
how to diagnose a template that the
ground shifted under.
