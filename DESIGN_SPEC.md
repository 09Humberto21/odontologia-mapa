# 🦷 Mapa de Estudio — Odontología
## Design Specification v3.0

**Document:** Full Design Spec for Mobile + Web Optimization
**Author:** Sielvo (AI Design Lead)
**Date:** 2026-03-27
**Platform:** Single-page web app (HTML/CSS/JS)
**Target:** Mobile-first responsive, desktop-enhanced

---

## 1. EXECUTIVE SUMMARY

### Current State (Audit Findings)
- **118 KB** single HTML file with 10 features integrated
- **39 unique font sizes** → needs consolidation to 8 max (type scale)
- **17 border-radius values** → needs consolidation to 5 (design tokens)
- **Only 1 breakpoint** (600px) → needs 3 minimum for proper responsive
- **8 modals/overlays** → inconsistent open/close patterns, no swipe-to-dismiss on mobile
- **Small touch targets** (5px padding buttons) → needs 44px minimum per WCAG
- **Z-index chaos** (2, 5, 2000, 3000, 4000, 5000) → needs layered system
- **No loading skeletons** → jarring content shifts when AI generates
- **No haptic/animation feedback** on mobile interactions
- **Print CSS** partially fixed but needs full isolation

### Design Philosophy
**"Clinical Precision, Zero Friction"** — The app should feel like a premium medical tool: clean, fast, trustworthy, and effortless on any screen size.

---

## 2. DESIGN TOKENS (Unified System)

### 2.1 Type Scale (8 sizes only)
| Token | Size | Usage |
|---|---|---|
| `--fs-xs` | `0.68rem` (10.8px) | Badges, source labels, timestamps |
| `--fs-sm` | `0.78rem` (12.5px) | Captions, meta text, tag labels |
| `--fs-base` | `0.88rem` (14px) | Body text, descriptions, quiz options |
| `--fs-md` | `1rem` (16px) | Topic names, section titles, questions |
| `--fs-lg` | `1.15rem` (18.4px) | Card titles, modal headers |
| `--fs-xl` | `1.35rem` (21.6px) | Area titles, lab titles |
| `--fs-2xl` | `1.8rem` (28.8px) | Score displays, hero stats |
| `--fs-3xl` | `clamp(2rem, 5vw, 3rem)` | Page title only |

### 2.2 Spacing Scale (8-point grid)
| Token | Value | Usage |
|---|---|---|
| `--sp-1` | `4px` | Inline gaps, icon margins |
| `--sp-2` | `8px` | Small gaps, badge padding |
| `--sp-3` | `12px` | Card inner padding, list gaps |
| `--sp-4` | `16px` | Section gaps, modal body padding |
| `--sp-5` | `20px` | Card padding, header padding |
| `--sp-6` | `24px` | Between sections, modal headers |
| `--sp-8` | `32px` | Large section spacing |
| `--sp-12` | `48px` | Page-level vertical rhythm |

### 2.3 Border Radius (5 values)
| Token | Value | Usage |
|---|---|---|
| `--r-sm` | `6px` | Tags, badges, code blocks |
| `--r-md` | `10px` | Buttons, inputs, small cards |
| `--r-lg` | `16px` | Cards, progress bars, atlas cards |
| `--r-xl` | `22px` | Modals, panels, overlays |
| `--r-full` | `50px` | Pill buttons, search bar, avatars |

### 2.4 Color System
#### Dark Theme (default)
| Token | Value | Purpose |
|---|---|---|
| `--bg` | `#0a0a0f` | Page background |
| `--bg2` | `#111218` | Card background |
| `--bg3` | `#0e0e1a` | Input/console background |
| `--surface` | `#151520` | Elevated surfaces (modals) |
| `--border` | `#1e1e2e` | Default borders |
| `--border-hover` | `#333340` | Hover borders |
| `--text` | `#ffffff` | Primary text |
| `--text2` | `#e0e0e0` | Secondary text |
| `--text3` | `#888888` | Tertiary/muted text |
| `--text4` | `#555555` | Disabled/placeholder text |

#### Light Theme
| Token | Value | Purpose |
|---|---|---|
| `--bg` | `#f5f5f8` | Page background |
| `--bg2` | `#ffffff` | Card background |
| `--bg3` | `#f0f0f5` | Input background |
| `--surface` | `#ffffff` | Modal surface |
| `--border` | `#e0e0e8` | Default borders |
| `--border-hover` | `#bbbbc5` | Hover borders |
| `--text` | `#111118` | Primary text |
| `--text2` | `#333340` | Secondary text |
| `--text3` | `#666670` | Tertiary text |
| `--text4` | `#999` | Placeholder text |

