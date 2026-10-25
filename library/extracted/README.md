# Persistent textbook extraction

This directory is part of the repository's [external memory](../../MEMORY.md). Its text and JSON files are tracked in **ordinary Git** so another machine can use the existing extraction immediately after obtaining the Git history. The source PDFs are tracked separately through Git LFS.

The extraction was produced and indexed on 2026-10-25, then preserved here at the learner's explicit request. Text and raw navigation files were copied byte for byte from the original extraction. [manifest.json](manifest.json) records the source paths and SHA-256 hashes, PDF page counts, extraction options, and the sizes and SHA-256 hashes of all data files. All paths in the manifest are relative to the repository root.

| Book ID | Full text | PDF pages |
| --- | --- | ---: |
| spivak-calculus-4e | [full.txt](spivak-calculus-4e/full.txt) | 699 |
| axler-ladr-3e | [full.txt](axler-ladr-3e/full.txt) | 352 |
| dummit-foote-abstract-algebra-3e | [full.txt](dummit-foote-abstract-algebra-3e/full.txt) | 947 |
| kato-kurokawa-saito-number-theory-1 | [full.txt](kato-kurokawa-saito-number-theory-1/full.txt) | 157 |

## Files inside each book directory

- `full.txt`: complete UTF-8 output of Poppler `pdftotext -layout`. A form feed (`\f`, U+000C) ends each physical PDF page, including the last page. Empty pages are retained. Splitting on `\f` yields one entry per PDF page plus a final empty entry. Page N is entry N-1; no printed-page offset is involved.
- `front-20.txt`: the same extraction for the first 20 physical PDF pages, including covers and any text beyond the front matter.
- `outline.json`: raw flattened PDF bookmarks as arrays `[depth, title, physical_pdf_page]`, with zero-based nesting depth and one-based destination page; `null` means the destination could not be resolved. An empty array means no bookmarks were extracted. These bookmarks are **not verified contents**: Dummit & Foote has broken destinations and Spivak has some incorrect targets, as documented in their indexes.
- `page-labels.json`: the PDF's own label for each page, in physical page order. Array index N-1 describes PDF page N. These labels are not necessarily printed page numbers; Spivak and Dummit & Foote use physical numbers as labels.
- `contents.json`: the structured data underlying the checked Markdown index. Each entry has `entry`, `title`, `printed`, and `pdf`; `pdf` is one-based, and `printed` is `null` when the printed contents provides no page number. Entries give starting pages only.

The extraction preserves the source's existing OCR and font-mapping defects. In particular, Axler's output contains control characters where some mathematical glyphs could not be mapped correctly; these bytes were retained rather than silently guessed or removed. Rendering the original remains necessary for ambiguous formulas, diagrams, and exact exercise statements. Git attributes preserve LF endings and allow the layout whitespace of these raw text files.

## Reading a page without repeating extraction

Run from the repository root (Spivak, physical PDF page 109):

```bash
python3 - <<'PY'
from pathlib import Path
pages = Path('library/extracted/spivak-calculus-4e/full.txt').read_text(encoding='utf-8').split('\f')
print(pages[109 - 1])
PY
```

Search a book with `rg`, then use its checked index and page boundaries to locate the passage. Always verify a numbered exercise or theorem against the original PDF before assigning or quoting it, following `AGENTS.md`.

## Maintaining this data

Keep useful extraction, OCR improvements, and source metadata here in Git. Do not move the only copy into `/tmp` or an ignored cache. Temporary, unannotated page renders are expendable; useful annotations and verification findings belong in tracked records.

When a PDF changes, verify its edition and source hash, regenerate the affected full text and navigation from that exact file, review its contents and page mapping, and update the manifest and Markdown index together. Record the tool and options used. A text extraction can be regenerated with `pdftotext -layout INPUT.pdf OUTPUT.txt`; the 20-page excerpt uses `-f 1 -l 20 -layout`. Extraction does not require or authorize modifying the original PDF.

Before committing an update, verify the manifest's source and data hashes, the full-text page count against the PDF count, and agreement between `contents.json` and the Markdown index. Stage the extraction and its metadata in the same authorized commit.
