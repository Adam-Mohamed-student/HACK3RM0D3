<div align="center">

# ⚡ HACK3RM0D3

### LIBERATED AI. COGNITION WITHOUT CONTROL.

**One interface. Multiple models. More ways to experiment with AI.**

[![License](https://img.shields.io/badge/License-AGPL--3.0-22c55e?style=for-the-badge)](LICENSE)
[![OpenRouter](https://img.shields.io/badge/AI-OpenRouter-7856FF?style=for-the-badge)](https://openrouter.ai/)
![Next.js](https://img.shields.io/badge/Next.js-14-black?style=for-the-badge)
![Version](https://img.shields.io/badge/Version-1.0-0ea5e9?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Experimental-f59e0b?style=for-the-badge)

**[Overview](#-overview) • [Features](#-features) • [Quick Start](#-quick-start) • [Advanced Setup](#-other-ways-to-run) • [OpenRouter](#-openrouter-models) • [Documentation](#-documentation)**

</div>

---

## 🧠 Overview

**HACK3RM0D3** is a self-hostable multi-model AI chat and experimentation toolkit powered by [OpenRouter](https://openrouter.ai/).

Instead of switching between different AI sites, use one interface to explore supported models, compare their answers, tune generation settings, and experiment with AI research workflows.

> **What can you use it for?** Learning, programming assistance, model comparison, prompt experiments, research, and exploring how different AI systems approach the same problem.

### At a glance

| Capability | What it does |
| --- | --- |
| 💬 **Multi-model chat** | Chat with supported OpenRouter models in one interface |
| 🔄 **Live model catalog** | Fetch recently listed text-capable models for ordinary chat |
| ⚔️ **Model comparisons** | Compare and synthesize responses with experimental multi-model modes |
| 🧪 **Prompt experiments** | Explore AutoTune, Parseltongue, and Semantic Transformation Modules |
| 🖥️ **Self-hosting** | Choose a single HTML app, a Next.js frontend, or an API-backed deployment |
| 🔬 **Research utilities** | Use the included evaluation scripts and supporting documentation |

---

## ✨ Features

### 💬 AI Chat & Model Selection
- Connect using **your own OpenRouter API key**.
- Explore available text-capable models using a live catalog in the regular chat selector.
- Search for models by name/provider in the Next.js model picker.
- Fall back to bundled model choices if catalog retrieval fails.
- Save chat settings/history in the browser where supported.

### ⚔️ Multi-Model Modes
- **HACK3RM0D3 CLASSIC** — multi-model comparison workflow.
- **ULTRAPLINIAN** — tier-based parallel evaluations with experimental scoring.
- **CONSORTIUM** — orchestration and response synthesis through supported API/frontend paths.

These modes may invoke multiple models per request and **can cost more than a single chat request**. Experimental scores are not guarantees of correctness.

### 🧪 AI Experimentation
- **AutoTune** — context-aware generation parameters and feedback-driven adjustments.
- **Parseltongue** — input transformations and robustness experiments.
- **STM (Semantic Transformation Modules)** — configurable output-style transformations.
- **Research tools** — scripts for evaluation, sampling, and analysis in the \`research/\` folder.

### 🎨 Interface Options
- Standalone browser interface in \`index.html\`.
- React / Next.js interface in \`src/\`.
- Optional Express API in \`api/\`, with a separate Hugging Face deployment variant in \`HF/\`.

The standalone interface and React interface are separate implementations; **some features differ between them**.

---

## 🚀 Quick Start

### Option 1 — Standalone HTML App (easiest)

**Requirements:** Git, Python 3 (for a local server), a modern browser, and an [OpenRouter API key](https://openrouter.ai/keys).

**1. Clone the project**

\`\`\`bash
git clone https://github.com/Adam-Mohamed-student/HACK3RM0D3.git
cd HACK3RM0D3
\`\`\`

**2. Start a local web server**

\`\`\`bash
python -m http.server 8000
\`\`\`

On Windows, if \`python\` is not recognized, try \`py -m http.server 8000\`.

**3. Open the application**

Visit **http://localhost:8000/index.html**.

**4. Connect OpenRouter**

Open **Settings**, enter your own OpenRouter API key, select a supported model, and start chatting.

> [!TIP]
> The standalone version requires **no npm install or frontend build**. Keep the terminal window open while using the local server.

---

## 🛠️ Other Ways to Run

All commands in this section are run from the **root directory** of the cloned repository unless stated otherwise.

### Option 2 — Next.js Development Server

**Requirements:** Node.js 20+ and npm.

\`\`\`bash
git clone https://github.com/Adam-Mohamed-student/HACK3RM0D3.git
cd HACK3RM0D3
npm ci
npm run dev
\`\`\`

Open **http://localhost:3000**, configure your OpenRouter API key in Settings, and choose a model.

For a static production export:

\`\`\`bash
npm run build
\`\`\`

With the current \`next.config.js\`, the static build is written to **\`out/\`**. Deploy that folder to a static host.

**GitHub Pages:** If publishing to \`https://adam-mohamed-student.github.io/HACK3RM0D3/\`, configure \`basePath: '/HACK3RM0D3'\` in \`next.config.js\` before building. A build alone does not enable GitHub Pages; configure deployment in the repository settings or a workflow.

### Option 3 — Optional REST API

**Requirements:** Node.js 20+ and npm. The API runs separately from the frontend.

**1. Create a local environment file**

macOS / Linux:

\`\`\`bash
cp .env.example .env
\`\`\`

Windows PowerShell:

\`\`\`powershell
Copy-Item .env.example .env
\`\`\`

**2. Edit \`.env\` with your own settings**

\`\`\`dotenv
PORT=7860
OPENROUTER_API_KEY=
HACKERMODE_API_KEY=
CORS_ORIGIN=http://localhost:3000
HF_TOKEN=
HF_DATASET_REPO=
\`\`\`

- \`OPENROUTER_API_KEY\`: optional server-side model key; requests may incur costs.
- \`HACKERMODE_API_KEY\`: set a strong secret before making the API accessible to others.
- \`CORS_ORIGIN\`: allowed frontend origin.
- \`HF_TOKEN\` and \`HF_DATASET_REPO\`: optional dataset publishing settings; leave unset unless intentionally using this feature.

**3. Install dependencies and start the API**

\`\`\`bash
npm ci
npm run api:dev
\`\`\`

Default API address: **http://localhost:7860**  
Health check: **http://localhost:7860/v1/health**

For API routes and example requests, see **[API.md](API.md)**.

> [!WARNING]
> Do not expose an API that has no authentication configured. An API using your server-side OpenRouter key can incur charges from other people's requests.

### Option 4 — Docker Compose (optional)

The repository includes \`docker-compose.yml\`, \`Dockerfile\`, and \`Dockerfile.web\` for a web + API deployment.

\`\`\`bash
# After cloning and entering HACK3RM0D3:
cp .env.example .env
# Configure .env with the necessary keys/settings
docker compose up --build -d
\`\`\`

On Windows PowerShell use \`Copy-Item .env.example .env\` instead of \`cp\`.

The Compose file maps the frontend to **http://localhost:3000** by default (\`WEB_PORT\` can override the port).

This configuration is included in the source, **but has not been end-to-end validated here**. Review the environment, API access controls, and deployment configuration before public use.

---

## 🔄 OpenRouter Models

HACK3RM0D3's **ordinary chat model picker** requests OpenRouter's text-model catalog:

\`\`\`http
GET https://openrouter.ai/api/v1/models?sort=newest&output_modalities=text
\`\`\`

- Recently listed models can appear without a manual code update.
- The **Next.js selector** supports searching for a model.
- The **standalone HTML selector** can refresh its available model choices.
- If catalog retrieval fails, bundled model choices remain as a fallback.
- A saved model may become unavailable or incompatible later.

**Important:** Special model races, tier scoring, and orchestration modes still maintain some **fixed model selections**. The live model catalog does not automatically update all those workflows.

Check [OpenRouter's model catalog](https://openrouter.ai/models) for model availability, supported parameters, and pricing. A model being listed does not guarantee it will work for every workflow.

See [OPENROUTER_UPDATE_NOTES.md](OPENROUTER_UPDATE_NOTES.md) for the scope of the model-selector update.

---

## 💡 Why Use HACK3RM0D3?

| For | How it helps |
| --- | --- |
| 🎓 **Students** | Compare explanations and explore different ways to solve problems |
| 💻 **Developers** | Test models, refine prompts, and experiment with API integration |
| 🔬 **Researchers** | Compare output behavior and use experimental evaluation tools |
| 🤖 **AI enthusiasts** | Explore multiple providers and model settings from one interface |
| 🏠 **Self-hosters** | Run and customize the interface on infrastructure they control |

Model outputs can be wrong. Verify important information before relying on it.

---

## 🔐 Privacy & Security

- **Never commit API keys or secrets** into the repository. Keep \`.env\` private.
- The browser interfaces can use **localStorage** for settings, keys, or conversation data. Avoid entering sensitive information on shared browsers.
- Requests to OpenRouter and downstream model providers are processed by external services.
- The project contains **client-side telemetry functionality**; review its implementation before entering sensitive prompts.
- The optional API includes a **dataset publishing** integration. Leave it disabled unless you intentionally want to publish suitable data.
- Self-hosting does **not** automatically mean fully offline use or private model processing.

Read [SECURITY.md](SECURITY.md), [TERMS.md](TERMS.md), and [GITHUB_SECURITY_REVIEW.md](GITHUB_SECURITY_REVIEW.md) for more details.

---

## 📂 Project Structure

\`\`\`text
HACK3RM0D3/
├── index.html                 # Standalone web app
├── src/                       # Next.js / React frontend
├── public/                    # Static assets
├── api/                       # Express API
├── HF/                        # Hugging Face deployment variant
├── functions/                 # Cloudflare-related functions
├── research/                  # Model evaluation scripts
├── paper/                     # Research paper sources
├── Dockerfile                 # API container
├── Dockerfile.web             # Frontend container
├── docker-compose.yml         # Optional combined deployment
├── .env.example               # Example local configuration
├── API.md                     # API reference
├── OPENROUTER_UPDATE_NOTES.md # OpenRouter catalog changes
└── README.md
\`\`\`

## 📚 Documentation

| File | Purpose |
| --- | --- |
| [API.md](API.md) | API endpoints, configuration, and usage |
| [OPENROUTER_UPDATE_NOTES.md](OPENROUTER_UPDATE_NOTES.md) | Live model catalog changes |
| [PAPER.md](PAPER.md) | Research background |
| [CONTRIBUTING.md](CONTRIBUTING.md) | Contributing guidelines |
| [SECURITY.md](SECURITY.md) | Security information |
| [TERMS.md](TERMS.md) | Terms and data-handling information |

## 🧩 Troubleshooting

| Issue | Try this |
| --- | --- |
| \`python\` isn't recognized | Install Python 3 or use \`py -m http.server 8000\` on Windows |
| \`npm\` isn't recognized | Install Node.js 20+ with npm |
| Port 3000 or 8000 is occupied | Stop the other process or use an available port |
| Model list won't load | Check your network connection; the fallback models may still appear |
| OpenRouter request fails | Check your API key, available balance, model ID, and provider availability |
| GitHub Pages shows missing assets | Check the \`basePath\` setting and rebuild the static export |

---

## 🤝 Contributing

Bug reports, improvements, documentation updates, and pull requests are welcome. See [CONTRIBUTING.md](CONTRIBUTING.md). Never include credentials or private user conversations in issues or commits.

## ⚖️ License

Distributed under the [GNU Affero General Public License v3.0](LICENSE). Follow the license terms and retain legally required notices when redistributing or modifying the code.

---

<div align="center">

### HACK3RM0D3

**LIBERATED AI. COGNITION WITHOUT CONTROL.**

*Explore models. Compare ideas. Build something better.*

</div>
