# 🦷 Design Plan v4.0 — Full Visual Overhaul
## "Clinical Precision, Zero Clutter"

**For review by:** Satoshi
**Author:** Sielvo (Design Lead)
**Date:** 2026-03-27

---

## 🔍 PROBLEMS IDENTIFIED

### 1. **Information Overload**
- **252 interactive elements** visible on the main page simultaneously
- Each topic shows 5 action buttons + notes toggle + textarea = 7 controls per topic
- 6 areas × ~6 topics × 7 controls = visual chaos
- **Fix:** Progressive disclosure — show less, reveal on demand

### 2. **Flat Visual Hierarchy**
- Everything looks the same weight — header, progress, cards, timeline all compete for attention
- No clear visual "path" guiding the eye
- Progress cards and main cards use similar styling
- **Fix:** Create clear visual layers with size, contrast, and spacing

### 3. **Textarea Problem**
- Manually resizable textareas look janky and break layout
- Notes textarea is `resize: vertical` — creates inconsistent heights
- IA console textarea has `resize: none` but fixed `min-height` looks static
- **Fix:** Auto-growing textareas + no manual resize handles

### 4. **Section Layout Issues**
- All sections run together in one long scroll with no visual breaks
- Progress grid → cards → timeline feel like one blob
- No section dividers or visual breathing room
- **Fix:** Clear section breaks with labels, dividers, and variable spacing

### 5. **Inconsistent Modal Widths**
- Area modal: 640px, Lab: 850px, Quiz: 720px, Full modals: 800px
- Creates jarring size changes when opening different features
- **Fix:** Standardize to 2 sizes: standard (680px) and wide (860px)

### 6. **Button Overload Per Topic**
- 5 colored buttons (🔬 Lab, 💬 Chat, 🧠 Quiz, 🏥 Case, 🃏 Flash) per topic
- Plus tag, notes toggle — too much visual noise
- On desktop they wrap awkwardly; on mobile they scroll but look cluttered
- **Fix:** Collapse into a clean action bar or reveal-on-hover/tap

---

## ✅ PROPOSED CHANGES

### A. PAGE STRUCTURE — Cleaner Sections

**Current flow:**
```
Header → Search → Progress Grid → Card Grid → Timeline
(all crammed together)
```

**Proposed flow:**
```
1. HERO HEADER (compact, gradient bg, search integrated)
2. ─── divider ───
3. QUICK STATS BAR (6 area pills, horizontal, clickable)
4. ─── divider ───
5. MAIN CONTENT (card grid — the focus)
6. ─── divider ───
7. STUDY PATH (timeline — collapsible)
```

**Changes:**
- **Merge search into header** — search bar sits right below the title, no separate section
- **Replace progress grid with a compact horizontal stats bar** — 6 small colored pills showing area name + score, horizontally scrollable. Clicking one scrolls to that area in the grid. Saves ~200px of vertical space.
- **Add section dividers** — subtle labeled lines between sections: `───── 📚 Áreas de Estudio ─────`
- **Make timeline collapsible** — collapsed by default, click "📍 Ver ruta de aprendizaje" to expand

### B. TOPIC CARDS — Progressive Disclosure

**Current:** Every topic shows ALL buttons immediately → visual overload

**Proposed:** Clean 2-state design:

**State 1 — Collapsed (default):**
```
● Cinemática NiTi (Nickel-Titanium)          [Alta prioridad]  📝
  Movimientos reciprocante y rotatorio...
```
- Just the dot, name, description, priority tag
- Small 📝 icon if notes exist
- Click/tap anywhere on the topic row to expand

**State 2 — Expanded (on click):**
```
● Cinemática NiTi (Nickel-Titanium)          [Alta prioridad]  📝
  Movimientos reciprocante y rotatorio...

  ┌─────────────────────────────────────────┐
  │ 🔬 Laboratorio  🧠 Quiz  🏥 Caso Clínico │
  │ 🃏 Flashcards   💬 Consulta IA           │
  └─────────────────────────────────────────┘

  📝 Mis notas: ____________________________
```
- Buttons appear in a clean 2-row grid
- Notes field appears (auto-grow, no resize handle)
- Smooth slide-down animation

