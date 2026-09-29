---
name: inbox
description: Use when someone says "check the inbox", "process the inbox", or "check for inbox files". Reads new handoff notes dropped in inbox/ (summaries from Claude desktop/phone/other chats), folds anything worth keeping into memory or context files, then archives the processed file.
---

## What this skill does

The `inbox/` folder is a drop zone for handoff notes from other Claude conversations (desktop app, phone app, claude.ai chats). This skill reads whatever's new, decides what's worth keeping, saves it in the right place, and clears the folder so nothing gets reprocessed.

Typical use: you have a useful chat on your phone, ask it "summarise this as a handoff note for my AIOS", save that as a `.md` file in `inbox/`, then say "check the inbox" here.

## Execution

### Step 1: List inbox contents

Glob `inbox/*.md`, excluding `README.md`. If nothing's there, say "inbox is empty, nothing to process" and stop.

### Step 2: Read and triage each file

Read each file in full. Decide where each fact belongs:

- **Persistent memory** (user, feedback, project, or reference type) — use Claude Code's standard memory system. Skip anything derivable from the files, already in `CLAUDE.md`, or ephemeral detail that won't matter next week.
- **Context files** — durable background about the business or priorities fits better in `context/about-business.md`, `context/about-me.md`, or `context/priorities.md`. Read the target file first, then edit in place rather than duplicating.
- **Decisions log** — if the note records a decision the user made (not just a fact), append it to `decisions/log.md` in that file's existing format.

Not everything is worth keeping. If a file has nothing durable, say so rather than forcing a save.

### Step 3: Report back

Per file: what was kept and where it went, what was skipped and why. A few bullets, not an essay.

### Step 4: Archive processed files

Move each processed file from `inbox/` to `archives/inbox/` (create it if missing), keeping the filename. Move, not copy — the inbox should end up containing only `README.md`.

## Notes

- Never touch `inbox/README.md`.
- If a file is malformed or empty, skip it and say so rather than guessing.
- Don't create new context files — only write into existing ones or the memory system.
