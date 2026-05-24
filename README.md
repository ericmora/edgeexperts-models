# EdgeExperts Models

Public repository for LLM models used by [EdgeExperts](https://github.com/ericmora/edgeexperts) — an on-device RAG platform with multi-expert debate.

## Available Models

| Model | Parameters | Format | Description |
|-------|-----------|--------|-------------|
| [gemma-4-e2b-uncensored](./gemma-4-e2b-uncensored/) | 2B | LiteRT-LM | Gemma 4 E2B uncensored, optimized for edge deployment |

## Structure

Each model has its own folder containing:
- `README.md` — Model documentation, export process, usage details
- `model.task` — LiteRT-LM model file (downloaded via app, not in repo)

## Adding a New Model

1. Create a folder: `<model-name>/`
2. Add `README.md` with model details, export instructions, and usage
3. Export the model to LiteRT-LM format using `litert-torch`
4. Register the model in EdgeExperts Firestore `models` collection

## Firestore Schema

```json
{
  "models": {
    "<modelId>": {
      "name": "Gemma 4 E2B Uncensored",
      "folder": "gemma-4-e2b-uncensored",
      "repo": "ericmora/edgeexperts-models",
      "branch": "main",
      "format": "litert-lm",
      "parameters": "2B",
      "contextWindow": 8192,
      "downloadUrl": "https://raw.githubusercontent.com/ericmora/edgeexperts-models/main/gemma-4-e2b-uncensored/model.task",
      "sizeBytes": 0,
      "description": "Gemma 4 E2B uncensored variant for edge deployment",
      "active": true,
      "createdAt": "2026-05-24T00:00:00Z"
    }
  }
}
```

## License

Individual model licenses apply. See each model's README for details.
