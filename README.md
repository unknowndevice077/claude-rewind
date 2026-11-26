# rewind

A Claude Code skill that makes big changes safe to undo.

Claude Code already has rewind built in: press `Esc` twice (or `/rewind`) and pick the prompt before things went wrong. It restores your files from a local snapshot, so it costs zero tokens.

But rewind doesn't track files changed by shell commands (`rm`, `mv`, `sed -i`...), and it can't help if you never committed. This skill teaches Claude to:

- offer a safety commit before big refactors
- edit with tracked tools instead of shell commands
- tell you exactly how to rewind when something breaks

## Install

```bash
git clone https://github.com/unknowndevice077/claude-rewind ~/.claude/skills-src/rewind
cp -r ~/.claude/skills-src/rewind/skills/rewind ~/.claude/skills/
```

On Windows (PowerShell):

```powershell
git clone https://github.com/unknowndevice077/claude-rewind $HOME\.claude\skills-src\rewind
Copy-Item -Recurse $HOME\.claude\skills-src\rewind\skills\rewind $HOME\.claude\skills\
```

Then in Claude Code: "refactor the auth module" and it will check your git state first.

Docs: https://code.claude.com/docs/en/checkpointing

## License

MIT
