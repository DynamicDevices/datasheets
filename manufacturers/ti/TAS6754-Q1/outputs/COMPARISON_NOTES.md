# TAS6754-Q1 outputs — pdftotext vs pdf2md (quick comparison)

This file summarizes the tradeoffs between the two output variants stored under this directory:

- `pdftotext/`: raw baseline text (`pdftotext -layout`)
- `pdf2md/auto/`: structured Markdown produced by `pdf2md` (LLM-cleaned), with images and verbatim table blocks

## Summary (which is “better”?)

- **For embedded correctness (tables/figures) + navigation + AI consumption**: **`pdf2md/auto/` is better**
- **For cheapest, fastest, “good enough” searchable text**: **`pdftotext/` is better**

## Measured signals for this document

### `pdf2md/auto/`

- **Structure**: `index.md` present and link-valid (no missing targets)
- **Markdown sections**: 154 `.md` files
- **Images**: 148 `.png` files referenced from Markdown
- **Tables**: 210 verbatim table blocks (look for `<!-- VERBATIM_TABLE_START --> ... <!-- VERBATIM_TABLE_END -->`)
- **Text artifacts**: no obvious HTML entity leakage patterns like `&amp;#...` detected in the `.md` outputs

### `pdftotext/`

- **Single-file output**: `pdftotext/output.txt`
- **No images** (figures/tables are not represented as images)
- **Tables**: preserved only as layout-ish text; not reliably machine-parseable and often lossy for specs

## Recommended usage

- Use `pdftotext/` as the **baseline reference** (cheap diff anchor, quick grepping).
- Use `pdf2md/auto/` as the **primary “working” output** when you care about:
  - accurate tables/specs
  - navigable sections
  - embedded/AI workflows

## Context for future comparisons (how to update this file)

This note is intended to be **repeatable** across future converter changes. When you re-run the conversion (or update outputs), refresh this file by re-checking:

- **Index integrity**: `pdf2md/auto/index.md` links resolve to real files.
- **Table fidelity signal**: count of `<!-- VERBATIM_TABLE_START -->` blocks in `pdf2md/auto/*.md`.
- **Image coverage**: number of `pdf2md/auto/images/*.png` and number of in-markdown `./images/...` references.
- **Text artifact scan**: check for common entity leakage patterns (e.g. `&amp;#...`).
- **Baseline size**: line/char counts of `pdftotext/output.txt` (helps spot extraction regressions).

Example (run from the `pdf2md` repo root):

```bash
DOC_DIR="datasheets/manufacturers/ti/TAS6754-Q1"

# Baseline size signal
wc -l -c "$DOC_DIR/outputs/pdftotext/output.txt"

# pdf2md section + asset counts
ls -1 "$DOC_DIR/outputs/pdf2md/auto"/*.md | wc -l
ls -1 "$DOC_DIR/outputs/pdf2md/auto/images"/*.png | wc -l

# Verbatim table marker count
rg -c "VERBATIM_TABLE_START" "$DOC_DIR/outputs/pdf2md/auto"/*.md | awk '{s+=$1} END{print s}'

# Entity leakage scan (should be 0 or explain why)
rg -n "&amp;#|&#" "$DOC_DIR/outputs/pdf2md/auto"/*.md || true
```

