# EdgeExperts Models

Public repository for LLM models used by [EdgeExperts](https://github.com/ericmora/edgeexperts) — an on-device RAG platform with multi-expert debate.

## Standard Model Structure

Each model follows this directory layout:

```
<model-id>/
├── model.json           # Model metadata (required)
└── README.md            # Documentation
```

Binary files are hosted via **GitHub Releases** (supports files up to 2 GB each). Files are prefixed by platform (`macos-`, `ios-`, `android-`, `linux-`) since GitHub releases are flat (no subdirectories).

## model.json Schema

```json
{
  "id": "gemma-4-e2b-uncensored",
  "name": "Gemma 4 E2B Uncensored",
  "parameters": "2B",
  "contextWindow": 8192,
  "version": "1.0.0",
  "default": true,
  "baseUrl": "https://github.com/ericmora/edgeexperts-models/releases/download",
  "platforms": {
    "macos": {
      "format": "gguf",
      "filename": "macos-model.gguf",
      "sizeBytes": 2963546112,
      "split": true,
      "parts": [
        {"filename": "macos-model-split-00001-of-00003.gguf", "sizeBytes": 43314624}
      ]
    }
  }
}
```

Add a new platform entry per target (macos, ios, android, linux). Use `split: true` + `parts[]` if the file exceeds 2 GB.

## Download URLs

Assets are flat in releases. Platform prefix avoids name conflicts:

```
{baseUrl}/{model-id}-v{version}/{platform}-{filename}
```

Example:
```
https://github.com/ericmora/edgeexperts-models/releases/download/gemma-4-e2b-uncensored-v1.0.0/macos-model-split-00001-of-00003.gguf
```

After download, concatenate split parts in order to reconstruct the model.

## Adding a New Model

1. Create folder `<model-id>/` with `model.json` and `README.md`
2. Export model for each target platform
3. If file > 2 GB, split using `llama-gguf-split --split-max-size 1500M <input> <output-prefix>`
4. Create a GitHub Release tagged `<model-id>-v<version>`
5. Upload platform binaries as release assets (prefix filenames with `macos-`, `ios-`, etc.)
6. Update `model.json` in the repo with correct filenames, sizes, and split info
7. Publish to Firestore via Firebase Console (Web UI) or Admin SDK:
   - Collection: `models`, Document ID: `<model-id>`

## Available Models

| Model | Parameters | Default | Description |
|-------|-----------|---------|-------------|
| [gemma-4-e2b-uncensored](./gemma-4-e2b-uncensored/) | 2B | Yes | Gemma 4 E2B uncensored, optimized for edge |

## License

Individual model licenses apply. See each model's README for details.
