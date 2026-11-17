# OpenRouter model catalog update (2026-11-15)

- Next.js ordinary-chat model selector now loads current OpenRouter models, newest first, with search and offline fallback.
- Standalone `index.html` ordinary-chat selector refreshes available models without exposing credentials or losing the saved selection.
- Next.js/HF shared `getModels()` helpers now request the current text-model catalog and validate the response.
- No fixed model ID has been invented as the “latest”; OpenRouter returns whatever is currently available.
- Special multi-model/race, scoring, and fallback lists have **not** been updated automatically. They need model-by-model review for parameters, pricing, and functionality.
- This is a static source edit. No live paid request or end-to-end integration test was performed.
- OpenRouter catalog docs: https://openrouter.ai/docs/api/api-reference/models/get-models
