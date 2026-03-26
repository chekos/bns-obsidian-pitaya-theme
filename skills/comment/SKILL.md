---
name: comment
description: "Add, answer, and resolve [!comment] callouts in Obsidian markdown files. Use when leaving editorial comments on a draft, replying to existing comment threads, resolving addressed feedback, flagging claims that need sources, or reviewing writing with annotations instead of direct edits. Defines the callout format: author, date, text reference, type tags ([edit], [question], [flag]), threading, and resolution."
---

# Comment Callout Convention

This defines how to use `[!comment]` callouts in Obsidian markdown files. These are visible, structured editorial annotations — like Google Docs comments, but in plain markdown.

Use this convention whenever:
- The user asks you to review or give feedback on a document without editing it directly
- The user asks you to respond to comments left in a document
- You need to leave notes, questions, or suggestions on a piece of writing
- The user asks you to annotate, comment on, or flag issues in a draft

## Format

### Basic comment

```markdown
> [!comment]- **@author** · YYYY-MM-DD · re: "referenced text"
> The comment body goes here.
```

| Part | Purpose |
|------|---------|
| `[!comment]-` | Callout type, collapsed by default (`-`) |
| `**@author**` | Who left the comment |
| `YYYY-MM-DD` | Date |
| `re: "..."` | Short excerpt (5-15 words) from the passage being discussed, or a section heading |
| Body | The actual comment — concise and actionable |

### Typed comment

Add a tag before the author to categorize:

```markdown
> [!comment]- [edit] **@author** · YYYY-MM-DD · re: "referenced text"
> The comment body.
```

| Tag | When to use |
|-----|-------------|
| *(none)* | General annotation or note |
| `[edit]` | Suggesting a text change (rephrase, cut, rewrite) |
| `[question]` | Asking for clarification or more information |
| `[flag]` | Marking something that needs attention (missing source, factual concern, etc.) |

## Author

- When you (the AI) are leaving comments, use `**@claude**` (or the appropriate model name)
- When the user's name or handle is known from context (git config, prior conversation, memory), use that for comments attributed to them
- If existing comments are already in the file, follow the author convention already in use

## Placement

- Place comments **directly below** the paragraph or section they reference, after a blank line
- Never insert a comment in the middle of a paragraph
- When commenting on multiple sections, each comment goes after its respective section

## Resolving Comments

When a comment has been addressed, apply strikethrough to the title and body, and add a resolution line:

```markdown
> [!comment]- ~~[flag] **@claude** · 2026-03-25 · re: "performance claims"~~
> ~~This needs a source or benchmark reference.~~
> **Resolved** by @chekos · 2026-03-25
```

## Replying to Comments

Nest replies inside the parent comment using a second blockquote level. Replies use `[!comment]` (no `-`) since they're already inside a collapsed parent:

```markdown
> [!comment]- **@claude** · 2026-03-25 · re: "metrics summary"
> Which metrics are these? Be specific.
>> [!comment] **@chekos** · 2026-03-25
>> Clarified to "monthly active users and retention rate."
```

## Common Workflows

### "Review my draft, don't edit directly"

Read the document. For each issue you find, insert a comment at the relevant location using the appropriate type. After all comments are placed, summarize what you added:

> Added 4 comments to `essay.md`:
> - `[edit]` on "intro paragraph" — tighten opening
> - `[question]` on "methodology" — missing citation
> - `[flag]` on "results" — unsubstantiated claim
> - General on "conclusion" — strong ending, consider expanding

### "Answer the comments in this document"

Read through the document looking for existing `[!comment]` callouts. For each one:
- If it's a question you can answer: add a threaded reply with the answer
- If it's an edit suggestion you agree with: make the edit in the text, then resolve the comment
- If it's a flag: investigate and either resolve it (with explanation) or reply with what you found
- If it needs the user's input: reply explaining what decision is needed

### "Resolve all the comments"

Find all `[!comment]` callouts in the document. For each one, apply the resolution format (strikethrough + resolved-by line). Only resolve comments that have actually been addressed — if the underlying issue hasn't been fixed, leave the comment open and flag it.

## Flexibility

The structured format (`@author · date · re: "text"`) is a convention, not a rigid requirement. A quick `> [!comment] fix this` is perfectly valid. Use the full format when context and attribution matter (reviews, collaboration); use the short form for quick personal notes.
