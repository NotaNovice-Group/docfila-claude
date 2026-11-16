---
name: docfila-drafting
description: Create new documents in the user's DocFila library — letters, contracts, CVs, cover letters, reports, meeting notes, invoices, budgets, trackers and tables — as Word (docx), Excel (xlsx), PDF or text files. Use when the user asks to write, draft, generate, make or save a document, spreadsheet or file "to DocFila" or "to my documents", or wants a result kept rather than just shown in chat.
---

# Drafting documents into DocFila

`create_document` saves a new file to the user's library from text you write
and returns its `id` and `url`. It never overwrites anything.

## Choose the format

| The user wants | format | Text layout |
|---|---|---|
| A letter, contract, report, CV, notes — anything they may edit | `docx` | One line per paragraph. `# `, `## `, `### ` start headings. |
| A table, budget, tracker, list of figures | `xlsx` | Rows of tab-separated (or comma-separated) cells. `# Sheet: Name` starts a sheet. Cells starting with `=` are formulas. |
| A fixed, final document to send | `pdf` | Plain text; a clean text PDF is produced. |
| Markdown, CSV, JSON, HTML, plain text | `md`, `csv`, `json`, `html`, `txt` | Saved exactly as written. |

Default to `docx` for prose and `xlsx` for anything tabular, unless the user
asks for something else. PDF output is text-only (no images or custom fonts).

## Write it properly

- Draft the full content first. For anything longer than a few paragraphs, show
  the user an outline or the draft and confirm before saving, unless they asked
  you to just save it.
- Word: no Markdown inside paragraphs (`**bold**` is saved literally). Use a
  heading line instead of bold labels; use separate lines for list items,
  starting them with "• " or "1. ".
- Excel: put a header row first, one record per row, consistent columns. Use
  formulas for totals (`=SUM(B2:B13)`) so the workbook stays live. Keep each
  sheet rectangular.
- Give the document a specific `title` ("Tenancy notice – Flat 4 – March 2027",
  not "Document"), and set `type` when obvious (`letter`, `contract`, `invoice`,
  `report`, `cv`, `other`).
- To file it, call `list_folders` and pass `folderId`, or `create_folder` first
  if the user asks for a new folder (needs the "Organise your library" permission).
- If a call might be retried, pass the same `idempotencyKey` so no duplicate is
  created.

## After saving

Reply with the title and the `url` so the user can open it in DocFila, and say
what format it was saved in. If the tool says the connection lacks permission,
explain that the user can disconnect and reconnect DocFila in Claude's connector
settings and allow "Create documents and save edits".
