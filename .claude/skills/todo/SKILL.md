---
name: todo
description: Use when someone asks "what's on my to-do list", "what's outstanding", "add a to-do", "check off X", or wants to see/update the running task list. Reads and edits context/todo.md.
---

## What this skill does

`context/todo.md` is the user's running to-do list — open work not yet scoped into a decision or shipped. This skill reads it back on request and edits it (add, check off, reorder, remove) on request.

## Execution

### Reading the list

`context/todo.md` is the starting point, not the whole answer — "what's outstanding" should reflect everything, not just what's been manually copied into one file. Every time this is asked, do a full sweep:

1. `context/todo.md` — the maintained list itself.
2. `context/priorities.md` — the top-level quarter goals; flag if `todo.md` has drifted from these.
3. `decisions/log.md` — skim recent entries for "next up", "follow-up still open", "pending" type language that never made it onto `todo.md`.
4. `inbox/*.md` (excluding `README.md`) — unprocessed handoff notes are themselves outstanding work (processing them).
5. Anything else that looks like a running list, or files created recently in `context/` or `references/` that haven't been folded into `todo.md` yet.

Fold anything found in 2-5 that isn't already in `todo.md` into it (don't just report it and let it drift). Then present the combined picture. Match detail to the ask — a quick "what's outstanding" gets a grouped summary, a request for full detail gets everything. Group by section; don't re-derive priority order unless asked.

### Adding an item

Append to the most sensible existing section (or a new section if none fit — don't force a bad fit). Keep the one-line style already used in the file. Don't renumber existing items; add the new one at the end of its section.

### Checking off / removing an item

When an item is done: delete it from `todo.md`. If it's non-trivial (a shipped automation or real decision, not just a chore), suggest logging it in `decisions/log.md` first — ask before writing a decisions-log entry, since not everything rises to that bar.

### Notes

- This file is a working list, not an audit trail — no need to keep history of removed items.
- If `context/todo.md` doesn't exist, create it with sections mirroring `context/priorities.md`, plus a "Loose threads" section, before adding to it.
