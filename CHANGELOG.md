# Changelog — Luis Moreno Website

> Formato: [Semantic Versioning](https://semver.org/)
> Cada entrada incluye: fecha, tipo, archivos afectados, request original.

---

## [0.1.0] — 2025-04-13

### Added — Setup Inicial (Método AInnovate FASE 1)
- Estructura de documentación creada (`docs/`)
- `docs/01-project-overview.md` — Visión, objetivos, stack, estado del proyecto
- `docs/02-architecture.md` — Estructura de carpetas, decisiones arquitectónicas, convenciones
- `docs/03-security.md` — Headers de seguridad Netlify, CDNs permitidos
- `docs/04-deployment.md` — Proceso de deploy, checklist pre-deploy
- `docs/DB_SCHEMA.md` — N/A (sitio estático)
- `docs/API_DOCS.md` — Servicios externos (Calendly, Instagram, Google Fonts)
- `docs/SKILLS.md` — Registro de skill `frontend-design` (Anthropic)
- `docs/features/` — Carpeta para features (vacía, se llena en FASE 2)
- `.windsurfrules` — Reglas para Windsurf/Cascade
- `CLAUDE.md` — Reglas para Claude Code
- `.cursorrules` — Reglas para Cursor
- `.clinerules` — Reglas para Cline/Continue
- `.github/copilot-instructions.md` — Reglas para GitHub Copilot
- `.aider.conf.yml` — Reglas para Aider
- `CHANGELOG.md` — Este archivo
- `.env.example` — Template de variables de entorno

### Changed — Reorganización de Archivos
- Assets movidos a `public/images/` y `public/logos/`
- Eliminado `CLAUDE (1).md` (reemplazado por `CLAUDE.md` con formato AInnovate)
- Eliminada carpeta `docs/superpowers/` (estructura anterior no compatible con AInnovate)
- Eliminada carpeta `Proyect to integrate/` (contenido integrado en docs/01-project-overview.md)

### Decisiones Arquitectónicas
- Sitio convertido de landing page a multi-página (home + RestaurantQR showcase)
- Stack mantenido: HTML estático + Tailwind CDN + Netlify
- Skill `frontend-design` instalada para guiar rediseño visual

### Request original
> Lee el archivo metodo.md y ejecuta la Fase 1. Integrar RestaurantQR como producto estrella.
> Objetivo: generar autoridad brutal, credibilidad, confianza y ventas.

---

## [0.2.0] — 2026-04-13

### Added — FASE 2: Rediseño + RestaurantQR Showcase
- `vercel.json` — Config de deploy para Vercel (headers de seguridad, cleanUrls)
- Sección **RestaurantQR Showcase** con browser mockup + iframe placeholder
- Sección **Servicios ultra-simple** (3 cards: Automatización, Software, IA)
- Sección **Stats condensada** (3 números en fila)
- **Nav links** (Servicios, Producto, Sobre mí)
- **CTA button con borde animado** (conic-gradient rotation, reemplaza SVG star buttons)
- **Card glow effect** (mouse-tracking radial gradient, reemplaza pixel-canvas)
- **Browser mockup CSS** para demo embed

### Changed — Rediseño Completo
- `index.html` — Reescrito completamente (620 líneas vs 1652 anterior)
- Tipografía headings: Inter → **Syne** (más distintiva, con personalidad)
- Deploy: Netlify → **GitHub + Vercel**
- `docs/04-deployment.md` — Actualizado para Vercel
- Secciones consolidadas: Problem + Promise fusionadas en Stats condensado
- Eliminada sección Instagram (pendiente reintegrar en footer)
- Eliminado pixel-canvas web component (reemplazado por CSS card-glow)
- Eliminados SVG star buttons (~8KB cada uno, reemplazados por CSS animated border)
- `index-backup.html` — Backup del diseño anterior

### Decisiones Arquitectónicas
- Stack de deploy cambiado a GitHub + Vercel por preferencia del usuario
- Syne elegida como font display por ser geométrica con personalidad
- RestaurantQR se integra via iframe embed del dashboard real en Vercel
- Servicios reducidos a 3 cards ultra-simples (1 frase cada uno)

### Request original
> Comienza el rediseño (FASE 2). Stack: GitHub + Vercel. Integración RestaurantQR via iframe embed de demo link.
> Activar localhost para ver cambios en tiempo real.

---

## [0.3.0] — 2026-04-14

### Added — FASE 3: Hero Glassmorphism + Servicios Expandibles + Secciones Restauradas
- **Hero glassmorphism 2-column layout** (título grande izq + metrics card compacta der)
- **Pixel-canvas web component** re-integrado en service cards y card $4,200
- **Expandable cards** en Automatización (IDC data) y IA para tu Negocio (bento grid)
- **Bento grid** de agentes IA (Atención al Cliente, Leads, CRM) revelado on click
- **Sección Instagram** con card flotante (@luisr_a.i)
- **Sección "El costo de no actuar"** restaurada con diseño detallado del backup
- Stats en hero card: 2.8 hrs perdidas/empleado/día, 21% facturación que se fuga, $0 cuesta descubrirlo

### Changed
- `index.html` — Tipografía revertida de Syne a **Inter** para todo el sitio
- Footer Instagram actualizado de YOUR_HANDLE a @luisr_a.i
- Services grid: `align-items:start` para que cards no se estiren al expandir una

### Fixed — Bug Fixes Mobile + Desktop
- **Services cards stretching**: Cards ya no se estiran cuando una se expande (align-items:start)
- **"El costo de no actuar" mobile overflow**: Font sizes reducidos ($4,200 de 5.75rem→3.5rem, 23h/78% de 3.75rem→2.5rem), grid collapsa a 1 columna, card hero apila verticalmente
- **RestaurantQR iframe mobile**: Escalado con transform:scale(0.55) para que el contenido sea visible sin zoom extremo
- **"Quién soy" foto mobile**: Ahora visible en mobile (height:320px) en vez de display:none
- **Methodology pills ilegibles**: chip-dim cambiado de gris (#5A6A80) a azul legible (#7EB3FF con fondo azul)
- **Bento grid mobile**: Collapsa a 1 columna, CRM card apila verticalmente

### Archivos afectados
- `index.html` — Hero, servicios, costo, metodología, about, instagram, pixel-canvas JS
- `CHANGELOG.md` — Esta entrada
- `docs/features/home-redesign.md` — Actualizado

### Request original
> Corregir: cards se estiran al expandir, $4,200 overflow en mobile, iframe zoomed, foto no aparece, pills ilegibles, bento sin armonía en mobile
