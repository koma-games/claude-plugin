---
name: studio
description: Use when the user asks about tasks, projects, bugs, the board, cycles, labels or what they are working on in KOMA Studio, or wants an issue created, reassigned, prioritised, moved, commented on, deleted or restored.
---

# KOMA Studio

The task tracker of a small game studio, and the eleven tools that reach it. What the studio is
part of, and how to write for it, is the `koma` skill; this one is the board.

## Start with the board, not with a guess

Two ids and one label matter, and confusing them is the most common way to fail here.

- **The project id** is a slug: `saint-nicholas-night`. `list_projects` returns it.
- **The issue key** is what a person says: `SNN-42`, `KOM-10`. It is a label, derived from the
  project id and the issue number, and **no tool accepts it**.
- **The issue id** is what every tool takes: a uuid.

So "move KOM-10 to review" is two steps, always: `list_tasks` for that project, find the issue whose
key is `KOM-10`, then `move_task` with its id. Do not try the key as an id; it will not be found.

`list_tasks` is also where the project's vocabulary comes from: its members with their names, its
labels, its cycles and its builds. Anything that names a person or a label needs it first. Read it
once and reuse it for the rest of the conversation rather than calling it before every write.

## The words the tracker uses

The exact values are in each tool's schema, so they never have to be remembered. What the schema
cannot say is when to use which.

**Status** is where a thing sits: `backlog` (not scheduled), `todo` (scheduled, not started),
`in_progress`, `in_review` (waiting on somebody else), `done`, `cancelled`. The last two both stop
the clock and they are not synonyms: `done` is shipped, `cancelled` is a deliberate decision not to
do it. Never mark something `done` to get it off a list.

**Priority** is when: `urgent` means drop what you are doing, then `high`, `medium`, `low`, `none`.

**Kind** is what: `feature`, `bug`, `task`, `chore` (upkeep with no player-visible result).

**Severity** is how bad it is when it happens, and only means anything for a bug: `crash` (crash,
hang or data loss), `major` (unusable, no workaround), `minor` (works, but wrong), `cosmetic`.

Priority and severity are different questions and a person often means one while saying the other.
A cosmetic bug can be urgent the day before a showcase; a crash in a tool nobody uses this month is
not. When somebody says "critical", ask which they mean rather than setting both.

**Cycle** is a sprint with dates. Its phase is computed from today, so "the current cycle" is
whichever one contains today's date, not a flag on a row.

## Writing

`create_task` needs only a title. Everything else takes a default, and a new issue lands in
`backlog` as a `task` with no priority.

Set what the person actually said and nothing more. "Create a bug for the door not opening" is
`kind: bug` and a title, not an invented severity and a guessed assignee. If they said "urgent",
that is `priority: urgent`. If they did not say who, leave it unassigned; somebody will pick it up,
and a wrong assignee is worse than none because it looks decided.

**Labels can refuse a write.** A project can require a label from a given group, and labels carry
rules: one from a group, this one implies that one, these two conflict. A write that breaks a rule
comes back refused with the reason. Read `list_tasks` for the groups before labelling, and pass the
refusal on rather than retrying with a different guess.

`delete_task` moves an issue to the project trash and `restore_task` brings it back. Nothing in
these tools removes anything permanently, so a deletion is recoverable and is worth saying so when
somebody sounds hesitant.

## Answering well

**"What am I working on?"** `my_tasks`, and lead with what is `in_progress`, then what is `todo`.
Sort by priority inside each. Do not read out the backlog unless asked; it is a list of things
deliberately not scheduled.

**"What is the state of the project?"** `list_tasks`, then count by status and name what is
`in_review`, because that is the only column where the work is finished and waiting on a person.

**"Why is this still open?"** `read_task_history`. Comments and activity together, oldest first,
and the answer is usually in the last two entries.

**"Anything blocked?"** There is no blocked status. What people mean is `in_review` that has sat
still, or `in_progress` with no recent activity. Say which of the two you looked at.

Report keys, not uuids. A person recognises `SNN-42` and has never seen the id.

## What a connected application may do here

The token this plugin holds can be narrower than the person it belongs to, never wider. Two checks
run on every call: what the token was granted, and what the person themselves holds.

So "you can do this and this token cannot" is a real and correct answer, not a bug to work around.
A refusal naming a capability like `projects:project:snn:write` means the token is read-only for
that project. A refusal that says the application cannot use an endpoint at all means that route is
not open to connected applications. Neither is fixed by retrying.

Nothing here is decided by the gateway or by this plugin. The service that owns the data decides,
the same way it decides for the website.
