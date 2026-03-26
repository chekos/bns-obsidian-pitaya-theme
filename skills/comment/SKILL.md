---
name: comment
description: "Insert a structured editorial comment callout into the current Obsidian document. Use when reviewing, editing, or annotating writing — especially when collaborating with AI tools. Supports basic comments, resolved comments, threaded replies, and typed tags ([edit], [question], [flag])."
argument-hint: "[optional: edit|question|flag] <comment text>"
---

# Insert Comment Callout

Add a `[!comment]` callout to an Obsidian markdown document for visible editorial annotations.

## How It Works

When invoked, insert a comment callout at the appropriate location in the document the user is working on. Follow these steps:

### Step 1: Determine comment context

Ask the user (if not already clear from context):

1. **What file?** — Which markdown file to annotate. If the user has been working on a specific file in this session, default to that.
2. **Where?** — Where in the document the comment should go. The user may reference a section heading, a line number, or quote a passage.
3. **What type?** — A plain comment, or a typed one: `[edit]`, `[question]`, or `[flag]`. If the user provided an argument like `/comment edit This needs active voice`, parse the type from the first word.

If the user provided everything inline (e.g., `/comment flag re: "intro" This claim needs a citation`), skip the questions and proceed directly.

### Step 2: Determine the author

Use the following logic to set the `@author` field:

- If a previous comment callout exists in the file, check its author and reuse it if appropriate
- If the user's name or handle is known from context (e.g., git config, prior conversation), use that
- If running as an AI assistant, use `@claude` (or the appropriate model name)
- If uncertain, ask

### Step 3: Build the callout

Use today's date and construct the callout in this format:

**Basic comment:**
```markdown
> [!comment]- **@author** · YYYY-MM-DD · re: "referenced text"
> The comment body goes here.
```

**Typed comment** (when a tag is specified):
```markdown
> [!comment]- [type] **@author** · YYYY-MM-DD · re: "referenced text"
> The comment body goes here.
```

**Rules:**
- Always use `-` (collapsed by default) unless the user asks for expanded
- The `re: "..."` field should quote a short excerpt (5-15 words) from the passage being commented on. If the user pointed to a section heading, use that instead
- Keep the comment body concise and actionable
- Use the current date in `YYYY-MM-DD` format

### Step 4: Insert the comment

Place the callout **directly below** the paragraph or section it references. Do not insert it in the middle of a paragraph — always after a blank line following the target text.

If the user asks to comment on multiple sections, insert each comment after its respective section.

### Step 5: Confirm

After inserting, briefly confirm what was added and where. Example:

> Added a `[flag]` comment on the "methodology" section in `draft.md`.

## Comment Types Reference

| Tag | When to use |
|-----|-------------|
| *(none)* | General annotation or note |
| `[edit]` | Suggesting a text change (rephrase, cut, rewrite) |
| `[question]` | Asking for clarification or more information |
| `[flag]` | Marking something that needs attention (missing source, factual concern, etc.) |

## Resolving Comments

When the user asks to resolve a comment, apply strikethrough to the original comment and add a resolution line:

```markdown
> [!comment]- ~~[flag] **@claude** · 2026-03-25 · re: "performance claims"~~
> ~~This needs a source or benchmark reference.~~
> **Resolved** by @chekos · 2026-03-25
```

## Threading Replies

When the user replies to an existing comment, nest it inside the original using a second blockquote level:

```markdown
> [!comment]- **@claude** · 2026-03-25 · re: "metrics summary"
> Which metrics are these? Be specific.
>> [!comment] **@chekos** · 2026-03-25
>> Clarified to "monthly active users and retention rate."
```

Note: replies use `[!comment]` (no `-`) since they're already inside a collapsed parent.

## Batch Mode

When asked to review an entire document, read through it and insert multiple comments where warranted. Use appropriate types for each. At the end, provide a summary:

> Added 4 comments to `essay.md`:
> - [edit] on "intro paragraph" — tighten opening
> - [question] on "methodology" — missing citation
> - [flag] on "results" — unsubstantiated claim
> - General on "conclusion" — strong ending, consider expanding
