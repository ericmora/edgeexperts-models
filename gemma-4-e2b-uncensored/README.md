# Gemma 4 E2B Uncensored

Gemma 4 with 2 billion parameters, uncensored variant, optimized for edge deployment.

## Specs

| Property | Value |
|----------|-------|
| Parameters | 2B |
| Context Window | 8192 tokens |
| Quantization | Q4_K_M |
| License | Gemma |
| Base Model | [TrevorJS/gemma-4-E2B-it-uncensored](https://huggingface.co/TrevorJS/gemma-4-E2B-it-uncensored) |

## Platform Builds

| Platform | Format | Size |
|----------|--------|------|
| macOS | GGUF (llama.cpp/Metal) | ~1.4 GB |
| iOS | CoreML (.mlmodelc) | ~1.5 GB |
| Android | LiteRT-LM (.task) | ~1.3 GB |
| Linux | GGUF (llama.cpp) | ~1.4 GB |

## Export Instructions

### GGUF (macOS/Linux)
```bash
# From Ollama (already in GGUF format)
cp ~/.ollama/models/blobs/sha256-* model.gguf

# Or convert from HuggingFace
python3 -m llama_cpp.convert_hf_to_gguf \
  --model TrevorJS/gemma-4-E2B-it-uncensored \
  --outfile model.gguf \
  --outtype f16
```

### CoreML (iOS)
```bash
# Export to CoreML via optimum-cli
python3 -m optimum.exporters.coreml \
  --model TrevorJS/gemma-4-E2B-it-uncensored \
  --task text-generation \
  model.mlmodelc

# Zip for distribution
zip -r model.mlmodelc.zip model.mlmodelc/
```

### LiteRT-LM (Android)
```bash
HF_TOKEN=$HF_TOKEN litert-torch export_hf \
  --model=TrevorJS/gemma-4-E2B-it-uncensored \
  --output_dir=./ \
  --externalize_embedder \
  --jinja_chat_template_override=litert-community/gemma-4-E2B-it-litert-lm
```

## Usage in EdgeExperts

This model is the default for EdgeExperts. It's automatically downloaded during onboarding.

Users can switch models in Settings > Models.
