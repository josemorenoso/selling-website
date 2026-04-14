# Arquitectura — Luis Moreno Website

## Stack Completo
| Dependencia | Versión | Uso |
|-------------|---------|-----|
| TailwindCSS CDN | Latest | Sistema de estilos (vía script tag) |
| Three.js | r134 | Background 3D (mountain scene) |
| Syne (Google Fonts) | Variable | Tipografía headings (display) |
| Inter (Google Fonts) | Variable | Tipografía body |
| Puppeteer | 24.40.0 | Screenshots de desarrollo (dev only) |

## Estructura de Carpetas (Actualizada 2026-04-13)
```
luis-moreno-website/
├── docs/                              # Documentación (Método AInnovate)
│   ├── 01-project-overview.md         # Visión, objetivos, stack, estado
│   ├── 02-architecture.md             # Este archivo
│   ├── 03-security.md                 # Headers, CDNs, seguridad
│   ├── 04-deployment.md               # Vercel deploy + checklist
│   ├── DB_SCHEMA.md                   # N/A (sitio estático)
│   ├── API_DOCS.md                    # Servicios externos
│   ├── SKILLS.md                      # Skills instaladas (frontend-design)
│   └── features/                      # Un .md por funcionalidad
│       └── home-redesign.md          # Rediseño FASE 2
├── public/                            # Assets estáticos
│   ├── images/
│   │   └── luis-moreno.jpg            # Foto personal (8.9MB — optimizar antes de deploy)
│   └── logos/                         # Logos del tech stack (SVGs)
│       ├── n8n.svg
│       ├── notion.svg
│       ├── claude.svg
│       ├── github.svg
│       ├── langchain.svg
│       ├── mcp.svg
│       └── antigravity-color.svg
├── .github/
│   └── copilot-instructions.md        # Reglas para GitHub Copilot
├── index.html                         # Página principal (Home) — rediseñada FASE 2
├── index-backup.html                  # Backup del diseño anterior (FASE 1)
├── restaurantqr.html                  # [PENDIENTE] Showcase RestaurantQR + Demo
├── .windsurfrules                     # Reglas para Windsurf/Cascade
├── CLAUDE.md                          # Reglas para Claude Code
├── .cursorrules                       # Reglas para Cursor
├── .clinerules                        # Reglas para Cline/Continue
├── .aider.conf.yml                    # Reglas para Aider
├── CHANGELOG.md                       # Historial de cambios
├── metodo_ainnovate.md                # Framework de producción AInnovate v2
├── vercel.json                        # Configuración de deploy Vercel + headers seguridad
├── netlify.toml                       # [LEGACY] Config anterior de Netlify
├── package.json                       # Dependencias (solo puppeteer dev)
├── package-lock.json                  # Lock file
├── serve.mjs                          # Servidor local de desarrollo (puerto 3000)
├── screenshot.mjs                     # Utilidad de screenshots (dev, gitignored)
├── robots.txt                         # SEO
├── .env.example                       # Variables de entorno (template)
└── .gitignore
```

## Decisión: Sitio Estático Multi-Página (No SPA)
El sitio es HTML estático servido por Vercel. No usa frameworks (React, Next.js, etc.) porque:
1. El contenido es mayormente estático (landing + showcase)
2. La velocidad de carga es máxima sin bundlers
3. El deploy en Vercel es instantáneo
4. No hay backend ni autenticación en el sitio web
5. RestaurantQR se integra via iframe embed del dashboard real en Vercel

## Flujo de Datos
```
Visitante → index.html (Home)
    ├── CTA → Calendly (externo)
    ├── Nav/Card → restaurantqr.html (Showcase + Demo)
    └── Instagram → Perfil externo

restaurantqr.html (Demo Dashboard)
    ├── Datos mock (inline JSON)
    ├── Gráficas interactivas (Chart.js o similar)
    └── CTA → Calendly
```

## Variables de Entorno
| Variable | Descripción | Tipo | Requerida |
|----------|-------------|------|-----------|
| N/A | Sitio estático, sin variables de entorno en runtime | - | - |

> Las URLs de Calendly y redes sociales están hardcodeadas en el HTML ya que son públicas.

## Convenciones del Proyecto
| Tipo | Convención |
|------|------------|
| Archivos HTML | kebab-case (`restaurantqr.html`) |
| Clases CSS | kebab-case (`.hero-badge`, `.stat-bar`) |
| IDs HTML | kebab-case (`#mountain-canvas`, `#c-hero`) |
| Variables CSS custom | `--color-*`, `--spacing-*` |
| Assets/imágenes | kebab-case en carpeta `public/` |
| Documentación | Numerada `NN-nombre.md` en `docs/` |

## Decisiones Arquitectónicas

### ADR-001: Multi-página en vez de SPA
**Fecha:** 2025-04-13
**Contexto:** Se necesita integrar un producto showcase (RestaurantQR) al sitio de servicios existente
**Decisión:** Crear páginas HTML separadas en vez de migrar a un framework SPA
**Consecuencias:** Deploy más simple, carga más rápida, sin dependencias de build. Trade-off: no hay state compartido entre páginas (no necesario).

### ADR-002: RestaurantQR via iframe embed
**Fecha:** 2026-04-13
**Contexto:** RestaurantQR existe como producto real en producción (Next.js + Supabase + Vercel)
**Decisión:** Integrar via iframe embed del dashboard real hospedado en Vercel, en vez de recrear un demo standalone
**Consecuencias:** El showcase muestra el producto REAL, no un mock. Requiere que el dashboard real esté online. Se usa browser mockup CSS para presentación premium.

### ADR-004: Syne como font display
**Fecha:** 2026-04-13
**Contexto:** Inter era la única fuente, haciendo los headings genéricos
**Decisión:** Usar Syne para headings (geométrica con personalidad) + Inter para body
**Consecuencias:** Tipografía más distintiva y memorable. Syne está disponible en Google Fonts sin costo.

### ADR-005: Deploy en Vercel (no Netlify)
**Fecha:** 2026-04-13
**Contexto:** El producto RestaurantQR ya está en Vercel, y el usuario prefiere consolidar
**Decisión:** Migrar deploy de Netlify a GitHub + Vercel
**Consecuencias:** Config simplificada (`vercel.json`), mismo proveedor que RestaurantQR, cleanUrls automáticos.

### ADR-003: Mantener Tailwind CDN
**Fecha:** 2025-04-13
**Contexto:** El proyecto original usa Tailwind vía CDN script tag
**Decisión:** Mantener este approach. No migrar a PostCSS/build step
**Consecuencias:** Simplicidad máxima. El archivo es más grande pero para un sitio de pocas páginas es aceptable.
