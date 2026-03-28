# 🦷 Mapa de Estudio — Odontología

Plataforma interactiva de estudio de odontología potenciada por IA (Claude API). Construida en un solo día, en un solo archivo HTML, sin frameworks.

**Live:** [mapadeestudiodontologia.netlify.app](https://mapadeestudiodontologia.netlify.app)

---

## ✨ Features

### Aprendizaje con IA
- **🔬 Laboratorio Clínico** — Genera metodologías de estudio completas con IA + atlas de imágenes + citas de PubMed
- **💬 Consulta IA** — Chat en tiempo real por tema con streaming y Markdown
- **🧠 Quiz (10 preguntas)** — Generado por IA con dificultad progresiva y explicaciones
- **🏥 Casos Clínicos Interactivos** — Paciente paso a paso: diagnóstico → tratamiento
- **🃏 Flashcards** — Repetición espaciada con sistema Leitner (Easy/Medium/Hard)
- **📝 Examen Mixto** — 30 preguntas de todas las áreas con temporizador de 45 min

### Seguimiento y Planificación
- **📊 Dashboard de Progreso** — Mapa de debilidades (🟢🟡🔴), historial de quizzes
- **📅 Plan de Estudio IA** — Calendario semanal basado en tus debilidades
- **📝 Notas Personales** — Por tema, auto-guardadas en localStorage

### Diseño
- **🌙/☀️ Dark/Light Mode**
- **📱 Mobile-first** — Bottom sheet modals, touch targets de 44px, scroll horizontal
- **📄 Exportar PDF** — Imprime solo el contenido del Laboratorio
- **Design tokens** — 8 font sizes, 8 spacing, 5 radii, sistema de colores completo

## 🏗️ Stack Técnico

| Qué | Cómo |
|---|---|
| Frontend | HTML + CSS + JS puro (130KB, 1 archivo) |
| IA | Anthropic Claude API (Haiku) directo desde browser |
| Markdown | marked.js (CDN) |
| Datos | localStorage (progreso, notas, flashcards) |
| Deploy | Netlify |
| Frameworks | Ninguno |
| Build step | Ninguno |

## 🎨 También hicimos esto

Conectamos **Blender 5.1** via MCP Server (51 herramientas) y construimos una escultura 3D de Satoshi Nakamoto sosteniendo un Bitcoin dorado — materiales metálicos, iluminación de estudio, cámara — todo controlado por IA desde la terminal.

## 🚀 Uso

1. Abre `index.html` en un browser (o sirve con `python3 -m http.server`)
2. Ingresa tu API key de Anthropic cuando se te pida
3. Explora las 6 áreas, haz quizzes, estudia con flashcards

## 📚 Áreas de Estudio

| Área | Temas | Nivel |
|---|---|---|
| 🔬 Endodoncia | 6 | Avanzado |
| 🪥 Operatoria Dental | 6 | Avanzado |
| 🦠 Periodoncia | 5 | Intermedio |
| ⚕️ Cirugía Oral | 5 | Intermedio |
| 👑 Prostodoncia | 5 | Intermedio |
| 📐 Ortodoncia | 4 | Complementario |

## 👨‍💻 Autor

Construido por **Satoshi** con [OpenClaw](https://openclaw.ai) + Sielvo 🐾

Hecho en El Salvador 🇸🇻
