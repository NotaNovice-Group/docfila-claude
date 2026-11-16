---
name: docfila-editing
description: Revise an existing document in the user's DocFila library and save it as a new version — fix wording, update dates or amounts, translate, rewrite a section, correct a spreadsheet's values, or apply review comments. Use when the user asks to edit, change, update, correct, rewrite or translate a document that is already in DocFila.
---

# Editing a DocFila document safely

`edit_document` replaces a document's text with the complete text you send and
saves it as a **new version**; the previous file stays in version history. It is
not a patch: whatever you leave out is removed. Follow these steps exactly.

## 1. Read all of it

Call `read_document` from `offset: 0` and keep calling with `offset: nextOffset`
until there is no next chunk. Join the chunks' `text` in order. Keep the
`contentHash` returned with the read — the edit needs it, and it proves the
document has not changed since you read it.

## 2. Change only what was asked

Work on the joined text and keep its layout line for line:

- **Word**: one line per paragraph; table rows are tab-separated cells. Keep the
  same number of table rows and cells — rows and cells cannot be added or
  removed. Paragraph formatting, styles and images are kept by line position,
  so do not merge, split or reorder lines unless asked.
- **Excel**: keep every `# Sheet: <name>` line and each sheet's rows and
  columns; change cell values or formulas only. Sheets cannot be added,
  removed or renamed.
- **PowerPoint**: keep every `# Slide N` line and the line structure of each
  slide; change text only.
- **Text files** (md, txt, csv, json, html, code): any change is fine.
- **PDF**: the result becomes a new text-only PDF without the original layout.
  Tell the user this before saving and offer to create a Word document instead.
- Images cannot be edited.

## 3. Confirm, then save

Show the user a short summary of the changes (or the changed passages) and, for
anything beyond a trivial fix, wait for their go-ahead. Then call
`edit_document` with `id`, the complete `text`, `expectedContentHash` from the
read, and a short `changeDescription` ("Updated rent to €1,250 from April").

## 4. Check the result

- `changed: false` means the text matched; nothing was saved.
- `textMatchesRequest: false` means some lines were kept as they were (for
  example a line that held a picture); read the document again and tell the user.
- A "read it again" / version-conflict error means the document changed: read it
  again from the start and redo the edit — never resend the old text.
- Give the user the `url` and the new `versionNumber`.

To keep the original untouched and make a separate copy instead, read the
document and use `create_document` with the edited text.
