# Feature: Home Page Redesign (FASE 2 + FASE 3)

## Estado: ✅ En progreso

## Descripción
Rediseño completo de la landing page para maximizar conversión a llamadas de Calendly.

## Secciones (en orden — actualizado FASE 3)
1. **Nav** — Logo + links (Servicios, Producto, Sobre mí) + CTA animado
2. **Hero** — Glassmorphism 2-column: título grande (izq) + metrics glass card compacta (der) + marquee glass card
3. **Servicios** — 3 cards expandibles con pixel-canvas hover (Automatización con IDC data, Software, IA con bento grid)
4. **RestaurantQR Showcase** — Browser mockup con iframe embed del dashboard (escalado en mobile)
5. **El costo de no actuar** — Card protagonista $4,200 + 23h + 78% con descripciones y fuentes
6. **Metodología** — 3 pasos (Identificar, Diseñar, Implementar) + 4 pills
7. **Sobre Luis** — Foto + bio (foto visible en mobile)
8. **Garantía** — Devolución 100%
9. **Instagram** — Card flotante @luisr_a.i
10. **CTA Final** — "¿Listo para que tu negocio trabaje sin ti?"
11. **Footer** — Logo + copyright + Instagram link

## Decisiones de Diseño
- **Headings + Body:** Inter (única fuente, revertido de Syne en FASE 3)
- **Hero:** Glassmorphism glass cards con stats, progress bar, tag pills
- **Hero Stats:** 2.8 hrs perdidas/empleado/día, 21% facturación que se fuga, $0 cuesta descubrirlo
- **CTA Buttons:** CSS conic-gradient rotating border
- **Card Hover:** Pixel-canvas web component (re-integrado de backup)
- **Expandable Cards:** Automatización (IDC report data) + IA (bento grid de agentes)
- **Background:** Dot grid + grain overlay + Three.js mountain scene
- **RestaurantQR:** Browser chrome mockup con iframe (scale 0.55 en mobile)

## Archivos
- `index.html` — Landing page principal (~1000 líneas)
- `index-backup.html` — Backup del diseño FASE 1
- `vercel.json` — Config de deploy

## Pendiente
- [x] ~~Reintegrar enlace Instagram en footer~~ (actualizado a @luisr_a.i)
- [x] ~~Sección Instagram~~ (card flotante agregada)
- [ ] Optimizar imagen luis-moreno.jpg (8.9MB → <500KB)
- [ ] Agregar OG meta tags para social sharing
- [ ] Crear restaurantqr.html (página dedicada al producto)