**Result:** Main page goes from ~252 visible controls to ~30 (just topic rows + tags)

### C. TEXTAREA REDESIGN — Auto-Growing

**Remove all manual resize handles.** Replace with:

```css
textarea {
  resize: none;           /* Kill the handle */
  overflow: hidden;       /* No scrollbar */
  min-height: 44px;       /* One line */
  field-sizing: content;  /* Auto-grow with content (modern CSS) */
}
```

For the IA console input:
- Single line by default (looks like a chat input, not a code editor)
- Grows automatically as user types
- Send button aligned to the right
- Looks like a chat message bar, not a form

For notes:
- Starts as 1 line "Escribe tus notas..."
- Grows automatically
- No visible border until focused

### D. CARD VISUAL UPGRADE

**Current:** Cards are flat dark boxes with subtle borders
**Proposed:**

- **Top accent gradient:** Each card gets a 3px gradient bar at the top in its area color (already partially done, make it more visible)
- **Subtle inner glow:** Very faint radial gradient from the accent color inside the card header area
- **Card count badge:** Small "6 temas" count in the card header
- **Rounded icon containers:** The emoji icons get a larger, more prominent container with gradient background
- **Better spacing:** More padding between topics, clearer visual separation

### E. HEADER REDESIGN — Compact + Functional

**Current:** Large header with title, subtitle, 4 buttons = takes ~200px height

**Proposed:** Slim header bar:
```
┌─────────────────────────────────────────────────────────┐
│  🦷 Mapa de Estudio                    📊 📝 📅 🌙     │
│  ┌─────────────────────────────────┐                    │
│  │ 🔍 Buscar tema...               │                    │
│  └─────────────────────────────────┘                    │
└─────────────────────────────────────────────────────────┘
```

- Title on the left, action buttons on the right (like a real app navbar)
- Search bar integrated directly below
- Total height: ~120px instead of ~280px
- On mobile: title centered, buttons in a row below, search below that

### F. MODAL STANDARDIZATION

**Two sizes only:**
| Type | Width | Use case |
|---|---|---|
| **Standard** | `680px` | Area info, Quiz, Clinical Cases, Flashcards, Calendar |
| **Wide** | `860px` | Laboratorio (needs space for atlas + citations), Exam, Progress Dashboard |

**All modals get:**
- Consistent border radius: `--r-xl` (22px)
- Same header structure: badge → title → meta
- Same close button position and style
- Same animation (slide up on mobile, scale+fade on desktop)

### G. COLOR & CONTRAST REFINEMENT