#### Area Colors (unchanged, work well)
| Area | Color | Accent |
|---|---|---|
| Endodoncia | `#7c3aed` | Purple |
| Operatoria | `#00d4ff` | Cyan |
| Periodoncia | `#22c55e` | Green |
| Cirugía | `#f59e0b` | Amber |
| Prostodoncia | `#f97316` | Orange |
| Ortodoncia | `#ec4899` | Pink |

### 2.5 Z-Index Layers
| Layer | Z-Index | Elements |
|---|---|---|
| `--z-base` | `1` | Cards, content |
| `--z-sticky` | `10` | Sticky headers, floating buttons |
| `--z-dropdown` | `100` | Dropdowns, tooltips |
| `--z-modal` | `1000` | Area modals |
| `--z-overlay` | `2000` | Lab/Quiz/Clinical overlays |
| `--z-top` | `3000` | Lightbox, exam timer |
| `--z-system` | `5000` | Theme toggle, notifications |

---

## 3. RESPONSIVE BREAKPOINTS

### 3.1 Breakpoint System
| Name | Width | Layout |
|---|---|---|
| `mobile` | `< 480px` | Single column, stacked actions, bottom sheet modals |
| `tablet` | `480px – 768px` | Single column cards, side-by-side actions |
| `desktop-sm` | `768px – 1024px` | 2-column card grid, standard modals |
| `desktop` | `1024px – 1400px` | 2-3 column grid, wider modals |
| `desktop-lg` | `> 1400px` | 3-column grid, max-width containment |

### 3.2 Mobile-Specific Patterns
- **Bottom sheet modals** instead of centered overlays on screens < 480px
- **Swipe down to dismiss** on all modal sheets
- **Sticky action bar** at bottom of quiz/exam for navigation
- **Collapsible topic cards** — tap to expand, saves vertical space
- **Full-width buttons** on mobile (no inline row of 4 tiny buttons)
- **Touch targets minimum 44x44px** per WCAG 2.1 AA
- **Horizontal scroll for action buttons** when they don't fit

### 3.3 Grid Specifications
```
Mobile:    grid-template-columns: 1fr
Tablet:    grid-template-columns: 1fr
Desktop:   grid-template-columns: repeat(auto-fit, minmax(380px, 1fr))
Desktop-lg: grid-template-columns: repeat(3, 1fr) max-width: 1400px
```

---

## 4. COMPONENT SPECIFICATIONS

### 4.1 Header Bar
- **Desktop:** Centered title + action buttons in a row
- **Mobile:** Title stacks above a horizontally scrollable button bar
- Action buttons: pill-shaped, `--r-full`, minimum height 40px
- Dark mode toggle: fixed position, top-right corner, always accessible
- **Improvement:** Add a subtle gradient divider below header

### 4.2 Progress Cards (Area Overview)
- **Desktop:** 6-column grid
- **Tablet:** 3-column
- **Mobile:** 2-column, compact padding
- Add micro-animation: progress bars animate on scroll into view (IntersectionObserver)
- Show "last studied" timestamp below progress bar
- **Tap action:** Opens area modal (unchanged)

### 4.3 Topic Cards (Main Grid)
- **Improvement needed:** Currently each topic shows 4+ buttons inline which overflow on mobile
- **Fix:** Action buttons go into a 2x2 grid on mobile, or a horizontal scroll strip
- **Notes indicator (📝)** should be a subtle dot, not text
- **Last quiz score** badge in top-right of each topic item
- **Collapsed by default on mobile** — tap topic name to expand actions

### 4.4 Action Buttons (Per Topic)
| Button | Priority | Mobile | Desktop |
|---|---|---|---|
| 🔬 Laboratorio | High | Full row | Inline |
| 💬 Consulta IA | High | Full row | Inline |
| 🧠 Quiz | High | Full row | Inline |
| 🏥 Caso Clínico | Medium | Second row | Inline |
| 🃏 Flashcards | Medium | Second row | Inline |
| 📝 Notas | Low | Expandable | Expandable |

### 4.5 Modal System
**Unified modal pattern for all overlays:**

| Property | Mobile (< 480px) | Desktop |
|---|---|---|
| Position | Bottom sheet (slides up) | Centered |
| Width | 100vw | max-width: 750px |
| Height | 90vh max | 90vh max |
| Border radius | `22px 22px 0 0` (top only) | `22px` all |
| Close | Swipe down + X button | X button + Escape + click outside |
| Animation | Slide up from bottom | Scale + fade in |
| Header | Sticky with drag handle | Sticky |

