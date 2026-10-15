# Briefcraft — Freelance Scope Studio

An HTML, CSS and vanilla JavaScript app for freelancers who need to convert vague client messages into clear scopes and proposals. Built for the Hacktoberfest Side Hustle theme.

## Run locally (recommended for AI)
1. Install Ollama from https://ollama.com and Python 3.
2. Run `ollama pull qwen3:4b` (internet required for the initial download).
3. Quit the Ollama desktop app / existing server. In PowerShell:

```powershell
$env:OLLAMA_ORIGINS="http://localhost:8080"
$env:OLLAMA_NO_CLOUD="1"
ollama serve
```

On macOS/Linux, for a manually started server:
```sh
OLLAMA_ORIGINS=http://localhost:8080 OLLAMA_NO_CLOUD=1 ollama serve
```
If running as a background service, set these variables in that service's configuration and restart it; see Ollama's FAQ.

4. In a second terminal, from this project folder:
```sh
python -m http.server 8080 --directory dist
```
5. Open http://localhost:8080, choose AI connection and Test connection. Paste a brief and Analyze.

No npm, build tools, API keys or paid API required. Downloaded model inference can work offline; model speed and memory needs depend on your hardware. Ollama is a separate installation, not bundled. If port 8080 is occupied, choose a new port and use its exact origin in OLLAMA_ORIGINS. Do not use a wildcard origin or expose Ollama publicly. Hosted HTTPS pages can be blocked from loopback by browser network security; use the local app above if that happens.

## Features
- Local open-weight AI extracts deliverables and estimates work hours.
- Questions, risk flags, exclusions, assumptions and client-facing draft.
- Deterministic estimate = sum of estimated hours × hourly rate × (1 + buffer / 100).
- INR, USD, EUR and GBP; currency selection does not convert exchange rates.
- Copy, Markdown download, print to PDF; responsive UI and cancel/timeout controls.
- Prewritten café example explicitly labeled as a sample, not AI output.
- AI response validation and text escaping before display.
- No analytics, external fonts, external scripts or automatic brief persistence. The app sends user text only when Analyze is selected, directly to localhost:11434. Keep local-only Ollama enabled to avoid cloud inference. Exported/copied content is under your control.

## Why open innovation matters
Ollama is open-source (MIT) and Qwen3-4B has Apache-2.0 weights. The semantic scoping workflow uses the actual model; the sample is not a substitute for inference. Open weights let freelancers run client briefs locally, swap installed compatible models, inspect the prompt and avoid per-request API charges. Hardware, electricity and setup still have costs. No fine-tuning was done. AI estimates need human review.

## Commercial hypothesis / first-user plan
Audience: freelance web designers building small business websites. Value: avoid unpaid scope expansion and cut proposal drafting time. Test a one-time setup/support package or custom agency templates; pricing is a hypothesis, not validated revenue. Give it to three freelancers with real anonymized briefs. Measure drafting time, missed requirements, edits required and willingness to pay. No paying users or trials are claimed.

## Files
- dist/index.html — interface
- dist/styles.css — responsive design and print layout
- dist/app.js — Ollama integration, validation, quote calculation and exports
- dist/README.md — this guide
- LICENSE — MIT license for project code; model/runtime licenses are separate

## Limitations
Prototype, not a contract or accounting system. No authentication, billing, storage or document upload. No automatic enforcement of model license/availability for alternative models. Client text can influence AI output; review every draft. Quotes exclude taxes and external costs. Changing inputs does not silently change an existing result; analyze again or reload the sample. Browser/local inference end-to-end QA was not available in the build environment.

## Sources
- https://docs.ollama.com/api/chat
- https://docs.ollama.com/faq
- https://github.com/ollama/ollama/blob/main/LICENSE
- https://huggingface.co/Qwen/Qwen3-4B
