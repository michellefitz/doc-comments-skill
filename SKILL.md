---
name: doc-comments
description: >
  Generates an interactive HTML tool for annotating any document at the sentence level.
  Use this skill whenever a user wants to review, comment on, or give inline feedback on
  a piece of writing — articles, emails, reports, proposals, specs, or any text document.
  Triggers on phrases like "review this doc", "annotate this", "I want to comment on this",
  "help me mark up this document", "leave feedback on this writing", or any time a user
  has a piece of text they want to comment on sentence by sentence.
  Also useful when iterating on writing with Claude — generate the tool so the user can
  click specific sentences and describe what they want changed, then paste the structured
  feedback back into the conversation.
---

# Doc Comments Skill

This skill generates a self-contained interactive HTML file that lets the user annotate any
document at the sentence level — clicking individual sentences to leave comments, then copying
structured feedback to paste back to Claude.

## What it produces

A single HTML file (`doc-comments.html`) saved to the user's workspace. When opened in a browser it shows:

- The document text with each sentence individually clickable
- A comment sidebar where selected sentences get annotated
- A button to copy all feedback as structured text for Claude
- Buttons to copy the document as plain text, Markdown, or formatted HTML

## How to generate it

### Step 1 — Get the document content

The content can come from:
- A file in the workspace (read it)
- Text pasted directly in the conversation
- Something Claude has just written

### Step 2 — Split into paragraphs

Split the content into an array of paragraph strings. Each paragraph becomes one entry. Strip
any metadata headers (like `# Title` lines) or annotation notes — keep only the prose body.

### Step 3 — Build the JavaScript array

Create a properly escaped JavaScript array string. Each paragraph string must:
- Use double quotes
- Escape any internal double quotes as `\"`
- Escape any backslashes as `\\`
- Preserve em-dashes (—) and other unicode as-is (the HTML is UTF-8)

### Step 4 — Inject into the template

1. Read the template from `assets/template.html` (relative to this skill's directory)
2. Replace `__CONTENT_PLACEHOLDER__` with your JavaScript array string
3. Replace `__DOC_TITLE_PLACEHOLDER__` with a short title reflecting the document
   (e.g. "Q3 Strategy Doc", "Product Spec — Search", "Article Review")

### Step 5 — Save and present

Save the result to the user's workspace folder as `doc-comments.html`.

Then present the file using the `present_files` tool so the user gets a clickable link.

Remind the user:
- Open the file in their browser
- Click any sentence to add a comment
- Use Cmd+Enter to save a comment quickly
- Hit "Copy feedback for Claude" when done and paste it back into the chat

## Tips

- Strip title lines (e.g. `# Document Title`) from the paragraphs array but use the title
  to set `__DOC_TITLE_PLACEHOLDER__`
- Paragraph splits should follow the original paragraph breaks — don't re-split long paragraphs
  into sentences; the tool handles sentence-level splitting internally
- When the user pastes back structured feedback, it arrives as:
  `"[sentence text]"\n→ [their note]` — use this to make targeted edits to the document
