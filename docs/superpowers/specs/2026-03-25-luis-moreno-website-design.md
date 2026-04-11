# Luis Moreno — Personal Brand Website Design Spec
**Date:** 2026-03-25
**Goal:** High-conversion single-page website that generates authority, credibility, and transparency to drive high-ticket sales call bookings via Calendly.
**Business objective:** Raise $15,000 USD in 5 months (April–August 2026) to fund move to France.
**Target audience:** Business owners with 5–50 employees losing time and money to manual, repetitive processes.

---

## Technical Stack

| Item | Decision |
|---|---|
| Output | Single `index.html`, all styles inline |
| CSS | Tailwind CSS via CDN |
| Fonts | Google Fonts CDN: Space Grotesk (headings) + Inter (body) |
| Server | `serve.mjs` — Node.js static server at `localhost:3000` |
| Screenshots | `screenshot.mjs` — Puppeteer (installed locally via npm) |
| Photo | `Photo of my self.jpg` (project root) |
| Calendly | Placeholder `https://calendly.com/YOUR_LINK` — swap before launch |
| Instagram | Placeholder `https://instagram.com/YOUR_HANDLE` — swap before launch |

**Puppeteer setup:** Project root needs `package.json` + `npm install puppeteer`. Chrome binary downloads automatically. Paths corrected from `nateh` → `luisr`.

---

## Visual System

| Token | Value |
|---|---|
| Background | `#060609` |
| Surface (cards) | `#0d0d14` |
| Border | `rgba(255,255,255,0.07)` |
| Blue accent | `#2E7BF6` |
| Blue glow | `rgba(46,123,246,0.15)` |
| Text primary | `#F0F0F5` |
| Text muted | `#6B7280` |
| Font headings | Space Grotesk, tight tracking `-0.03em` |
| Font body | Inter, line-height `1.7` |

**Background texture:** Layered radial gradients (blue + purple tones) + SVG grain/noise filter.
**Depth system:** base (`#060609`) → elevated (`#0d0d14`) → floating (cards with border glow).
**Shadows:** Layered, blue-tinted, low opacity — never flat `shadow-md`.
**Animations:** Only `transform` + `opacity`. Spring-style easing. No `transition-all`.
**Interactive states:** Every clickable element has hover, focus-visible, and active states.

---

## Page Sections (in order)

### 1. Navbar
- Fixed position, frosted glass (`backdrop-blur-md`, semi-transparent background)
- Left: "Luis Moreno" wordmark
- Right: "Agendar Llamada →" CTA button (blue accent, hover glow)
- Subtle border-bottom on scroll

### 2. Hero
- Full viewport height (`100vh`)
- Animated blue radial glow behind headline
- Headline (~80–96px, Space Grotesk bold): *"Tu negocio debería trabajar para ti — no al revés."*
- Subheadline: One sentence on Done For You automation promise
- Two CTAs: primary Calendly button + secondary "Ver la Auditoría Gratis" (scroll anchor)
- Animated counter: "10+ horas/semana recuperadas" counting up on load

### 3. Problem Agitation — "El Costo de No Actuar"
- Section heading + subheading framing the pain
- 3 stat cards in a horizontal row:
  - Hours lost/week to manual tasks in SMBs
  - % of small businesses with zero automation
  - Estimated monthly cost of manual inefficiency
- Cards: surface color, subtle border, blue-tinted number styling
- Closes with one-line bridge to the solution

### 4. The Vehicle — Methodology
- Section heading: "Cómo lo hacemos"
- 3-step horizontal flow with a connecting line between steps:
  - `①` Identificar Procesos
  - `②` Documentar Flujos
  - `③` Implementar y Capacitar
- Below steps: badge row — "Modelo Done For You · Sin curva de aprendizaje · Sin fricción"
- CTA: "Empieza con una Auditoría Express Gratuita (20 min)" → Calendly

