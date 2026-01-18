# AN13917 (NXP) – Conversion Comparison

## Critical: public documents only

**Do not store confidential or NDA/proprietary datasheets here.** Only include documents you are allowed to redistribute publicly.

## Conversion metadata (fill this in)

Record exactly what produced the artifacts in this folder so results are reproducible.

- **Date generated**:
- **Source PDF filename**:
- **Source PDF checksum** (recommended):
  - `sha256sum source/<file>.pdf`

### Baseline (`pdftotext`)
- **Tool**: `pdftotext` (poppler)
- **Tool version**: `pdftotext -v`
- **Command used**:
  - Example: `pdftotext -layout source/<file>.pdf outputs/pdftotext/output.txt`

### pdf2md (`auto` / `always`)
- **Tool**: `pdf2md` (this project)
- **Repository**: `DynamicDevices/pdf2md`
- **Git commit** (required):
  - `git -C <path-to-pdf2md> rev-parse HEAD`
- **Any local modifications?** (recommended):
  - `git -C <path-to-pdf2md> status --porcelain`
- **Provider / model** (required):
  - Anthropic: `ANTHROPIC_MODEL_NAME`, `ANTHROPIC_VISION_MODE`, `LLM_PAGE_IMAGE_ZOOM`
  - Gemini: `LLM_MODEL_NAME`, `LLM_VISION_MODE`, `LLM_PAGE_IMAGE_ZOOM`
- **Command used**:
  - Example: `./scripts/convert_pdf_anthropic.sh -i source/<file>.pdf -o outputs/pdf2md/always -w 2 --llm-rps 0.5`

## Source
- Put the original PDF(s) in `source/`.

## Outputs
- **Baseline**: `outputs/pdftotext/`
- **pdf2md auto**: `outputs/pdf2md/auto/`
- **pdf2md always**: `outputs/pdf2md/always/`

## Comparison (fill this in)

### Overall fidelity
- **Completeness**: missing sections/pages?
- **Ordering**: content in the right place?
- **Artifacts**: headers/footers/page numbers removed correctly?

### Tables
- Table structure preserved?
- Column alignment correct?

### Code blocks / commands
- Commands preserved verbatim (no rewrites)?
- Line wrapping issues?

### Figures / diagrams
- Images extracted and linked?
- Captions correct?

### Notes
- Add any known issues and recommended settings here.
