# Umigame no Soup Host (ウミガメのスープ出題役)

A Claude Skill that turns Claude into a host for **Umigame no Soup** (海亀のスープ / "Turtle Soup"), a Japanese lateral-thinking puzzle game. Claude generates an original riddle, seals the answer away from itself, and lets you solve it by asking yes/no questions.

## How it works

- **Original puzzles only.** Each riddle is generated fresh by a subagent — no reuse of famous puzzles (the original Turtle Soup story, the elevator man, etc.).
- **The answer stays hidden, even from Claude's own reasoning.** The solution is written to a scratch file as base64 and isn't decoded until you ask your first question, so it won't leak into visible thinking.
- **Difficulty is tuned to be genuinely hard** — expect somewhere around 40–60 questions before you crack it. Misleading (but fair) details are part of the fun.
- **Answers come as "Yes" / "No" / "Irrelevant"** (はい / いいえ / 関係ありません), with an occasional short clarifying hint when a question is ambiguous.
- **Stuck?** After ~30 questions, Claude will offer step-by-step hints if you want them.
- Once you solve it (or give up), Claude explains the full solution and offers to run another round with a different theme.

> **Note:** Puzzles and answers are generated in Japanese, for a Japanese everyday-life context. This skill is built for Japanese speakers.

## Requirements

- Claude Code (or any Claude surface that supports Skills) with **subagent access** (the `Agent` tool). This is what lets Claude keep the answer sealed away from its own visible reasoning.
- Without subagent access, the skill still runs, but Claude will warn you that the answer may become visible in its thinking.

## Installation

**Option 1 — as a plugin marketplace**
```bash
claude plugin marketplace add <your-username>/<this-repo>
claude plugin install umigame-soup-host@<marketplace-name>
```

**Option 2 — manual**
Copy the `skills/umigame-soup-host/` folder into your own `skills/` directory (e.g. `~/.claude/skills/`), or upload `SKILL.md` directly via Claude.ai's **Customize > Skills**.

## Usage

Just ask Claude to host a round — e.g. "ウミガメのスープを出題して" or `/umigame-soup-host` if installed as a plugin command. Claude will present a short puzzle and the classic prompt: **"なぜでしょう？" (Why?)**. Ask yes/no questions until you figure it out.