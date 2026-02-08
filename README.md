# Code Comment — AI Agent Skill

An AI agent skill that adds or improves file-, function-, and inline-level comments in code. **Trigger** and **response** are driven by user input: when to run, comment language, detail level, and scope all follow what the user says and selects. Supports mainstream comment conventions (JSDoc, TSDoc, docstring, Javadoc, KDoc, C# XML, Go, Rust, Ruby, PHP, Swift, Dartdoc, and more).

## Features

- **Trigger from user input**: Used only when the user asks for comments (e.g. "add comments", "写注释", "comment this", "解释这段代码").
- **Response from user input**: Comment language matches the user's message (e.g. Chinese message → Chinese comments); detail level follows "brief" vs "detailed"; scope follows selection or "whole file".
- **Multi-language formats**: See [reference.md](reference.md) for JavaScript/TypeScript, Python, Java, Kotlin, C#, Go, Rust, C/C++, Ruby, PHP, Swift, Objective-C, SQL, Shell, HTML/XML, CSS/SCSS, Dart, Lua, Scala, YAML, and more.
- **Good/bad examples**: See [examples.md](examples.md) to avoid redundant or noisy comments.

## Installation

Copy the entire `code-comment` folder into the skills directory of your AI coding tool:

| Tool | Windows path | macOS/Linux path |
|------|-------------|------------------|
| Cursor (repo) | `repo\.cursor\skills\` | `repo/.cursor/skills/` |
| Cursor (global) | `%USERPROFILE%\.cursor\skills\` | `~/.cursor/skills/` |
| Claude Code (repo) | `repo\.claude\skills\` | `repo/.claude/skills/` |
| Claude Code (global) | `%USERPROFILE%\.claude\skills\` | `~/.claude/skills/` |
| Windsurf (repo) | `repo\.windsurf\skills\` | `repo/.windsurf/skills/` |
| Other tools | Refer to the tool's documentation for the skills directory location. |

Example (Windows, Cursor global):

```text
xcopy /E /I code-comment "%USERPROFILE%\.cursor\skills\code-comment"
```

Or copy the `code-comment` folder manually to the appropriate path above.

## Usage and verification

1. Open any code file in your AI coding tool (or select a range).
2. Ask explicitly for comments, for example:
   - English: "add comments", "comment this", "brief comments", "detailed comments"
   - Chinese: "给这段加注释", "写一下注释", "简单注释", "详细注释", "整个文件加注释"
3. The agent will follow this skill: use your **language** for comments, **brief/detailed** for depth, and **selection or whole file** for scope, and use the format for that file's language (see reference.md).

Use the language you want for comments in your message; say "brief" or "简单注释" for minimal comments.

## Files

| File            | Description |
|-----------------|-------------|
| **SKILL.md**    | Main instructions: trigger, response rules (language/detail/scope), and edge cases. |
| **reference.md**| Comment format quick reference for supported languages. |
| **examples.md** | Good vs bad comments, i18n and detail/scope examples. |

## License

MIT (see [LICENSE](LICENSE)).
