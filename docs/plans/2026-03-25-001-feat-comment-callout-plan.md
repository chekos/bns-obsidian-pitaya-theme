---
title: "feat: Add custom [!comment] callout for editorial annotations"
type: feat
status: completed
date: 2026-03-25
---

# feat: Add custom [!comment] callout for editorial annotations

## Overview

Add a visible, structured `[!comment]` callout type to the theme so that authors (human or AI) can leave editorial comments directly in Obsidian documents. This is pure CSS + documentation — no plugins required.

## Problem Frame

When collaborating with AI tools (Claude Code, OpenClaude) on writing, there's no native way to leave **visible, structured comments** in an Obsidian document. The built-in `%%` syntax is invisible in Reading mode, and plugin-based solutions add external dependencies. A custom callout solves this with zero dependencies — it's just markdown that renders beautifully.

## Requirements Trace

- R1. A `[!comment]` callout type with a distinct visual identity (color + icon)
- R2. Color must be visually distinct from the four existing families (slate, sage, amber, red) while fitting the pitaya aesthetic
- R3. Must meet WCAG AA contrast on the theme's dark background (`#121318`)
- R4. Collapsed by default convention (using `-`) so comments don't overwhelm document flow
- R5. README documents the callout with usage examples: basic, resolved, threaded, and typed comments

## Scope Boundaries

- No new CSS files — everything goes in `theme.css`
- No plugin or JavaScript — pure CSS custom callout
- No changes to existing callout styles
- Author/timestamp/reference are markdown conventions documented in the README, not enforced by CSS

## Context & Research

### Relevant Code and Patterns

The theme is a single `theme.css` (353 lines) with one `.theme-dark` root block defining CSS variables. Callout styling uses Obsidian's built-in variable system:

```
--callout-default: 100, 108, 140;   /* slate */
--callout-tip:     139, 170, 144;   /* sage */
--callout-warning: 212, 165, 116;   /* amber */
--callout-error:   212, 118, 118;   /* red */
```

Custom callouts in Obsidian use a selector outside the variable block:
```css
.callout[data-callout="comment"] {
    --callout-color: R, G, B;
    --callout-icon: lucide-icon-name;
}
```

The theme already has component-level CSS after the `.theme-dark` block (scrollbars at line 285, mermaid diagrams at line 304). A comment callout block fits naturally here.

### Color Palette Context

The theme's purple family includes:
- `--color-purple: #B898A5` (italic text — dusty mauve)
- `--code-operator: #B07AFC` (code — vivid purple)
- `--code-tag: #C4A2F5` (code — soft lavender)
- Heading gradient ends at `#B585AD` (H6)

A comment callout should sit in this purple family but be distinct from all of these. Target: a muted lavender that reads as "annotation/meta" rather than "content."

### Obsidian Callout Mechanics

- Custom callouts need only a `data-callout` CSS selector with `--callout-color` (RGB triplet) and `--callout-icon` (Lucide icon ID)
- Unsupported types fall back to the `note` style, so the callout works even without theme CSS — it just won't have custom color/icon
- Foldable: `[!comment]-` collapses by default, `[!comment]+` expands by default

## Key Technical Decisions

- **Color `160, 140, 190`** (muted lavender, ~`#A08CBE`): Sits between the dusty mauve of italic text and the vivid purple of code operators. Reads as "meta/annotation" on the dark background. Contrast ratio against `#121318` is ~7.0:1 (AAA). Distinct from all four existing callout families.
- **Icon `lucide-message-circle`**: Universal "comment" metaphor. Alternatives considered: `message-square` (more chat-like), `pencil-line` (more edit-like). Message-circle is the most recognizable comment icon.
- **Convention over enforcement**: Author, timestamp, and text reference are documented markdown patterns, not CSS-enforced structure. This keeps the callout flexible — a quick `> [!comment] fix this` works just as well as the full structured form.

## Open Questions

### Resolved During Planning

- **Should we add a CSS variable to the `:root` block too?** Yes — add `--callout-comment` alongside the other callout color variables for consistency, even though the `data-callout` selector is what actually applies the color. This lets someone override it via a CSS snippet.
- **Should the comment callout content area have different styling?** No — reuse the existing `--callout-content-background: rgba(0, 0, 0, 0.15)` which applies globally. Keep it consistent.

