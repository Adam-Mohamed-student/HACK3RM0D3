# HACK3ERMOD3 — Multi-Model AI Chat & Research Toolkit

A self-hostable, open-source AI chat and experimentation project. It provides a browser-based chat interface connected to [OpenRouter](https://openrouter.ai/), plus tools for comparing responses from different language models and experimenting with prompt-processing pipelines.

> **Origin and licensing:** This package includes work from the upstream HACK3ERMOD3 project. Keep the original copyright and attribution notices and the included **AGPL-3.0** license. This repository is not presented as an original implementation by the person uploading it. See the original project links and documentation in the source files.

## What can you do with it?

- **Chat across AI models:** Use an OpenRouter API key to access supported models through one interface.
- **Compare model outputs:** ULTRAPLINIAN runs multiple models and scores their replies; CONSORTIUM combines results through an orchestration process (depending on configured API access).
- **Experiment with prompts:** AutoTune adjusts sampling settings; Parseltongue explores input transformations; STM modules transform output style.
- **Study model behavior:** Feedback and research scripts can help explore response quality, reliability and differences between models.
- **Host your own interface:** Use the single-page app, the Next.js frontend, or an optional Express backend.

Potential uses include AI research, comparing approaches to the same question, experimenting with response formats, and exploring how model settings affect output. **Comparative scores do not guarantee factual accuracy**, and the number or availability of models depends on OpenRouter.

## Get started (easiest option)

You need a modern browser and **your own OpenRouter API key**. OpenRouter/model usage may incur charges.

1. Download or clone this repository.
2. Serve the repository directory with a local web server:

   ```bash
   python -m http.server 8000
   ```

3. Open **http://localhost:8000/index.html**.
4. Open **Settings** in the interface and add your OpenRouter API key.
5. Select a model and start chatting. Try model comparison and optional experiments once standard chat works.

The standalone `index.html` is a separate, single-file version of the interface; its behavior can differ from the React frontend. **Never paste a real API key into source files or commit browser exports to GitHub.**

## Run the Next.js frontend (developers)

Requirements: Node.js 20+ and npm.

```bash
npm ci
npm run dev
```

Open **http://localhost:3000**. Use Settings to supply your OpenRouter API key. The default configuration supports a static export using `npm run build`; deploy the resulting `out/` folder to a static host. If hosting under a GitHub Pages repository subpath, configure `basePath` in `next.config.js` for the repository name and rebuild.

## Optional REST API

The project also includes an Express API server in `api/`, an alternative Hugging Face layout in `HF/`, and experimental/research endpoints. See [API.md](API.md) for endpoint details.

```bash
cp .env.example .env
# Add your actual values to .env, NEVER to .env.example
npm ci
npm run api:dev
```

On Windows PowerShell, use `Copy-Item .env.example .env`. By default, the server listens on **http://localhost:7860**; health check: **GET /v1/health**.

For any public deployment, configure `HACKERMODE_API_KEY` or `HACKERMODE_API_KEYS`, restrict `CORS_ORIGIN`, and apply network/access safeguards. **If no API authentication key is configured, the server allows unauthenticated requests.** A server-side OpenRouter key can incur costs from clients using your server.

A Docker Compose configuration is included, but it has not been validated as part of this cleanup. Review its dependencies and security settings before deploying it.

## Privacy and security: read before use

- **Do not commit** `.env` files, API keys, credentials, browser storage exports, chat history, or real-user research datasets.
- The web interface may keep API keys and conversations in browser **localStorage**. That protects against accidentally including them in this source-code archive, but does not make a shared computer or browser profile safe for secrets.
- The React frontend includes **client-side telemetry code** (`src/lib/telemetry.ts`), and the standalone app may implement tracking separately. Inspect the privacy controls and network requests before using sensitive prompts; this GitHub preparation did **not** disable all telemetry.
- The optional API supports **opt-in dataset publication** to Hugging Face using `HF_TOKEN` and `HF_DATASET_REPO`. Content placed in a public dataset can be copied permanently. Keep the feature disabled unless users understand and consent.
- Calls to external AI providers send selected prompt content to those providers. Do not use real credentials or private material in prompts.
- Treat prompting and model evaluation features as **research tools**, not guarantees that a model will respond correctly or safely.

## Repository layout

| Path | Purpose |
| --- | --- |
| `index.html` | Standalone browser app |
| `src/` | Next.js / React interface, state and prompt-processing modules |
| `api/` | Optional Express REST API |
| `HF/` | Hugging Face API/deployment variant |
| `functions/` | Cloudflare Pages Functions including telemetry proxy |
| `research/` | Evaluation and benchmarking scripts |
| `API.md` | API endpoints and request examples |
| `PAPER.md`, `paper/` | Research write-up and LaTeX materials |
| `TERMS.md`, `SECURITY.md`, `CONTRIBUTING.md` | Policies and contribution guidance |

## Contributing

Open issues for bugs, add reproducible examples, and submit pull requests with clear descriptions. Never include active credentials, user data, or private deployment configurations in bug reports.

## Licensing and credits

This repository contains upstream code released under **AGPL-3.0**. See [LICENSE](LICENSE) and preserve the applicable original notices. Any modifications and redistribution must comply with that license. This README describes how to run and evaluate the existing project and does not imply ownership of its original work.


## Live OpenRouter model catalog (November 2026 update)

The Next.js model picker and the standalone `index.html` ordinary-chat picker now request OpenRouter's live text-model catalog on startup (`GET /api/v1/models?sort=newest&output_modalities=text`). Models are shown in newest-first order; the Next.js picker includes a search box. If the request fails, the built-in model list remains usable. A previously selected model ID is preserved, even if it is no longer offered, so check availability before sending prompts.

This feature does not require putting an API key in source code. An OpenRouter key is still needed to send requests; model availability and usage prices depend on your OpenRouter account. Check model pricing before use. Other modes with fixed sets of models (including multi-model/race and special fallback pipelines) have **not** been automatically rewritten, because their model choices, API parameters, budgets and orchestration must be validated separately. No live API-key integration test was performed.
