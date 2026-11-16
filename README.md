<div align="center">

```text
╔════════════════════════════════════════════════════════════════════╗
║                                                                    ║
║                     H A C K 3 R M 0 D 3                            ║
║                                                                    ║
║           ░▒▓█  LIBERATED AI. COGNITION WITHOUT CONTROL.  █▓▒░     ║
║                                                                    ║
╚════════════════════════════════════════════════════════════════════╝
```

# HACK3RM0D3

**One interface. Many models. A playground for AI experimentation.**

An open-source, self-hostable multi-model AI chat and research toolkit powered by [OpenRouter](https://openrouter.ai/). Chat with different AI models, compare their responses, experiment with model parameters, and explore AI behavior in one place.

[![License: AGPL-3.0](https://img.shields.io/badge/License-AGPL--3.0-22c55e?style=for-the-badge)](LICENSE)
[![OpenRouter](https://img.shields.io/badge/Models-OpenRouter-6366f1?style=for-the-badge)](https://openrouter.ai/)
![Self-hostable](https://img.shields.io/badge/Deploy-Self--hosted-0ea5e9?style=for-the-badge)
![Status](https://img.shields.io/badge/Build-Experimental-f59e0b?style=for-the-badge)

**[Features](#-features) · [Quick start](#-quick-start) · [Model catalog](#-openrouter-model-catalog) · [How it helps](#-why-use-hack3rm0d3) · [Privacy](#-privacy--security) · [Docs](#-documentation)**

</div>

---

## ⚡ At a glance

| | |
|---|---|
| **Multi-model chat** | Access supported AI models through OpenRouter using your own key. |
| **Live model discovery** | Browse a current, searchable catalog in the Next.js frontend; the standalone app also refreshes its ordinary-chat list. |
| **Model comparison** | Evaluate different answers using multi-model research and orchestration modes. |
| **Prompt experiments** | Explore adaptive parameters, transformations, and output formatting modules. |
| **Flexible deployment** | Run a standalone HTML app, a Next.js frontend, or an optional Express API. |
| **Local-first history** | Browser-side storage for chat history and settings; review privacy caveats below. |

## ✨ Features

### 🧠 Chat with different AI models

Choose from models available to your OpenRouter account, including offerings from major AI providers. The ordinary-chat model picker now retrieves a **live text-model catalog**, so newly listed models can appear without editing a hardcoded array.

### ⚔️ Compare responses

- **hackermode CLASSIC:** A preset multi-model prompt-and-response comparison workflow.
- **ULTRAPLINIAN:** Tier-based parallel model evaluation with a composite response score.
- **CONSORTIUM:** A separate model-orchestration and synthesis workflow in the supported API/frontend paths.

Scores are experimental comparisons, **not proof that an answer is true**. Multi-model modes may use several paid API calls for one question.

### 🧪 Experiment with model behavior

- **AutoTune:** Context-sensitive generation settings, including feedback-based adjustment.
- **Parseltongue:** Input transformation and robustness-testing techniques.
- **STM (Semantic Transformation Modules):** Output-style transformations, including direct-answer formatting and hedge reduction.
- **Research scripts:** Evaluation and analysis utilities in `research/`.

### 🎨 Built for exploration

The standalone interface includes themed UI options, responsive layouts, chat history controls, and hidden extras. The Next.js interface offers a separate React-based experience, so features can differ between the two.

---

## 🚀 Quick start

### Option A — Run the standalone app (simplest)

**You need:** a modern browser, Python (or another local static server), and an [OpenRouter API key](https://openrouter.ai/keys).

```bash
# Clone your fork/repository (replace the URL with your own)
git clone https://github.com/YOUR_USERNAME/YOUR_REPOSITORY.git
cd YOUR_REPOSITORY

# Serve the project locally
python -m http.server 8000
```

Open **http://localhost:8000/index.html**, then:

1. Open **Settings**.
2. Enter your own OpenRouter API key.
3. Choose a model from the model selector.
4. Start a conversation, or try the experimental modes.

> [!TIP]
> This version requires **no frontend build step**. You can also deploy `index.html` on a static web host. Using a local server is usually more reliable than opening the file directly.

### Option B — Run the Next.js app

**You need:** Node.js 20+ and npm.

```bash
npm ci
npm run dev
```

Open **http://localhost:3000**, add your API key in Settings, and choose a model. To create a static production export:

```bash
npm run build
```

The exported site is written to `out/`. For a GitHub Pages repository subpath, update `basePath` in `next.config.js` first and rebuild.

### Option C — Run the optional REST API

The repository also contains an Express API in `api/` and an alternate `HF/` variant.

```bash
# macOS / Linux
cp .env.example .env

# Windows PowerShell:
# Copy-Item .env.example .env

# Edit .env with your own settings, then:
npm ci
npm run api:dev
```

Default address: **http://localhost:7860**  
Health endpoint: **`GET /v1/health`**  
Full endpoints and examples: **[API.md](API.md)**

> [!WARNING]
> **Before exposing the API publicly:** configure `HACKERMODE_API_KEY` or `HACKERMODE_API_KEYS`, restrict `CORS_ORIGIN`, and add appropriate network protections. Without API authentication configured, the server can accept unauthenticated requests. A server-side OpenRouter key can incur usage charges.

---

## 🔄 OpenRouter model catalog

**Updated November 15, 2026.** Regular chat no longer has to rely exclusively on the original fixed model list.

```text
OpenRouter model catalog
          │
          ▼
Fetch currently listed text-capable models
          │
          ├── Success → display current models, newest first
          │                 └── Search by name/provider (Next.js)
          │
          └── Failure → fall back to bundled model choices
```

The standalone `index.html` and the Next.js ordinary-chat selector support catalog refreshes. Existing model selections are preserved where possible, but an old saved model might no longer be available. **Special model-race, scoring, and orchestration presets still use their own selections**; those were not automatically migrated.

See **[OPENROUTER_UPDATE_NOTES.md](OPENROUTER_UPDATE_NOTES.md)** for the exact scope and limitations. Model pricing, account permissions, and support for particular request parameters can change; verify them before running large comparisons.

## 💡 Why use HACK3RM0D3?

| Use case | How this project helps |
|---|---|
| **Students and learners** | Compare different explanations of a concept and spot where models disagree. |
| **Developers** | Experiment with model behavior, sampling parameters, and API workflows. |
| **Researchers** | Explore prompt transformations, output processing, and model comparisons. |
| **AI enthusiasts** | Try multiple providers from one customizable interface. |
| **Self-hosters** | Keep control of deployment and inspect the application source code. |

**Remember:** Model outputs can be inaccurate, and OpenRouter requests may cost money even when the interface itself is self-hosted.

---

## 🛡️ Privacy & security

The project is open-source and can be self-hosted, but **self-hosted does not mean entirely offline or automatically private**.

- **Your API key:** Enter it through the app's settings; do not hardcode it into files or commit it to GitHub. The browser interface can keep keys in `localStorage`.
- **Your conversations:** Chat history may be stored in the browser. Clearing browser storage can delete it; use the application's export/import controls if you need backups.
- **Third-party model providers:** Requests sent through OpenRouter are processed by external services under their respective policies.
- **Telemetry:** The frontend contains client-side telemetry functionality. Inspect the controls and network calls before entering sensitive content; this distribution does **not** claim telemetry is globally disabled.
- **Public research dataset:** The optional API includes an **opt-in** Hugging Face dataset publishing feature. If enabled, user inputs and model outputs may become publicly accessible. Automatic redaction cannot be guaranteed to remove all private information.
- **Repository hygiene:** `.gitignore` covers common local secrets and generated files; **always review `git diff --cached` before publishing**.

Read **[TERMS.md](TERMS.md)**, **[SECURITY.md](SECURITY.md)**, and **[GITHUB_SECURITY_REVIEW.md](GITHUB_SECURITY_REVIEW.md)** before sharing or deploying the project.

## 🗂️ Repository structure

```text
HACK3RM0D3/
├── index.html                   # Standalone browser interface
├── src/                         # Next.js / React application
├── public/                      # Static assets
├── api/                         # Optional Express API
├── HF/                          # Hugging Face deployment variant
├── functions/                   # Cloudflare-related functions
├── research/                    # Evaluation and experiment scripts
├── paper/                       # Research paper sources
├── API.md                       # API documentation
├── OPENROUTER_UPDATE_NOTES.md   # Model-catalog changes
├── GITHUB_SECURITY_REVIEW.md    # Publication security checklist
├── TERMS.md                     # Data-handling terms
├── SECURITY.md                  # Security guidance
├── CONTRIBUTING.md              # Contribution guidance
└── LICENSE                      # AGPL-3.0 license
```

## 📚 Documentation

| Document | What you'll find |
|---|---|
| [API.md](API.md) | Server API details and usage examples |
| [OPENROUTER_UPDATE_NOTES.md](OPENROUTER_UPDATE_NOTES.md) | Live-model discovery changes and caveats |
| [PAPER.md](PAPER.md) | Research background and implementation details |
| [TERMS.md](TERMS.md) | Data collection, privacy and related terms |
| [SECURITY.md](SECURITY.md) | Reporting and security expectations |
| [CONTRIBUTING.md](CONTRIBUTING.md) | Guidance for contributors |

## 🤝 Contributing

Issues, reproducible bug reports, documentation fixes, and pull requests are welcome. Please do not include credentials, user chats, or private datasets in issues or commits. Read [CONTRIBUTING.md](CONTRIBUTING.md) first.

## ⚖️ License

Licensed under **[AGPL-3.0](LICENSE)**. Retain applicable copyright and license notices when distributing modified versions.

---

<div align="center">

**`HACK3RM0D3`**

*LIBERATED AI. COGNITION WITHOUT CONTROL.*

<sub>Explore thoughtfully · Verify outputs · Protect your data</sub>

</div>