**Drag handle on mobile:**
```css
.modal-drag-handle {
  width: 36px; height: 4px;
  background: var(--border);
  border-radius: 2px;
  margin: 8px auto 4px;
}
```

### 4.6 Laboratorio Modal
- **Structure:** Header (sticky) → Methodology (AI Markdown) → Atlas Gallery → Citations → Actions
- **Atlas grid:** 2 columns on desktop, 1 column on mobile
- **Images:** 200px height desktop, 160px mobile, object-fit: cover
- **onerror fallback:** SVG diagram replaces broken images seamlessly
- **PDF button:** Isolated print — only lab content prints
- **Improvement:** Add a "Copy to clipboard" button for the methodology text

### 4.7 Quiz Interface
- **Progress bar:** Sticky at top with question counter
- **Options:** Full-width cards, minimum 52px height, clear hover/selected states
- **Navigation:** Bottom sticky bar with Prev/Next
- **Mobile:** Options have larger tap targets (full-width, 56px min-height)
- **Results screen:** Pie chart or circular progress indicator for score
- **Improvement:** Add confetti animation on >80% score

### 4.8 Flashcard Interface
- **Card:** Center-aligned, large (280px height), flip animation on tap
- **Mobile:** Card takes full width minus 32px padding
- **Rating buttons:** 3 large buttons below card (Easy/Medium/Hard) with color coding
- **Progress:** "5 of 10" counter + mastered vs remaining
- **Improvement:** Swipe left/right to rate (left = hard, right = easy)

### 4.9 Clinical Case Interface
- **Step-by-step progress:** Horizontal stepper at top (Step 1 → 2 → 3 → 4 → 5)
- **Patient presentation:** Styled as a medical record card
- **Options:** Same as quiz but with clinical context styling
- **Feedback:** Green/red border + explanation after each step
- **Improvement:** Add a "case summary" at the end with all decisions mapped

### 4.10 Exam Mode
- **Timer:** Fixed position top-right, large countdown, pulses red at <5 min
- **Question navigator:** Grid of numbered circles showing answered/unanswered
- **Mobile:** Timer in sticky header, navigator as bottom drawer
- **Results:** Breakdown by area with color-coded bars

### 4.11 Study Calendar
- **Date picker:** Native `<input type="date">` for reliability
- **Calendar grid:** 7-column (Mon-Sun), colored by topic area
- **Mobile:** Calendar scrolls horizontally if needed
- **Each day card:** Topic name + suggested study time

### 4.12 Progress Dashboard
- **Overall score:** Large circular gauge (SVG ring)
- **Topic grid:** Cards with color status (🟢🟡🔴⚪)
- **History:** Scrollable list of past quiz attempts
- **Weakness chart:** Horizontal bars sorted weakest first

---

## 5. ANIMATION & MICRO-INTERACTIONS

### 5.1 Transitions
| Element | Animation | Duration | Easing |
|---|---|---|---|
| Modal open | Scale 0.95→1 + fade | 300ms | `cubic-bezier(.4,0,.2,1)` |
| Modal close | Scale 1→0.95 + fade | 200ms | `ease-in` |
| Bottom sheet open | Translate Y 100%→0 | 350ms | `cubic-bezier(.32,.72,.24,1.02)` |
| Card hover | TranslateY -4px + shadow | 200ms | `ease-out` |
| Button press | Scale 0.97 | 100ms | `ease` |
| Progress bar fill | Width animation | 1.2s | `ease-out` |
| Flashcard flip | RotateY 0→180deg | 500ms | `ease-in-out` |
| Quiz answer reveal | Border color + bg | 300ms | `ease` |
| Tab switch | Fade + slide | 200ms | `ease` |

### 5.2 Loading States
- **AI generation:** Skeleton loader (pulsing rectangles mimicking text lines) instead of single spinner
- **Image loading:** Blur placeholder → sharp on load
- **Quiz generation:** Animated progress steps: "Generating questions... (3/10)"

### 5.3 Empty States
- **No quiz history:** Illustration + "Toma tu primer quiz para ver tu progreso aquí"
- **No notes:** "Toca para agregar tus notas personales"
- **No flashcards mastered:** "Las tarjetas que domines aparecerán aquí"

---

## 6. ACCESSIBILITY

### 6.1 Requirements (WCAG 2.1 AA)
- [ ] **Contrast ratio:** 4.5:1 minimum for text, 3:1 for large text
- [ ] **Touch targets:** 44x44px minimum
- [ ] **Focus indicators:** Visible focus ring (2px solid var(--accent)) on all interactive elements
- [ ] **Keyboard navigation:** Tab through all buttons, Enter to activate, Escape to close modals
- [ ] **ARIA labels:** All buttons, modals, and interactive elements
- [ ] **Screen reader:** Announce modal state changes, quiz progress, score results
- [ ] **Reduced motion:** `prefers-reduced-motion` media query to disable animations

