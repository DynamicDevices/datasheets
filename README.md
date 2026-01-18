# Datasheets Repository

This repository stores **source datasheets** (usually PDFs) and **multiple conversion outputs** from different processes.

## Critical: do NOT store confidential or NDA material

**Do not add datasheets or documents that are confidential, proprietary, export-controlled, or covered by an NDA** to this repository.
Only store documents that are **publicly distributable**.

## Organization

- Group by **manufacturer** (lowercase): `manufacturers/<manufacturer>/...`
- Group by **document** (prefer document number or short name): `manufacturers/<manufacturer>/<doc-id>/...`

Example:

```
manufacturers/nxp/AN13917/
  source/
  outputs/
    pdftotext/
    pdf2md/
      auto/
      always/
  README.md
```

## What to store per datasheet

- **`source/`**: original datasheet PDF(s)
- **`outputs/pdftotext/`**: baseline extraction (layout-preserving if possible)
- **`outputs/pdf2md/auto/`**: output from pdf2md in auto vision mode
- **`outputs/pdf2md/always/`**: output from pdf2md in always-vision mode

## Future compatibility

Add new converters under `outputs/<converter>/<variant>/` without changing existing layout.

## Notes on large PDFs

If you plan to store many large PDFs, consider enabling Git LFS for `*.pdf`.
