# Gemma 4 E2B Uncensored

## Overview

Gemma 4 E2B (2B parameters) uncensored variant, optimized for edge deployment via LiteRT-LM format. This model runs fully on-device with no cloud dependency.

## Model Details

| Property | Value |
|----------|-------|
| Base model | `TrevorJS/gemma-4-E2B-it-uncensored` |
| Parameters | 2B |
| Format | LiteRT-LM (.task) |
| Quantization | Default (FP16) |
| Context window | 8192 tokens |
| Source | HuggingFace → LiteRT export |

## Export Process

```bash
# Install LiteRT tools
uv tool install litert-torch-nightly

# Export from HuggingFace
HF_TOKEN=$HF_TOKEN litert-torch export_hf \
  --model=TrevorJS/gemma-4-E2B-it-uncensored \
  --output_dir=models/gemma4-e2b-uncensored \
  --externalize_embedder \
  --jinja_chat_template_override=litert-community/gemma-4-E2B-it-litert-lm
```

## Usage in EdgeExperts

This model is loaded by the native backend (MLX on Apple, LiteRT on other platforms) for on-device LLM inference. It powers:
- Chat with experts (RAG-augmented responses)
- Forum debate (multi-expert discussion)
- Follow-up questions on debate results

## Files

| File | Description |
|------|-------------|
| `model.task` | LiteRT-LM model file (download separately) |
| `README.md` | This documentation |

> **Note:** The `model.task` file is not included in this repository due to size. It must be exported using the process above or downloaded from the EdgeExperts app's Models section.

## License

This model is derived from Gemma 4, subject to Google's Gemma Terms of Use. The uncensored variant is provided by TrevorJS on HuggingFace.