### 5. The Unstoppable Promise
- Section heading: "Lo que obtienes"
- 2×2 grid of promise cards:
  - ⏱ **10+ horas/semana** recuperadas
  - 🏖 **Tu negocio funciona sin ti** — libertad real
  - ⚡ **Implementación en 3 semanas** — sin esperas
  - 💰 **El sistema se paga solo en menos de 30 días**
- Each card: icon, bold metric, short description

### 6. Services — Bento Grid
- Asymmetric grid (large-large-small-small layout):
  - **Large:** Agentes de IA para Atención al Cliente — 24/7, sin humanos, respuestas instantáneas
  - **Large:** Agentes de Generación de Leads — LinkedIn + Google Maps scraping automatizado
  - **Small:** Automatización de Procesos Internos — elimina tareas repetitivas del equipo
  - **Small:** CRM & Seguimiento Automatizado — nunca pierdas un lead por falta de follow-up
- Cards: elevated surface, icon top-left, title, short description, subtle blue hover glow

### 7. Tech Stack
- Linear-style horizontal strip with logos + names:
  - n8n · GoHighLevel · Supabase · DigitalOcean · Hostinger · CrewAI
- Logos: use SVG/PNG from CDN or inline SVGs where available
- Label below: *"Infraestructura real en VPS — no herramientas básicas de arrastrar y soltar."*
- Subtle separator lines between logos

### 8. About Luis — Transparency Section
- Two-column layout (50/50):
  - **Left:** `Photo of my self.jpg` with blue color treatment (`mix-blend-multiply` layer) + `bg-gradient-to-t from-black/60` overlay. Rounded corners, subtle blue border glow.
  - **Right:** Name (large), positioning statement, short personal story (why automation, why France), human tone. Builds trust and connection.
- Heading: "Quién está detrás del sistema"

### 9. Guarantee
- Full-width dark card with blue border glow
- Icon: shield or checkmark
- Bold centered text: *"Garantía de Devolución del 100%"*
- Subtext: *"Si no ves resultados, te devuelvo cada centavo — y te quedas con toda la infraestructura instalada."*
- No fine print. No asterisks.

### 10. Instagram Window
- Section heading: "Sígueme para ver el trabajo en tiempo real"
- Embedded link/widget to Instagram profile
- Placeholder: `https://instagram.com/YOUR_HANDLE`
- Fallback: styled card with Instagram logo + "Ver perfil" button if iframe embed is blocked

### 11. Final CTA
- Full-width section, high contrast
- Large heading: "¿Listo para recuperar tu tiempo?"
- One-line promise recap
- Single large Calendly button: "Agendar Auditoría Gratuita →"
- Repeats the zero-risk framing (20 min, gratis, sin compromiso)

### 12. Footer
- Minimal: "Luis Moreno © 2026" left, social icons right
- No clutter

---

## Copy Strategy

- **Language:** Spanish (primary market)
- **Vocabulary focus:** "Resultados", "Transformación", "Lo que obtienes"
- **Tone:** Technical expert who delivers real engineering value — not a no-code hobbyist
- **Clarity rule:** After one read, the visitor knows exactly what you do and what they get
- **Calendly CTA** appears in: Navbar, Hero (primary), Methodology section, Final CTA — minimum 4 placements

---

## Files to Create

```
Web desing v.2/
├── index.html          ← Main deliverable
├── serve.mjs           ← Static server (localhost:3000)
├── screenshot.mjs      ← Puppeteer screenshot script
├── package.json        ← npm config for Puppeteer
├── Photo of my self.jpg ← Already exists (brand asset)
└── temporary screenshots/  ← Auto-created by screenshot.mjs
```

---

## Screenshot & Review Workflow

1. `node serve.mjs` (background)
2. `node screenshot.mjs http://localhost:3000`
3. Read screenshot PNG with Read tool
4. Compare: spacing, colors (exact hex), font sizes, alignment, border-radius, shadows
5. Fix mismatches → re-screenshot
6. Minimum 2 comparison rounds before declaring done
