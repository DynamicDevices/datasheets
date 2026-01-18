# pdf2md – always-vision mode

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
  - `ANTHROPIC_VISION_MODE=always` or `LLM_VISION_MODE=always`
- **Rate limiting / retries**:
  - `LLM_RPS`, `LLM_MAX_RETRIES_TEXT`, `LLM_MAX_RETRIES_VISION`, `LLM_MAX_BACKOFF_SECONDS`
- **Command used**:
  - Example: `python pdf2md.py -i source/<file>.pdf -o outputs/pdf2md/always --provider anthropic -w 2 --llm-rps 0.5`
