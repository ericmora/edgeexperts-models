# EdgeExperts Models

Public repository for LLM models used by [EdgeExperts](https://github.com/ericmora/edgeexperts) — an on-device RAG platform with multi-expert debate.

## Standard Model Structure

Each model follows this directory layout:

```
<model-id>/
├── model.json           # Model metadata (required)
├── README.md            # Documentation
└── platforms/           # Platform-specific builds
    ├── macos/           # macOS (GGUF for llama.cpp / Metal)
    ├── ios/             # iOS (CoreML .mlmodelc as .zip)
    ├── android/         # Android (TFLite / LiteRT-LM)
    └── linux/           # Linux (GGUF)
```

## model.json Schema

```json
{
  "id": "gemma-4-e2b-uncensored",
  "name": "Gemma 4 E2B Uncensored",
  "description": "Gemma 4 2B parameters uncensored, optimized for edge deployment",
  "parameters": "2B",
  "contextWindow": 8192,
  "quantization": "Q4_K_M",
  "license": "gemma",
  "author": "Google (uncensored variant)",
  "baseUrl": "https://github.com/ericmora/edgeexperts-models/releases/download",
  "version": "1.0.0",
  "default": true,
  "platforms": {
    "macos": {
      "format": "gguf",
      "filename": "model.gguf",
      "sizeBytes": 2963546112,
      "sha256": "",
      "split": true,
      "parts": [
        {"filename": "model-split-00001-of-00003.gguf", "sizeBytes": 42949672},
        {"filename": "model-split-00002-of-00003.gguf", "sizeBytes": 1614807040},
        {"filename": "model-split-00003-of-00003.gguf", "sizeBytes": 1449787392}
      ]
    },
    "ios": {
      "format": "mlmodelc",
      "filename": "model.mlmodelc.zip",
      "sizeBytes": 1500000000,
      "sha256": ""
    },
    "android": {
      "format": "task",
      "filename": "model.task",
      "sizeBytes": 1300000000,
      "sha256": ""
    },
    "linux": {
      "format": "gguf",
      "filename": "model.gguf",
      "sizeBytes": 1400000000,
      "sha256": ""
    }
  }
}
```

## Download URLs

Model binaries are hosted via **GitHub Releases**. The download URL pattern:

Single file:
```
{baseUrl}/{model-id}-v{version}/{platform}/{filename}
```

Split files (when `split: true`):
```
{baseUrl}/{model-id}-v{version}/{platform}/{part-filename}
```

Example:
```
https://github.com/ericmora/edgeexperts-models/releases/download/gemma-4-e2b-uncensored-v1.0.0/macos/model-split-00001-of-00003.gguf
```

After download, concatenate split parts in order to reconstruct the model.

## Adding a New Model

1. Create folder `<model-id>/` with `model.json` and `README.md`
2. Export model for each target platform
3. If file > 2GB, split using `llama-gguf-split --split-max-size 1500M <input> <output-prefix>`
4. Create a GitHub Release tagged `<model-id>-v<version>`
5. Upload platform binaries as release assets
6. Register in EdgeExperts Firestore `models` collection:
```bash
cd catalog && pnpm publish-models
```

## Available Models

| Model | Parameters | Default | Description |
|-------|-----------|---------|-------------|
| [gemma-4-e2b-uncensored](./gemma-4-e2b-uncensored/) | 2B | Yes | Gemma 4 E2B uncensored, optimized for edge |

## License

Individual model licenses apply. See each model's README for details.
