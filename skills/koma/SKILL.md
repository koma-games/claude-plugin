---
name: koma
description: Use when the user asks what KOMA is, names one of its products or services (mova, KOMA Studio, files, tools, sign-in), or writes any text, code comment or interface copy that will live in a KOMA repository.
---

# KOMA

A small platform for a game studio: what it is made of, and how anything written for it is spelled.
The task tracker inside it has its own skill, `studio`, and that is where the board, its vocabulary
and its tools are described.

## The products and the services

Two products, and a person will name them: **KOMA**, the app at `app.koma.im` with **mova**, the
social surface inside it; and **KOMA Studio** at `studio.koma.im`, which is where these tasks live,
along with builds, translation and Steam. Files, tools and sign-in are their own services. A
**service** is machine-facing and has a one-word slug; a **product** is what a person installs. They
are different name systems and collapsing them is the mistake to avoid.

## Writing anything that lands in a KOMA repository

Not style preferences. The first is enforced by CI and fails the pipeline.

- **No em dash and no en dash, ever, in any language.** Only the plain hyphen. If a dash was joining
  two halves of a sentence, rewrite it: a full stop, a semicolon, a colon, or a conjunction. In code
  comments the in-line separator is a double hyphen.
- An empty cell in a table is a plain hyphen. Not "N/A", not blank.
- Names are spelled out. `database`, never `db`.
- A name says what a thing is, never how it arrived. A protocol, a format or a vendor may qualify a
  name but must never be the whole of it.
