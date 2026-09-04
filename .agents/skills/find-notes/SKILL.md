---
name: find-notes
description: Search deeply for compact, complete, self-contained web notes on a technical topic, then present a ranked shortlist and a top pick for the user to choose from before adding one entry to README.md. Use when the user asks for a learning resource, notes, or reading for a topic in this awesome-notes repo — "find resources for X", "add a section for X", "what should I read to refresh X", "is there a better link for X".
license: Apache-2.0
compatibility: Requires internet access, a web search tool, and curl.
---

# find-notes

This repo is a list of things you re-read to **refresh** an understanding you once
had. Not a curriculum, not a link dump, not a bookshelf. One canonical link per
topic.

Your job: given a topic, search deeply, then hand back a **ranked shortlist** of what
clears the bar below, your top pick with the reason it won, and the list of what you
rejected and why. The user picks; `README.md` then gets that one entry.

## The bar

A candidate qualifies only if it is **all six**:

1. **Web-native prose.** A site or single long page you read in a browser, with a
   table of contents and stable per-section URLs.
2. **Complete on its own.** Covers the topic end to end. Someone who finishes it has
   the whole mental model and needs no companion course, book, or video to fill gaps.
3. **Compact.** Cover to cover in one or two sittings. A semester distilled — not a
   reference manual.
4. **Random-access on a re-read.** Sections are headed by concept and stand on their
   own, so you can jump to the one thing you forgot and reload it without re-reading
   from chapter one. Check this from the table of contents: are the section names
   concepts you would actually go looking for?
5. **Concepts over APIs.** Teaches ideas. Tool-specific material qualifies only when
   the tool *is* the topic (see the CUDA and Modern C++ entries in README.md).
6. **Free and durably hosted.** No paywall, no login, no signup. The test is
   whether the URL will still resolve in five years and still land on the same
   section — a stable path, not one that moves when the site is reorganized.
   Course sites, personal domains, GitHub Pages, and canonical vendor docs all
   qualify (see the CUDA entry in README.md). Be wary of platform learning
   portals — `/learn/...`, `/courses/...` — which get restructured, and of
   `~username` faculty paths, which die when the person moves.

## Automatic rejections

Never propose these, and do not offer them as runners-up:

- **Slide decks** — `*.pdf` lecture slides, `assets/lectures/`, anything with slide
  numbers. Notes, not slides.
- **Lecture videos, playlists, MOOCs.** The one exception in README.md
  (3Blue1Brown) sits *beside* a text as a supplement, never as the primary link.
- **1000-page textbooks and reference manuals** — PBR Book, Foundations of Computer
  Graphics, CLRS, the Dragon Book. Complete, but not compact.
- **Sprawling tutorial sites with no single reading order** — Scratchapixel,
  GeeksforGeeks, W3Schools, tutorialspoint.
- **Course landing pages** that are mostly syllabus, schedule, and homework links.
- **Blog series** unless indexed as one ordered whole *and* genuinely complete.
- **Awesome-lists, Reddit threads, listicles**, and AI-generated content farms.
- **Books free only as an unofficial PDF.** Official free text or nothing.

## Calibrate against README.md

Read `README.md` first. The existing entries define the shape:

| Entry | Why it qualifies |
| --- | --- |
| CS 186 / CS 168 / CS 61C / 6.390 notes | Official course notes published as a readable web book |
| OSTEP single-page note (Jose Hu) | A 700-page book compressed to one headed, jump-to-able page — the ideal |
| Little Book of Linear Algebra | Purpose-built as a compact complete treatment |
| Illustrated Transformer | Single page, one idea, definitive |
| Computer Graphics from Scratch | Free full text, pseudocode, no API, ~15 short chapters |

The test for any candidate: **does it sit comfortably next to the OSTEP note and the
CS 186 notes?** If it is conspicuously longer, or leaves gaps those fill, it does not.

## Process

1. **Read `README.md`.** Check whether the topic or a near neighbour is already
   covered — the job may be replacing a weak link rather than adding one.

2. **Search deeply — at least five or six queries**, varying the framing until new
   queries stop surfacing new names:
   - `<topic> course notes online textbook site:edu`
   - `<topic> "little book" OR "from scratch" OR "in one weekend"`
   - `<topic> notes single page complete free`
   - `<topic> lecture notes web book <known-strong-school>` — name the schools or
     authors who own the topic, when there is an obvious home
   - the sub-areas of the topic by name, to catch a resource titled after a part
     rather than the whole
   - what practitioners call it, which is often not the academic name

   One or two searches is not enough to rank anything. Keep going until the same
   handful of names keeps coming back — that repetition is the signal you have
   found the real field, not the first page of it.

   Search is for discovery only. Never trust a snippet's claim about length, cost,
   or completeness.

3. **Verify every finalist by fetching it**, not by reputation:
   - `curl -s -o /dev/null -w '%{http_code}' -L <url>` — expect 200, and no redirect
     to a paywall or login.
   - Pull the table of contents. Count the chapters. Check the last chapter actually
     reaches the end of the topic instead of trailing off.
   - Confirm there is no signup wall and no "buy the book to continue" partway in.
   - Check it is not rotting — dead links, or 2009 content about a moving target.

   This step is what catches the length and completeness failures that reputation
   hides. Do not skip it for a resource you think you already know.

4. **Present a ranked shortlist, then your top pick, then ask.** Give three to five
   surviving candidates, best first. One line each: title, author, URL, and the
   single reason it ranks where it does — length, coverage, or what it does better
   than the one below it. Then name your top pick and say what decided it against
   the runner-up.

   Close by asking the user to rank them or confirm the pick. This is a judgment
   call about their own reading taste, so the shortlist is real: do not stack it
   with filler to reach three, and do not bury the second choice. If only one
   candidate survives the bar, say so plainly and explain what the others failed —
   a shortlist of one is a valid answer, padding it is not.

5. **Report the rejects below the shortlist.** Name the obvious candidates you
   discarded and the rule each one broke. This is what stops the same weak link
   resurfacing next time, and it shows the shortlist is what survived rather than
   what you found first.

6. **Wait for the user's pick before editing.** `README.md` gets exactly one entry
   for the topic — the one they chose. Never edit before they answer.

## Output format

Match `README.md` exactly: `### Section`, then `- Title (Author): URL`. The author
parenthetical goes in only when the work is known by its author. Sections are
ordered by when they were added — append new ones at the end.

```
### Computer Graphics
- Computer Graphics from Scratch (Gabriel Gambetta): https://gabrielgambetta.com/computer-graphics-from-scratch/
```

## Commits

One entry per commit.

**README entries** — `docs(<topic>): <what>`, where `<topic>` is the README section
the entry lands in, lowercased. The scope is what carries the signal: it says which
topic moved without opening the diff.

```
docs(robotics): add Introduction to Robotics and Perception
docs(linear-algebra): replace 3Blue1Brown with Little Book of Linear Algebra
docs(operating-systems): drop dead OSTEP mirror
```

**Changes to this skill** — prefix with `skill:` so they are easy to separate from
the link history.

```
skill: add find-notes
skill: drop the ten-minute skimmability criterion
skill: loosen the durability rule to allow new resources
```

Either way: **one line, always.** Imperative mood, no trailing period, under 72
characters. Never write a commit body in this repo — if the reason for a change will
not fit on the subject line, it belongs in this skill or in `README.md`, not in the
git log.
