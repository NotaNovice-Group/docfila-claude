---
name: docfila-files-and-media
description: Convert, combine and transform files in the user's DocFila library — PDF to Word, Excel, CSV, text or images; Word, Excel or PowerPoint to PDF; photos or scans into one PDF; split, merge, stamp or fill PDF forms; remove an image background; generate an image with Studio; or edit videos with VynCut (trim, join, captions, music, looks). Use when the user asks to convert, turn into, export as, combine, split, merge, stamp, fill in, cut out, generate a picture, or edit, trim or caption a video that is in DocFila.
---

# Files and media in DocFila

Every tool here saves its result as a **new document** and returns its `url`.
Originals are never changed. Find the source first with `search_documents`,
`list_documents` or `find_documents_by_details` and use its `id`.

## Conversions — `convert_document`

| From | `to` |
|---|---|
| PDF | `docx` (editable Word, layout reconstructed), `xlsx` / `csv` (tables only), `txt`, `png` / `jpg` (pass `pages`: `"1"`, `"2-4"` or `"all"`; several pages come back as a zip) |
| Word, Excel, PowerPoint | `pdf` |
| Image | `pdf` (for several images use `images_to_pdf`, in the order given) |

- PDF → Excel/CSV only works when the PDF has a real table; a 422 answer means
  none was found. Offer `docx` or `txt` instead.
- Scanned PDFs have no text layer: `txt` may be empty. Say so.
- After converting, offer the link and, if useful, read the result with
  `read_document` to check it.

## PDF tools (jobs)

`split_pdf` (`pages: "1-3,4-6"` → one new PDF per range), `merge_pdfs` (first
ID first), `stamp_pdf` (`text`: PAID, APPROVED, DRAFT…), `fill_pdf_form`
(`fields` keyed by the PDF's own field names; `flatten: true` makes them
permanent). These start a job: call `get_pdf_job` with the `jobId` after a few
seconds, repeat until `status` is `completed` (then give the new document's
link) or report the error.

## Images

- `remove_background`: product photos, portraits, logos → PNG with a
  transparent (default) or `#RRGGBB` background; `quality: "best"` for hair and
  fine edges.
- `generate_image`: write a specific visual brief (subject, style, colours,
  composition, text to include) and pick `aspectRatio` for the destination
  (1:1 social, 9:16 story, 16:9 slide, 4:5 feed). It uses the account's AI
  credits — say so the first time. To change one, generate again with a
  revised brief.

## Video — `edit_video` (VynCut)

- `clips`: up to 12 library videos, played in order. `startSec`/`endSec` trim
  each one (leave `endSec` out to keep the clip to its end); `speed` 0.25–3;
  `look`: vivid, noir, sepia, film, glow, studioPortrait, detailBoost, coolLift.
- `captions`: text with `startSec`/`endSec` in the finished video's time,
  `position` top/middle/bottom, `size` small/medium/large.
- `music`: an audio document and its `volume` (0.6 sits under speech).
- `shape`: 9:16 for Reels/TikTok/Shorts, 1:1 or 4:5 for feeds, 16:9 for
  YouTube and slides. `quality` 720p by default; 1080p for final cuts.
- The finished video is at most 15 minutes. Rendering takes a little while for
  long or high-quality exports.

If a tool says the connection lacks permission, the user can reconnect DocFila
in Claude's connector settings and tick the permission it names.