### Deferred to Implementation

- **Exact contrast ratio**: Verify `#A08CBE` on `#121318` during implementation; adjust if needed to stay above 4.5:1 AA.

## Implementation Units

- [x] **Unit 1: Add comment callout CSS**

  **Goal:** Register the `[!comment]` callout type with custom color and icon in `theme.css`.

  **Requirements:** R1, R2, R3

  **Dependencies:** None

  **Files:**
  - Modify: `theme.css`

  **Approach:**
  - Add `--callout-comment: 160, 140, 190;` to the callout variables block (after line 233, alongside the other `--callout-*` variables) with a comment identifying the color family
  - Add a `.callout[data-callout="comment"]` selector block after the existing component styles, setting `--callout-color` and `--callout-icon`
  - Place the new selector in a clearly commented section (`/* === Comment callout === */`) following the existing section comment pattern (`/* === Callouts === */`, `/* ─── Mermaid diagrams ─── */`)

  **Patterns to follow:**
  - Variable naming: `--callout-comment` matches `--callout-tip`, `--callout-warning`, etc.
  - Section comments: match existing `/* === Section === */` or `/* ─── Section ─── */` style
  - The `data-callout` selector pattern from Obsidian's custom callout documentation

  **Verification:**
  - `theme.css` contains both the variable declaration and the selector
  - No existing styles are modified
  - The RGB values are consistent between the variable and the selector

- [x] **Unit 2: Document comment callout in README**

  **Goal:** Add a section to `README.md` documenting the comment callout with usage examples.

  **Requirements:** R4, R5

  **Dependencies:** Unit 1

  **Files:**
  - Modify: `README.md`

  **Approach:**
  - Add a new `## Comment Callout` section after the existing `Callouts` mention in the Design section, or as a new top-level section before Accessibility
  - Document the structured convention: `[!comment]- **@author** · date · re: "text"`
  - Include examples: basic comment, resolved comment, threaded reply (nested callout), and typed comment tags (`[edit]`, `[question]`, `[flag]`)
  - Keep the README voice consistent — concise, descriptive, no tutorial tone

  **Patterns to follow:**
  - README structure: short sections, tables where appropriate, markdown code blocks for examples
  - Match the existing voice: "A warm, personal, dark writing environment..."

  **Test scenarios:**
  - All markdown examples are valid Obsidian callout syntax
  - Examples demonstrate the collapsed-by-default convention (`-`)

  **Verification:**
  - README contains a comment callout section with at least 4 usage examples
  - Examples use correct Obsidian blockquote/callout syntax

- [x] **Unit 3: Update accessibility table**

  **Goal:** Add the comment callout color to the accessibility contrast table in the README.

  **Requirements:** R3

  **Dependencies:** Unit 1, Unit 2

  **Files:**
  - Modify: `README.md`

  **Approach:**
  - Calculate the contrast ratio of `#A08CBE` on `#121318`
  - Add a row to the accessibility table: `Comment callout (#A08CBE) | X.XX:1 | AA/AAA`
  - If the ratio falls below 4.5:1, adjust the RGB values in Unit 1 accordingly

  **Patterns to follow:**
  - Existing accessibility table format with Element | Ratio | Level columns

  **Verification:**
  - Accessibility table includes the comment callout entry
  - Stated contrast ratio is accurate and meets at least AA

## System-Wide Impact

- **Interaction graph:** None — this is additive CSS with no callbacks or observers
- **Error propagation:** N/A — if the CSS doesn't load, Obsidian falls back to the default `note` callout style (graceful degradation)
- **State lifecycle risks:** None
- **API surface parity:** N/A
- **Integration coverage:** Manual verification in Obsidian — create a test note with all four example types and confirm rendering in both Edit and Reading modes

## Risks & Dependencies

- **Low risk**: If the Lucide icon `message-circle` isn't available in the user's Obsidian version, it falls back to the default callout icon. No broken rendering.
- **Color perception**: The muted lavender may appear too similar to slate on certain displays. If so, bump saturation slightly (e.g., `150, 130, 195`).

## Sources & References

- Obsidian callout documentation: custom callouts use `.callout[data-callout="type"]` with `--callout-color` and `--callout-icon`
- Lucide icon reference: `message-circle` from lucide.dev
- Existing theme: `theme.css` lines 212-233 (callout variables)
