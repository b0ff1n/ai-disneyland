# Textbook library

The learner supplied these four PDFs and requested local versioning and indexing on 2026-10-25. The originals are stored through Git LFS. The indexes are ordinary Markdown and refer to these exact files. Full-text extraction and navigation metadata are also retained in ordinary Git under [extracted/](extracted/README.md), following the [external-memory rules](../MEMORY.md).

## Catalog

| Book ID and index | Verified source | PDF pages | Contents entries |
| --- | --- | ---: | ---: |
| [spivak-calculus-4e](indexes/spivak-calculus-4e.md) | Michael Spivak, *Calculus*, 4th edition, Publish or Perish, 2008 | 699 | 48 |
| [axler-ladr-3e](indexes/axler-ladr-3e.md) | Sheldon Axler, *Linear Algebra Done Right*, 3rd edition, Springer, 2015 | 352 | 148 |
| [dummit-foote-abstract-algebra-3e](indexes/dummit-foote-abstract-algebra-3e.md) | David S. Dummit & Richard M. Foote, *Abstract Algebra*, 3rd edition, Wiley, 2004 | 947 | 124 |
| [kato-kurokawa-saito-number-theory-1](indexes/kato-kurokawa-saito-number-theory-1.md) | *Number Theory 1: Fermat's Dream*, English translation by Masato Kuwata, AMS, Translations of Mathematical Monographs 186 | 157 | 44 |

For *Number Theory 1*, the title page verifies the authors, translator, publisher, and volume. The supplied scan does not include a copyright page, so the edition number, printing, publication year, and ISBN remain unverified. The exact file is identified by its SHA-256, not by assumptions about its long filename.

Spivak and Axler remain the main preparation resources. Abstract algebra and number theory remain lower priorities. Cataloging a book is not evidence that the learner has read or mastered it.

## Using a book

1. Open its index above. The source link points to the unchanged file in `originals/`; the index records its size, SHA-256, and the PDF pages supporting its identity.
2. Find the chapter, section, appendix, or exercise block in the contents table. All entries are starts, not full ranges. Titles follow the supplied contents, with OCR errors and spacing normalized against the source.
3. Use the **physical PDF page**, counting from 1, to read the saved extraction or open the original. Printed page numbers and viewer labels can differ. Axler and *Number Theory 1* have several page-number gaps; their indexes provide piecewise mappings. Some of Spivak's bookmarks are off by one page, and Dummit & Foote's bookmarks are unusable for contents navigation.
4. Read the actual statement and its continuation before quoting, assigning, or discussing a numbered item. Render the page if extraction makes a formula or diagram unclear. The index does not replace this step.
5. Record locators in this form: `axler-ladr-3e, section 3.B, printed p. 59, PDF p. 75`; include the exercise or theorem number after verifying it on the page.

The indexes cover the printed contents: chapters, listed sections and subheadings, appendices, and back matter. Axler and *Number Theory 1* list exercise-block starts in their contents; Spivak and Dummit & Foote require locating the problem/exercise block within the indexed chapter or section. Full extracted text is available separately in [extracted/](extracted/README.md), including page-boundary conventions, navigation formats, and provenance.

Use the saved extraction first; see [how to read a page](extracted/README.md). To re-extract a specific page for comparison, run from the repository root (Spivak, chapter 5, printed p. 90):

```bash
pdftotext -f 109 -l 109 -layout 'library/originals/calculus-4nbsped-0914098918-9780914098911_compress.pdf' -
```

To inspect that page visually, write a temporary render:

```bash
pdftoppm -f 109 -l 109 -singlefile -scale-to 1800 -png 'library/originals/calculus-4nbsped-0914098918-9780914098911_compress.pdf' /tmp/spivak-pdf-109
```

These examples require Poppler tools. Durable full-text extraction, useful OCR results, and navigation metadata belong in tracked `library/extracted/`. Only expendable intermediate files, such as the unannotated page render above, belong in ignored `library/cache/` or a temporary directory. The originals must not be rewritten to add OCR, annotations, or bookmarks as part of reading.

## Git LFS

[Git LFS](https://git-lfs.com/) must be installed on each machine. For this checkout, its filters and hooks were configured with `git lfs install --local`; the repository's `.gitattributes` tracks everything under `library/originals/` as LFS data. Indexes, extraction, navigation metadata, and checksums remain ordinary Git text, available independently of downloading the LFS originals.

In a new checkout, after installing Git LFS, run from the repository root:

```bash
git lfs install --local
git lfs pull
git lfs ls-files
git lfs fsck
```

`git lfs pull` requires a configured remote containing the LFS objects. A local commit alone does not upload them. If transferring this checkout without a remote, preserve its local `.git/lfs/objects/` as well as the Git repository; pointers alone cannot reconstruct the books. With the objects already present locally, `git lfs checkout` restores missing working-tree PDF content from the pointers.

A file beginning with `version https://git-lfs.github.com/spec/v1` is a pointer, not a readable PDF. Restore the LFS content before using the index; if the objects are unavailable, report that limitation rather than changing editions.

To verify the four exact indexed files, run **from the `library/` directory**:

```bash
sha256sum --check SHA256SUMS
```

When a source is replaced, verify its title and copyright pages, rebuild the affected contents/page map and saved extraction, and update [SHA256SUMS](SHA256SUMS) and [the extraction manifest](extracted/manifest.json). A matching title alone does not guarantee matching pagination or exercises.

To add or update a source after explicit authorization, stage the PDF together with its index, checksum, and any changed `.gitattributes`. Check `git lfs ls-files` and `git lfs fsck` before committing. Publishing or pushing requires a separate explicit user request under `AGENTS.md`.
