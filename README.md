# ウミガメのスープ出題役 (Umigame no Soup Host)

Claudeを「ウミガメのスープ」（水平思考クイズ）の出題役にするClaude Skill。オリジナルの謎を出題し、質問に「はい／いいえ／関係ありません」で答え、正解判定まで行う。

## できること

- **毎回オリジナルの謎を生成。** 有名な既存問題（「ウミガメのスープ」本編、エレベーターの男など）の使い回しはしない。
- **真相はClaude自身の思考(thinking)にも漏れない。** 問題作成はサブエージェントに任せ、真相はbase64化してスクラッチファイルに保存。最初の質問が来るまでファイルは開かない。
- **難易度は「やや難〜難」を想定**（質問40〜60回程度）。ミスリードはあるが、後で聞けば納得できるフェアな謎にしてある。
- **回答は「はい」「いいえ」「関係ありません」**が基本。質問が曖昧なときだけ一言補足が入る。
- **30問を超えて行き詰まったら**、ヒントが欲しいか聞いてくれる。
- **正解したら**真相を解説し、続けてもう1問やるか聞いてくれる。

> 謎と回答は日本語・日本の日常的な文脈を前提に生成される。日本語話者向けのスキル。

## 必要な環境

- サブエージェント（`Agent`ツール）が使える環境（Claude Codeなど）。これが真相を出題役自身の思考から隠す仕組みの要。
- サブエージェントが使えない場合でもスキル自体は動くが、その場合は真相がClaudeのthinkingに漏れる可能性がある旨が伝えられる。

## インストール方法

**方法1 — プラグインマーケットプレイスとして**
```bash
claude plugin marketplace add <ユーザー名>/<このリポジトリ名>
claude plugin install umigame-soup-host@<マーケットプレイス名>
```

**方法2 — 手動**
`skills/umigame-soup-host/`フォルダをそのまま自分の`skills/`ディレクトリ（例: `~/.claude/skills/`）にコピーするか、Claude.aiの「Customize > Skills」から`SKILL.md`を直接アップロードする。

## 使い方

Claudeに「ウミガメのスープを出題して」のように頼むだけ。プラグインとしてインストールしていれば`/umigame-soup-host`でも呼び出せる。問題文と「なぜでしょう？」が提示されるので、はい／いいえで答えられる質問を重ねて真相を探ろう。

---

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