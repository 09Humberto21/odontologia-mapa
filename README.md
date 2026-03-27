# 🦷 Mapa de Estudio — Odontología

Interactive dental study platform powered by AI (Claude API).

## Features

- **🔬 Laboratorio Clínico** — AI-generated study methodologies with clinical atlas + PubMed citations
- **💬 Consulta IA** — Real-time AI chat per topic with streaming Markdown responses
- **🧠 Quiz de Aprendizaje** — 10 AI-generated multiple choice questions per topic with score tracking
- **📊 6 Specialty Areas** — Endodoncia, Operatoria, Periodoncia, Cirugía, Prostodoncia, Ortodoncia
- **🖼️ SVG Clinical Diagrams** — Inline vector illustrations (tooth anatomy, radiographs, implants, CBCT, adhesion, periodontium)
- **📚 PubMed Citations** — Verified references with PMID links

## Tech Stack

- Pure HTML/CSS/JS — single file, no build step
- Anthropic Claude API (Haiku) for AI features
- marked.js for Markdown rendering
- NCBI E-utilities for PubMed/PMC integration

## Usage

1. Open `index.html` in a browser (or serve via `python3 -m http.server`)
2. Click any topic's buttons: 🔬 Laboratorio, 💬 Consulta IA, 🧠 Quiz
3. Explore the clinical atlas and PubMed citations

## Author

Built by **Satoshi** with [OpenClaw](https://openclaw.ai) + Sielvo 🐾
