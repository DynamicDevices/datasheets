# pdf2md – auto mode

## Conversion metadata (fill this in)

- **Date generated**:
- **pdf2md repo**: `DynamicDevices/pdf2md`
- **pdf2md git commit**:
  - `git -C <path-to-pdf2md> rev-parse HEAD`
- **Any local modifications?**:
  - `git -C <path-to-pdf2md> status --porcelain`
- **Provider / model**:
  - Anthropic: `ANTHROPIC_MODEL_NAME`
  - Gemini: `LLM_MODEL_NAME`
- **Vision mode**:
  - `ANTHROPIC_VISION_MODE=auto` or `LLM_VISION_MODE=auto`
- **Rate limiting / retries**:
  - `LLM_RPS`, `LLM_MAX_RETRIES_TEXT`, `LLM_MAX_RETRIES_VISION`, `LLM_MAX_BACKOFF_SECONDS`
- **Command used**:
  - Example: `python pdf2md.py -i source/<file>.pdf -o outputs/pdf2md/auto --provider anthropic -w 2 --llm-rps 0.5`

---
## Run metadata (generated)
- Date: 2026-01-18T21:31:55+00:00
- Source: /data_drive/dd/pdf2md/datasheets/manufacturers/nxp/AN13917/source/AN13917.pdf
- pdf2md commit: 77de58c3b175fb8ba134b656b385f899116e25b4
- pdf2md dirty files: 2
- Provider: anthropic
- Vision mode: auto
- LLM_RPS: 0.5
- Workers: 2
- Command: python pdf2md.py -i "/data_drive/dd/pdf2md/datasheets/manufacturers/nxp/AN13917/source/AN13917.pdf" -o "/data_drive/dd/pdf2md/datasheets/manufacturers/nxp/AN13917/outputs/pdf2md/auto" -p prompt.txt -w 2 --provider anthropic (with vision=auto)
