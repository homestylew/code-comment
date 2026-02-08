---
name: code-comment
description: Add or improve code comments following language conventions. Triggered when user asks for comments (e.g. add comments, 写注释, document this).
---

# Code Comment

Use this skill **only when the user's input** indicates they want comments: e.g. "add comments", "写注释", "document this", "解释这段代码", "comment this", "补充注释". Do not apply when the user is asking for other changes (refactor, fix bug, etc.) unless they also ask for comments.

**Response must follow user input**: comment language, detail level (brief vs detailed), and scope (selection vs file) should be inferred from what the user said and what they selected.

## Trigger (user input)

- Apply when the user **says** they want comments: in any language (e.g. 加注释 / add comments / document / 解释一下).
- Do **not** apply when the user did not ask for comments.

## Response (follow user input)

Derive these from the **user's message and context**:

| What to decide | How to derive |
|----------------|---------------|
| **Comment language** | Prefer the language of the user's message (e.g. Chinese message → Chinese comments). If unclear, match existing comments in the file. Default to English only if neither applies. |
| **Detail level** | "简单注释" / "brief" / "简要" → minimal (file/function summary only). "详细" / "detailed" / "每行" → more inline explanation. No hint → moderate (public API + non-obvious logic). |
| **Scope** | User selected a range → comment only that range. User said "整个文件" / "whole file" → whole file. Otherwise infer from selection. |

If the user's intent is ambiguous, ask once (e.g. "注释用中文还是英文？" or "要简单注释还是详细注释？").

## Instructions

1. **Identify language** of the target file and open [reference.md](reference.md) for that language's comment format (JSDoc, docstring, Javadoc, etc.). If the language is not listed, use the file's existing comment style or the language's common doc format.
2. **Respect existing style** in the file (same delimiter, indentation, line length). Match existing comment language if present.
3. **Add only comments** — do not change any executable code (no rename, refactor, or logic change). Do not add TODO/FIXME unless the user asks.
4. **Preserve existing comments** — if the file already has comments, keep them unless they are clearly outdated or wrong. Merge new comments with existing ones; do not duplicate. If an existing comment is inaccurate, update it in place.
5. **Comment hierarchy**: file/module summary at top (if appropriate), then class/function doc blocks, then critical inline comments for non-obvious logic. Keep line length reasonable (e.g. 80–100 chars); wrap if needed.
6. **Decorator / annotation placement**: place doc comments **before** decorators or annotations (Python `@decorator`, Java `@Override`, etc.), following each language's convention.
7. **Mixed-language files**: for files with multiple embedded languages (HTML with JS/CSS, Vue SFC, JSX/TSX), use the correct comment syntax for each language section (`<!-- -->` for HTML, `/* */` for CSS, `//` or `/** */` for JS).
8. **Avoid**: comments that only repeat the code; restating type information already expressed in code (TypeScript types, Python type hints, Java generics — focus on semantics/why instead); secrets (keys, passwords); excessive inline noise. See [examples.md](examples.md) for good vs bad.

## When to skip or reduce comments

- Minified/bundled code: skip or minimal.
- Generated code: minimal or skip unless user asks.
- Test files with clear `describe`/`it` names: light comments only.
- Config files (JSON, YAML, .env): only brief inline where needed.
- Trivial functions (getters, setters, simple delegation, one-line lambdas): skip or one-line summary only.

## Quick reference

- Comment formats per language: [reference.md](reference.md)
- Good/bad examples and i18n: [examples.md](examples.md)