**Current issue:** The background is very dark (#06060c) but cards (#0f0f1a) are barely distinguishable

**Proposed:** Increase contrast between layers:
| Layer | Current | Proposed |
|---|---|---|
| Page bg | `#06060c` | `#08080f` |
| Card bg | `#0f0f1a` | `#121220` |
| Surface | `#12121e` | `#181828` |
| Input bg | `#0a0a14` | `#0e0e1a` |

This gives more visible card edges and better depth perception.

### H. TYPOGRAPHY TIGHTENING

- **Headings:** Reduce letter-spacing to `-0.5px` for that premium tight look
- **Body text:** Increase line-height from 1.75 to 1.8 for readability
- **Badges/tags:** All uppercase, `letter-spacing: 1.5px`, font-weight 800
- **Numbers/scores:** Use `font-variant-numeric: tabular-nums` for aligned digits

---

## 📐 VISUAL MOCKUP (ASCII)

### Desktop (1200px)
```
┌──────────────────────────────────────────────────────────────┐
│  🦷 Mapa de Estudio — Odontología           📊 📝 📅 🌙    │
│     🔍 Buscar tema...                                        │
├──────────────────────────────────────────────────────────────┤
│  Endo 72%  Oper 65%  Perio 50%  Cirug 45%  Prost 40%  Orto 30%  │
├──────────── 📚 Áreas de Estudio ─────────────────────────────┤
│  ┌──────────────────────┐  ┌──────────────────────┐         │
│  │ 🔬 Endodoncia  [ADV] │  │ 🪥 Operatoria  [ADV] │         │
│  │───────────────────── │  │───────────────────── │         │
│  │ ● Cinemática NiTi    │  │ ● IDS              [!]│         │
│  │ ● Irrigación PUI     │  │ ● Biomimética        │         │
│  │ ● Biocerámicos       │  │ ● Adhesión           │         │
│  │ ● CBCT               │  │ ● Estratificación    │         │
│  │ ● Anatomía           │  │ ● Mínima Intervención│         │
│  │ ● Diagnóstico     📝 │  │ ● Prep. Cavitaria    │         │
│  └──────────────────────┘  └──────────────────────┘         │
│  ┌──────────────────────┐  ┌──────────────────────┐         │
│  │ 🦠 Periodoncia [INT] │  │ ⚕️ Cirugía     [INT] │         │
│  │ ...                   │  │ ...                   │         │
│  └──────────────────────┘  └──────────────────────┘         │
├──────────── 📍 Ruta de Aprendizaje (click to expand) ────────┤
└──────────────────────────────────────────────────────────────┘
```

### Topic Expanded
```
│  ● Cinemática NiTi (Nickel-Titanium)     [Alta prioridad]    │
│    Movimientos reciprocante y rotatorio...                    │
│                                                               │
│    🔬 Laboratorio   🧠 Quiz   🏥 Caso Clínico                │
│    🃏 Flashcards    💬 Consulta IA                            │
│                                                               │
│    📝 Escribe tus notas...                                    │
│                                                               │
│    💬 Pregunta sobre este tema... ──────────── [✦ Enviar]     │
```

### Mobile (375px)
```
┌─────────────────────────┐
│ 🦷 Mapa de Estudio      │
│       📊 📝 📅 🌙       │
│ 🔍 Buscar...            │
├─────────────────────────┤
│ E72 O65 P50 C45 P40 O30│← horizontal scroll
├── 📚 Áreas ─────────────┤
│ ┌─────────────────────┐ │
│ │ 🔬 Endodoncia       │ │
│ │ ● Cinemática NiTi   │ │← tap to expand
│ │ ● Irrigación PUI    │ │
│ │ ● Biocerámicos      │ │
│ │ ● CBCT              │ │
│ │ ● Anatomía          │ │
│ │ ● Diagnóstico       │ │
│ └─────────────────────┘ │
│ ┌─────────────────────┐ │
│ │ 🪥 Operatoria       │ │
│ │ ...                  │ │
│ └─────────────────────┘ │
└─────────────────────────┘
```

---

## ⚡ IMPLEMENTATION PLAN

| Step | Change | Impact |
|---|---|---|
| 1 | **Compact header** — navbar style, search integrated | Major visual difference |
| 2 | **Quick stats bar** replacing progress grid | Saves ~200px, cleaner |
| 3 | **Topic progressive disclosure** — collapsed by default, expand on click | Removes ~220 visible buttons |
| 4 | **Auto-growing textareas** — no resize handles | Cleaner, more polished |
| 5 | **Section dividers** with labels | Better visual structure |
| 6 | **Card visual upgrade** — accent bars, glows, better spacing | Premium feel |
| 7 | **Modal standardization** — 2 sizes, consistent headers | Professional consistency |
| 8 | **Color contrast boost** — better layer differentiation | Depth and readability |
| 9 | **Collapsible timeline** | Less scroll, cleaner page |
| 10 | **Typography tightening** | Polish |

**Estimated result:** The page should feel 50% less cluttered while having 100% of the same functionality, just organized better.

---

## 🤔 QUESTIONS FOR SATOSHI

1. Do you like the **compact navbar header** replacing the centered hero header?
2. Are you okay with **topics being collapsed by default** (click to expand)?
3. Do you want to keep the **progress cards as a grid** or switch to the **horizontal pills bar**?
4. Any features you want **more prominent** or **hidden further**?
5. Color preference: keep the current very dark bg, or slightly lighter for more contrast?

---

*Awaiting approval to proceed with implementation.*
