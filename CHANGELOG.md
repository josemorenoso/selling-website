# Changelog — Luis Moreno Website

> Formato: [Semantic Versioning](https://semver.org/)
> Cada entrada incluye: fecha, tipo, archivos afectados, request original.

---

## [0.5.1] — 2026-04-18

### Cambiado — FASE 3.1: Feedback de audit y conversión
Ajustes basados en auditoría directa del usuario para elevar conversión y resolver issues reales.

#### Hero
- **Stats reemplazados** (los viejos sonaban a "mercado perdiendo", no a autoridad):
  - `2.8 hrs perdidas/empleado/día` → `3 sem entrega promedio`
  - `21% facturación que se fuga` → `24/7 operando solo`
  - `$0 cuesta descubrirlo` → `100% código es tuyo`
- Main metric superior: `10+ hrs/sem recuperadas` → `Sistema operando / entregado y documentado` (más assertivo)
- Progress bar: `Satisfacción del cliente 98%` → `Uptime mensual 99.8%` (más técnico y creíble)
- Tag pill `ACTIVO` → `EN PRODUCCIÓN` (autoridad)
- **Copy subtítulo comprimido**: "Implemento sistemas de automatización con IA que eliminan el trabajo repetitivo..." → "Automatizo los procesos que te están robando horas. Tu equipo ejecuta, tú diriges — y tu negocio crece sin ti empujándolo"
- **Fix overflow mobile**: añadidas reglas `@media (max-width:768px)` específicas para `.hero .glass-card`, `.hero .glass-stat-val`, `.hero .glass-stat-label`, `.hero .tag-pill`

#### Servicios
- **Título corregido**: "Tres formas de multiplicar tu negocio" → "Soluciones que te ofrezco" (más concreto, pedido del user)
- **Label**: "Qué hago por ti" → "Servicios"
- **Métricas Agente IA**: `98% tasa respuesta / <3s tiempo respuesta` → `+30% aumento en ventas / 24/7 respondiendo leads` (sincronizado con propuesta de valor real)

#### Producto Estrella
- **Fix login iframe**: Los browsers bloquean cookies third-party en iframes cross-origin → Supabase no persiste sesión. Solución:
  - Añadido botón **"Abrir demo en pestaña nueva ↗"** como CTA secundario prominente
  - Añadido botón **"↗ Abrir"** en la barra del browser-mockup
  - Disclaimer explicativo bajo el iframe con instrucción clara
- Copy tech movido a línea inferior más sutil (antes mezclado con CTAs)

#### Fondo — Profundidad Cinematográfica
- **Gradient mesh direccional** agregado al body (3 radial-gradients posicionados: azul top-left, teal right, azul oscuro bottom)
- **Dot pattern mejorado**: opacity 0.35 → 0.22, size 36px → 42px, añadido `mask-image` radial para que se disuelva en los bordes
- **Vignette sutil**: nuevo `.bg-vignette` div con radial-gradient que contiene la mirada al centro
- **Noise opacity**: 0.028 → 0.035 (más grain, más cine)

#### Jerarquía tipográfica + Armonía
- Hero `.hero-grid` gap: 2.5rem → 3rem (más respiro entre columnas)
- `.glass-stat-label`: color `#5A6A80` → `#A8B6CC`, letter-spacing ajustado, añadido `margin-top:2px` y `line-height:1.3`
- `.tag-pill`: color `#8A9BB0` → `#C5D0E0`, font-weight 600 → 700
- `"Operando con"` label: color `#5A6A80` → `#A8B6CC` (era casi invisible)

#### Por Qué Trabajar Conmigo — Copy comprimido
Párrafos largos reducidos a 1-2 frases impactantes con `<strong>` en claims clave. Todos los 6 cards ahora tienen el mismo ritmo tipográfico.

- Fix typo: "Te voy con un plan concreto" → "Sales con un plan concreto"

### Archivos afectados
- `index.html` — hero stats, servicios, producto estrella, por qué, fondo, responsive
- `CHANGELOG.md` — esta entrada

### Issues resueltos del feedback
- ✅ Hero stats raros ("2.8 hrs" etc) → reemplazados por autoridad
- ✅ Hero se sale en web/mobile → reglas responsive añadidas
- ✅ Título "3 formas multiplicar" → "Soluciones que te ofrezco"
- ✅ Agente IA: +30% ventas visible
- ✅ Login iframe producto → botón alternativo en nueva pestaña (root cause: cookies third-party bloqueadas por browser)
- ✅ Excesos de letras → copy comprimido en "Por qué"
- ✅ Fondo plano → mesh gradient + vignette + dot pattern refinado

### Request original
> Login no funciona en producción. Audita: fondo transparente, jerarquía, armonía, excesos de letra, stats raros del hero. Pon +30% en agente IA. Título "3 formas" es raro → "Soluciones que te ofrezco".

---

## [0.5.0] — 2026-04-18

### Cambiado — FASE 3: Rediseño para Autoridad, Credibilidad y Confianza
Reescritura masiva enfocada en generar autoridad inmediata y comunicar valor concreto al cliente. Inspirada en referencia `admirable-liger-25cfe0.netlify.app`.

#### Legibilidad global
- `.muted` ahora `#A8B6CC` (antes `#5A6A80` — ilegible)
- `.dimmed` ahora `#C5D0E0` (antes `#8A9BB0`)
- `.nav-link` ahora `#C5D0E0`
- Cumple WCAG AA en body text sobre fondos translúcidos

#### Sección Servicios (antes "Qué hago")
- Nuevo título: "Qué hago por ti" / "Tres formas de multiplicar tu negocio"
- 3 cards **simétricas** con estructura uniforme: chip top, título, descripción, 2 métricas visuales, tech chips
- Métricas por card: 40+hrs/0 errores, 3-5sem/100% código tuyo, 98%/<3s
- Eliminado: bento expandable redundante (IA agents detail)

#### Producto Estrella (antes "RestaurantQR")
- Nuevo nombre: "Plataforma de Fidelización para Restaurantes" con gradient
- Copy orientado a valor: +30% ventas, +65% retención, software replicable
- **Iframe actualizado** a URL real: `https://restaurant-fidelity-system.vercel.app/`
- Añadidas credenciales demo visibles: `demo@gmail.com` / `123456789`
- Nuevo CTA: "Quiero esto en mi negocio"

#### Reemplazado: "Costo de no actuar" → "Por qué trabajar conmigo"
- Nueva zona de autoridad con 6 razones: código tuyo, resultados medibles, Done For You, especialista no agencia, velocidad, stack moderno
- Icons SVG por razón
- CTA final en caja destacada

#### Metodología
- Copy reforzado, texto más legible (`.dimmed` en lugar de `.muted`)
- Tamaño texto 0.925rem / line-height 1.7

#### Portafolio
- Separadores visuales antes/después con decoradores "◆ EN PRODUCCIÓN"
- Título nuevo: "5 sistemas. Funcionando ahora mismo."
- Copy de cada card **punchier**: métricas destacadas con `<strong>`, orientadas a valor, CTAs específicas ("Chatear con el agente", "Probar el formulario")
- Badge "● Live" verde en cada card
- Fondo diferenciador sutil con radial gradient

#### Quién soy
- **Eliminado**: "ingeniero de automatización"
- Reemplazado por: "especialista en automatización, desarrollo de web apps y sistemas de IA"
- Copy más assertivo con `<strong>` en claims clave

#### Demos / PIN Gate
- Cambio de `demo_access: 'true'` a `demo_access_ts: <timestamp>`
- TTL de 15 minutos
- **Invalidación automática** cuando el usuario viene de fuera de `/demos/` (via document.referrer)
- Los 5 demo pages refrescan timestamp al cargar (mantiene sesión mientras navega entre demos)
- Access check mejorado con IIFE + TTL

#### Webhooks n8n
- `prospectos.html`: URL actualizada a `/webhook-test/captador-prospectos`
- `reporte.html`, `presupuestos.html`, `hoteles.html`: confirmadas URLs correctas
- **Mejor manejo de errores**: muestra status HTTP real, detecta CORS, log en consola para debugging

### Archivos afectados
- `index.html` — legibilidad, servicios, producto, "por qué", metodología, portafolio, sobre-mí
- `demos/index.html` — lógica PIN con TTL
- `demos/{restaurantes,hoteles,prospectos,reporte,presupuestos}.html` — access check TTL + error handling
- `docs/progress/fase-3-autoridad-credibilidad.md` — NUEVO, tracking persistente
- `CHANGELOG.md` — esta entrada

### Request original
> Necesito una página web que genere confianza, credibilidad y autoridad de inmediato. Enfocada en qué gana el cliente, números, profesionalidad, que haga querer agendar cita ya.

---

## [0.4.0] — 2026-04-16

### Agregado — Portafolio de Automatizaciones (5 herramientas en vivo)
- Sección `#portafolio` en `index.html` con 5 cards de herramientas de automatización
- Nav link "Portafolio" en navbar
- Sistema de demos protegido por PIN (`/demos/index.html`)
- CSS compartido para demos (`demos/shared.css`)
- `demos/restaurantes.html` — iframe del dashboard RestaurantQR real
- `demos/hoteles.html` — widget chat n8n con agente IA GPT-4o
- `demos/prospectos.html` — formulario de captación de leads → email
- `demos/reporte.html` — generador de reportes semanales → email
- `demos/presupuestos.html` — cotizador dinámico con checkboxes → 2 emails
- `workflows/captador-prospectos.json` — workflow n8n importable (Webhook → Code → Gmail ×2)
- `workflows/reporte-negocio.json` — workflow n8n importable (Webhook → Code → Gmail)
- `workflows/creador-presupuestos.json` — workflow n8n importable (Webhook → Code → Gmail ×2)
- `workflows/hotel-booking-ai-agent-v3.json` — copiado de existente + _readme
- `workflows/qloapps-check-availability-v10.json` — copiado de existente + _readme
- `workflows/qloapps-generate-link-v10.json` — copiado de existente + _readme
- `docs/features/portfolio.md` — feature doc completo

### Archivos afectados
- `index.html` — sección #portafolio, nav link, CSS portfolio-grid
- `demos/` — 6 archivos nuevos (index, shared.css, 5 demo pages)
- `workflows/` — 6 archivos (3 nuevos, 3 copiados)
- `docs/features/portfolio.md` — nuevo
- `CHANGELOG.md` — esta entrada

### Request original
> Implementar portafolio de automatizaciones con 5 herramientas en vivo, demos protegidas por PIN, workflows n8n importables.

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
