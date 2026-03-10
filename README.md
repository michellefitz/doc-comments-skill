# doc-comments

A skill for [Claude Cowork](https://claude.ai) that generates an interactive HTML tool for annotating any document at the sentence level.

Click a sentence, leave a comment, copy structured feedback back to Claude. Useful for reviewing and iterating on any piece of writing — articles, emails, specs, reports, proposals.

![doc-comments screenshot](<img width="756" height="493" alt="Copy plain teet" src="https://github.com/user-attachments/assets/1c107c05-7f55-4008-b180-05f0de258a00" />)

---

## Install

Download [`doc-comments.skill`](./doc-comments.skill) and open it in Claude Cowork. Click **Copy to your skills** to install.

Once installed, just tell Claude:

> "Generate a doc-comments tool for this draft"
> "I want to annotate this article"
> "Help me mark up this document"

Claude will generate a ready-to-open HTML file loaded with your content.

---

## How it works

When triggered, Claude:

1. Reads your document (from a file, pasted text, or something Claude just wrote)
2. Splits it into paragraphs and builds a JavaScript content array
3. Injects it into the HTML template
4. Saves a `doc-comments.html` file to your workspace

Open it in any browser — no server needed, no dependencies, fully self-contained.

### In the tool

- **Click any sentence** to select it and open a comment input
- **Type your note** and hit Add comment (or Cmd+Enter)
- Commented sentences get an amber underline so you can see what's been annotated
- **Copy feedback for Claude** — formats all your comments as structured text to paste back into the conversation
- **Copy plain text / Markdown / formatted** — copy the document itself in different formats for pasting into Substack, Notion, or anywhere else

---

## Customising

The skill is two files:

- `SKILL.md` — instructions Claude follows to generate the tool
- `assets/template.html` — the HTML file with `__CONTENT_PLACEHOLDER__` and `__DOC_TITLE_PLACEHOLDER__` that Claude fills in

If you want to change the design, edit `template.html`. If you want to change the behaviour (different copy formats, different comment structure, etc.), edit `SKILL.md`. Then repackage using the [skill-creator skill](https://claude.ai).

---

## Built with

Built using Claude Cowork. Originally created as part of a writing workflow for [Michelle's Substack](#) — wrote the first post, needed a better way to give feedback on it, built the tool in the same session.

---

## Licence

MIT
