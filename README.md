# DocFila plugins for Claude

Work with your [DocFila](https://www.docfila.com) library and apps from Claude
Code: answer questions from your own contracts, invoices and reports; draft
Word, Excel or PDF files straight into DocFila; revise documents with the
original kept in version history; convert files and edit PDFs; cut videos with
VynCut; make Studio images; and run polls, TimeDeck timers, forms, bookings,
quotes, share links and e-signature requests.

## Install

```
/plugin marketplace add NotaNovice-Group/docfila-claude
/plugin install docfila@docfila
```

Then run `/mcp`, choose **docfila** and sign in with your DocFila account. You
choose what Claude may do: reading is always on; creating and editing, folders,
download links, your DocFila apps and DocFila AI are optional, and "Share and
send" stays off until you tick it.

Prefer an API key? Create one in DocFila and add the server yourself instead:

```
claude mcp add --transport http docfila https://api.docfila.com/claude/mcp \
  --header "Authorization: Bearer dfk_your_key"
```

## What you get

**Connector** — the DocFila MCP server at `https://api.docfila.com/claude/mcp`:

| Area | Tools |
|---|---|
| Library | `search_documents`, `find_documents_by_details`, `list_documents`, `get_document`, `read_document`, `list_folders`, `get_account`, `create_document`, `edit_document`, `create_folder`, `move_documents`, `rename_document`, `get_download_link` |
| Files and media | `convert_document`, `images_to_pdf`, `remove_background`, `split_pdf`, `merge_pdfs`, `stamp_pdf`, `fill_pdf_form`, `get_pdf_job`, `edit_video`, `generate_image` |
| Apps | `list_workspaces`, `get_workspace`, `add_workspace_note`, `add_planner_card`, `update_planner_card`, `request_approval`, `decide_approval`, `create_poll`, `list_polls`, `get_poll_results`, `close_poll`, `create_timer`, `control_timer`, `list_forms`, `get_form_responses`, `get_schedule`, `create_quote`, `list_quotes`, `convert_quote_to_invoice` |
| Share and send | `create_share_link`, `revoke_share_link`, `add_document_to_workspace`, `remove_document_from_workspace`, `set_form_status`, `send_quote_for_approval`, `request_signature`, `get_signature_status` |

**Skills** (used automatically when relevant)

| Skill | For |
|---|---|
| `docfila-library` | Answering questions from your documents, with citations |
| `docfila-drafting` | Writing new docx / xlsx / pdf files into DocFila |
| `docfila-editing` | Safe edits saved as new versions |
| `docfila-paperwork` | Multi-document jobs: extraction to Excel, contract review, comparisons, deadlines |
| `docfila-files-and-media` | Conversions, PDF tools, background removal, Studio images, VynCut video edits |
| `docfila-apps` | Workspaces (notes, Planner, meetings), Polls, TimeDeck, Forms, Schedule, quotes, share links and e-signature |

**Commands**

| Command | Does |
|---|---|
| `/docfila:ask <question>` | Answer from your library with citations |
| `/docfila:find <query>` | List matching documents |
| `/docfila:tidy [scope]` | Propose, then apply, folders and clear names |
| `/docfila:summarize <doc>` | Facts, dates, amounts, obligations |
| `/docfila:draft <what>` | Write and save a new document |
| `/docfila:revise <doc> -- <changes>` | Edit and save a new version |
| `/docfila:extract <docs>` | Pull figures from many documents into Excel |
| `/docfila:review <contract>` | Terms, risks and deadlines |
| `/docfila:deadlines [area]` | Renewals and notice dates, soonest first |
| `/docfila:convert <doc> to <format>` | Convert a document |
| `/docfila:pdf <split\|merge\|stamp\|fill> …` | PDF jobs |
| `/docfila:video <what to make>` | Edit videos with VynCut |
| `/docfila:workspace <name> [: what to add]` | Catch up on a workspace, or add a card or note |
| `/docfila:poll <what for>` | Create a poll |
| `/docfila:timer <agenda>` | TimeDeck timers |
| `/docfila:sign <doc> to <email>` | E-signature request (asks first) |
| `/docfila:connect` | Check or fix the connection |

## Privacy and limits

Claude reaches only what you approved, through DocFila's own services acting
as you, with every plan limit, AI-credit charge and quota applied. It never
deletes documents, and it asks before anything reaches other people. Document text is
marked as untrusted data so instructions hidden in a file are not followed.
Disconnect everywhere at <https://www.docfila.com/claude/connect>. Details:
<https://www.docfila.com/claude> and <https://www.docfila.com/privacy>.

The skills in `skills/` also work in claude.ai: zip a skill folder and upload
it under Settings → Capabilities → Skills, with the DocFila connector added.
