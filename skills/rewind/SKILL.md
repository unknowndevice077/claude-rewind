---
name: rewind
description: Make big Claude Code changes safe to undo. Use before multi-file refactors, risky edits, or whenever the user says "don't break anything", "be careful", "I haven't committed" or asks how to undo what Claude did.
---

# rewind

Claude Code saves a checkpoint before every prompt. Press `Esc` twice (or type `/rewind`) to pick a prompt and restore the code, the conversation, or both. Restoring is free: it copies saved file snapshots back, no model call, no tokens.

It has gaps. This skill covers them.

## Before a big change (5+ files, a refactor, a migration)

1. Run `git status`. If the repo has no commits or has uncommitted work, tell the user and offer a safety commit:
   `git add -A && git commit -m "checkpoint before <task>"`
   Only commit when they say yes.
2. Say in one line what you are about to touch, so the user knows which checkpoint to rewind to.

## While working

- Change files with the Edit/Write tools, not shell commands. Rewind only tracks edits made by those tools.
- Never delete, move or overwrite files with `rm`, `mv`, `cp`, `sed -i` or redirects during a risky change. Rewind cannot undo them. If one is needed, say so first and make sure git has a copy.
- Subagent edits are not reliably restored either. Keep risky edits in the main session.

## After

- Run the tests or the build. If it broke, tell the user straight away and remind them:
  "Press Esc twice and pick the prompt before this one to restore the code. It costs no tokens."
- If they want to keep the change, suggest a commit.

## What rewind can't save you from

- Shell command changes (see above)
- Files outside the project, symlinks, hard links
- Anything older than the session's last 100 checkpoints

Git is the real save file. Rewind is the quick undo.
