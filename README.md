# Code Comment — AI Agent Skill

An AI agent skill that adds or improves file-, function-, and inline-level comments in code. **Trigger** and **response** are driven by user input: when to run, comment language, detail level, and scope all follow what the user says and selects. Supports mainstream comment conventions (JSDoc, TSDoc, docstring, Javadoc, KDoc, C# XML, Go, Rust, Ruby, PHP, Swift, Dartdoc, and more).

## Features

- **Trigger from user input**: Used only when the user asks for comments (e.g. "add comments", "写注释", "comment this", "解释这段代码").
- **Response from user input**: Comment language matches the user's message (e.g. Chinese message → Chinese comments); detail level follows "brief" vs "detailed"; scope follows selection or "whole file".

## Installation

### Option 1: npx (requires Node.js — common for frontend / full‑stack)

From your project root or any directory:

```bash
npx skills add homestylew/code-comment
```

This installs the skill into your tool’s skills directory (e.g. Cursor).

### Option 2: Manual install (no Node required — e.g. for Java / backend-only)

1. **Get the repo** (choose one):
   - Clone: `git clone https://github.com/homestylew/code-comment.git`
   - Or on GitHub click **Code → Download ZIP**, then extract.
2. **Copy into the skills directory**: Copy the **entire `code-comment` folder** to the path for your tool in the table below.

| Tool | Windows path | macOS/Linux path |
|------|-------------|------------------|
| Cursor (repo) | `repo\.cursor\skills\` | `repo/.cursor/skills/` |
| Cursor (global) | `%USERPROFILE%\.cursor\skills\` | `~/.cursor/skills/` |
| Claude Code (repo) | `repo\.claude\skills\` | `repo/.claude/skills/` |
| Claude Code (global) | `%USERPROFILE%\.claude\skills\` | `~/.claude/skills/` |
| Windsurf (repo) | `repo\.windsurf\skills\` | `repo/.windsurf/skills/` |

**Example commands** (Cursor, global install):

- Windows (PowerShell or CMD):
  ```text
  xcopy /E /I code-comment "%USERPROFILE%\.cursor\skills\code-comment"
  ```
- macOS / Linux:
  ```bash
  cp -R code-comment ~/.cursor/skills/code-comment
  ```

You can also copy the `code-comment` folder to the path above using your file manager.

## Usage and verification

1. Open any code file in your AI coding tool (or select a range).
2. Ask explicitly for comments, for example:
   - English: "add comments", "comment this", "brief comments", "detailed comments"
   - Chinese: "给这个文件加注释", "写一下注释", "简单注释", "详细注释", "整个文件加注释"
3. The agent will follow this skill: use your **language** for comments, **brief/detailed** for depth, and **selection or whole file** for scope, and use the format for that file's language (see reference.md).

Use the language you want for comments in your message; say "brief" or "简单注释" for minimal comments.

## License

MIT (see [LICENSE](LICENSE)).
