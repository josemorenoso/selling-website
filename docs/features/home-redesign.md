# Feature: Home Page Redesign (FASE 2)

## Estado: ✅ En progreso

## Descripción
Rediseño completo de la landing page para maximizar conversión a llamadas de Calendly.

## Secciones (en orden)
1. **Nav** — Logo + links (Servicios, Producto, Sobre mí) + CTA animado
2. **Hero** — Badge + H1 + subtitle + CTAs + stat bar
3. **Logo Ticker** — Marquee "Operando con" (logos de herramientas)
4. **Servicios** — 3 cards ultra-simples (Automatización, Software, IA)
5. **RestaurantQR Showcase** — Browser mockup con iframe embed del dashboard
6. **Stats** — 3 números ($4,200 / 23h / 78%) condensados
7. **Metodología** — 3 pasos (Identificar, Diseñar, Implementar)
8. **Sobre Luis** — Foto + bio
9. **Garantía** — Devolución 100%
10. **CTA Final** — "¿Listo para que tu negocio trabaje sin ti?"
11. **Footer** — Logo + copyright + links

## Decisiones de Diseño
- **Headings:** Syne (geométrica, con personalidad)
- **Body:** Inter (limpia, legible)
- **CTA Buttons:** CSS conic-gradient rotating border (reemplaza SVG star buttons)
- **Card Hover:** Mouse-tracking radial gradient glow (reemplaza pixel-canvas)
- **Background:** Dot grid + grain overlay + Three.js mountain scene
- **RestaurantQR:** Browser chrome mockup con iframe placeholder

## Archivos
- `index.html` — Landing page principal
- `index-backup.html` — Backup del diseño anterior
- `vercel.json` — Config de deploy

## Pendiente
- [ ] URL de demo de RestaurantQR para activar iframe
- [ ] Reintegrar enlace Instagram en footer (actualizar handle)
- [ ] Optimizar imagen luis-moreno.jpg (8.9MB → <500KB)
- [ ] Agregar OG meta tags para social sharing
- [ ] Crear restaurantqr.html (página dedicada al producto)