### 6.2 Focus Management
- When modal opens → focus moves to first interactive element
- When modal closes → focus returns to trigger button
- Tab trap inside modals (focus doesn't escape to background)

---

## 7. PERFORMANCE OPTIMIZATION

### 7.1 Current Issues
- **118 KB single file** — acceptable but could lazy-load AI features
- **39 font sizes** → reduce to 8 (less CSS parsing)
- **Unsplash images** load on modal open (good, lazy)
- **marked.js CDN** — single external dep (acceptable)

### 7.2 Recommended Optimizations
- [ ] Consolidate CSS: reduce from ~530 rules to ~300 with token system
- [ ] Debounce search input (currently fires on every keystroke)
- [ ] Lazy render cards below fold (IntersectionObserver)
- [ ] Cache AI responses in sessionStorage (avoid re-generating same lab content)
- [ ] Compress SVGs (remove unnecessary precision)
- [ ] Add `will-change: transform` to animated elements
- [ ] Use `content-visibility: auto` on off-screen cards

---

## 8. PRINT SPECIFICATION

### 8.1 Laboratorio PDF Export
- **Scope:** ONLY lab modal content prints (methodology + atlas + citations)
- **Layout:** A4 portrait, 20mm margins
- **Typography:** Serif font for body (better print readability), 11pt base
- **Colors:** Full white background, black text, colored headings preserved
- **Images:** Print at 150px height, 2-column grid
- **Citations:** Print with full URLs in parentheses after link text
- **Page breaks:** Before atlas section, before citations section
- **Header:** Topic name + journal reference + date printed
- **Footer:** "Generated by Mapa de Estudio — Odontología"

---

## 9. DATA ARCHITECTURE (localStorage)

### 9.1 Storage Keys
| Key | Type | Purpose |
|---|---|---|
| `odo_quiz_results` | `Array<{topic, area, score, date, answers}>` | Quiz history |
| `odo_exam_results` | `Array<{score, date, byArea, answers}>` | Exam history |
| `odo_flashcards` | `Object<topicName, Array<{front, back, box, nextReview}>>` | Spaced repetition data |
| `odo_notes` | `Object<topicName, string>` | Personal notes |
| `odo_theme` | `'dark' \| 'light'` | Theme preference |
| `anthropic_key` | `string` | API key (GitHub version only) |

### 9.2 Data Limits
- Estimated max usage: ~2MB (well within 5-10MB localStorage limit)
- Implement `odo_` prefix for all keys to avoid conflicts
- Add "Export data" / "Import data" feature in settings for backup

---

## 10. IMPLEMENTATION PRIORITY

### Phase 1 — Critical (Layout & Touch)
1. Implement design token CSS variables
2. Consolidate font sizes to 8-level scale
3. Add 3 responsive breakpoints
4. Fix mobile touch targets (44px minimum)
5. Bottom sheet modals on mobile
6. Horizontal scroll for action buttons on mobile

### Phase 2 — Polish (Animations & States)
7. Skeleton loaders for AI content
8. Flashcard flip animation
9. Empty states with illustrations
10. Loading progress for quiz generation
11. Focus management and keyboard navigation

### Phase 3 — Enhancement
12. Swipe-to-dismiss modals
13. Cache AI responses in sessionStorage
14. Confetti on high quiz scores
15. Data export/import
16. IntersectionObserver for progress bar animations

---

## APPENDIX A: Component Tree
```
App
├── Header
│   ├── Title
│   ├── ActionBar (📊 📝 📅 🌙)
│   └── SearchBar
├── ProgressGrid (6 area cards)
├── MainGrid
│   └── AreaCard (×6)
│       └── TopicItem (×N)
│           ├── TopicInfo (name, desc, tag)
│           ├── ActionButtons (Lab, Chat, Quiz, Case, Flash)
│           ├── NotesSection (expandable)
│           └── ConsoleIA (expandable)
├── Timeline
└── Modals
    ├── AreaModal (info only)
    ├── LabOverlay (methodology + atlas + citations + PDF)
    ├── QuizOverlay (10 questions + results)
    ├── ClinicalOverlay (5-step case)
    ├── FlashcardOverlay (cards + spaced repetition)
    ├── ExamModal (30 questions + timer)
    ├── ProgressModal (dashboard + history)
    ├── CalendarModal (study plan)
    └── Lightbox (image zoom)
```

---

*Spec authored by Sielvo — Design lead for the Mapa de Estudio project*
*Version 3.0 | 2026-03-27*
