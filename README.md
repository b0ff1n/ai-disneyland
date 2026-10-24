# ai-disneyland 🎡

A minimal **file-based AI harness for studying**. Not an application and not a codebase: plain Markdown files + Claude Code or Codex + Git.

## Quick start

1. Open a terminal **in the `ai-disneyland` folder**.
2. Run `claude` (Claude Code) **or** `codex` (Codex CLI). These tools must be installed and authorized beforehand.
3. Ask: "Read the project instructions and tell me what you know about my study plan".
4. Start a session with `/study-session` in Claude Code or `$study-session` in Codex. You can also simply write "Let's run a study session on Spivak".
5. At the end, say: "We're done with the session. Write it up and update the progress files". Review the proposed changes.

## How it is organized

```text
ai-disneyland/
├── AGENTS.md                        # shared rules for the agent
├── CLAUDE.md                        # imports AGENTS.md for Claude
├── learning/
│   ├── learner.md                   # confirmed context about the learner
│   ├── roadmap.md                   # study goals and plans
│   ├── now.md                       # current state / next step
│   ├── progress/                    # progress per subject
│   └── sessions/                    # reports of completed sessions
├── templates/session-note.md        # report template
├── resources/README.md              # links to materials
├── .claude/skills/study-session/     # skill for Claude Code
└── .agents/skills/study-session/     # the same skill for Codex
```

`AGENTS.md` holds the rules of behavior; `learning/` is our **open and verifiable memory**. The contents of `learning/` are kept in Git. Claude Code's automatic memory, if enabled, lives outside this repository; do not treat it as the source of truth.

## Core principle

Reduce the amount of programming and increase the amount of **actual studying**. Do not add databases, RAG, external plugins, subagents, or scripts until there is a concrete problem they solve.

## Working with Git

The repository is already initialized and has an initial commit. Pushing to GitHub is **not configured**.

After unpacking: `git status` should show a clean state (if the archive was extracted together with `.git`). To attach your own remote repository:

```bash
git remote add origin git@github.com:YOUR_USERNAME/ai-disneyland.git
git push -u origin main
```

Create an empty **private** repository on GitHub in advance, or use another Git host and replace the URL. Do not commit API keys, other people's books, or personal or confidential materials without a deliberate decision.

## Where to edit

- New goals → `learning/roadmap.md`.
- Changes to the teaching method → `AGENTS.md` or `SKILL.md`.
- After a session → a new entry in `learning/sessions/`, plus updates to `now.md` and the relevant subject progress file.
- Recurring mistakes → `learning/progress/<subject>.md`, linked to the session date.

**Compatibility:** the skill is intentionally duplicated in `.claude/skills/` and `.agents/skills/` so that it works in both environments and when the ZIP is unpacked on different operating systems. If you edit the skill's method, keep both `SKILL.md` files in sync. The duplicates can later be replaced with symlinks.

Documentation: [Claude Code memory](https://code.claude.com/docs/en/memory), [Claude Code skills](https://code.claude.com/docs/en/skills), [Codex skills](https://learn.chatgpt.com/docs/build-skills).
