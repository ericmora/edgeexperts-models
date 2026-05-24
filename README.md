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
      "sizeBytes": 1400000000,
      "sha256": ""
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

```
{baseUrl}/{model-id}-v{version}/{platform}/{filename}
```

Example:
```
https://github.com/ericmora/edgeexperts-models/releases/download/gemma-4-e2b-uncensored-v1.0.0/macos/model.gguf
```

## Adding a New Model

1. Create folder `<model-id>/` with `model.json` and `README.md`
2. Export model for each target platform
3. Create a GitHub Release tagged `<model-id>-v<version>`
4. Upload platform binaries as release assets
5. Register in EdgeExperts Firestore `models` collection

## Available Models

| Model | Parameters | Default | Description |
|-------|-----------|---------|-------------|
| [gemma-4-e2b-uncensored](./gemma-4-e2b-uncensored/) | 2B | Yes | Gemma 4 E2B uncensored, optimized for edge |

## License

Individual model licenses apply. See each model's README for details.
