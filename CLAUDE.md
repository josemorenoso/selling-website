# LUIS MORENO WEBSITE — Reglas para IA (Método AInnovate v2)

> **ATENCIÓN IA:** Este proyecto usa Documentation-Driven Development.
> **ANTES** de escribir CUALQUIER línea de código, DEBES leer los docs relevantes.
> Documento completo del método: `metodo_ainnovate.md` (raíz del proyecto)

## Skill Obligatoria: frontend-design
**ANTES de escribir cualquier código frontend, invocar la skill `frontend-design`.**
Ver `docs/SKILLS.md` para detalles completos.

## Protocolo Obligatorio (antes de cada cambio)
1. LEER `docs/01-project-overview.md`
2. LEER `docs/02-architecture.md`
3. IDENTIFICAR qué feature se modifica
4. LEER `docs/features/[feature].md`
5. Si NO existe doc para la feature → CREARLO antes de codear
6. Si se toca deploy → LEER `docs/04-deployment.md`
7. Si se toca seguridad/headers → LEER `docs/03-security.md`
8. Si se implementa UI → LEER `docs/SKILLS.md` e invocar frontend-design

## Los 12 Mandamientos del Vibe Coding (INVIOLABLES)
| # | Mandamiento | Regla |
|---|-------------|-------|
| I | NO ALUCINARÁS | Solo implementar exactamente lo pedido. Ante duda → PREGUNTAR |
| II | SEPARARÁS LÓGICA DE ESTILOS | Nunca mezclar en el mismo archivo |
| III | DOCUMENTARÁS CADA CAMBIO | Ningún cambio sin su doc correspondiente |
| IV | ACTUALIZARÁS EL CHANGELOG | Cada request → nueva entrada |
| V | DOCUMENTARÁS LA DB | N/A (sitio estático) |
| VI | SEGUIRÁS LA ESTRUCTURA | No crear archivos fuera de la estructura |
| VII | USARÁS EL SISTEMA DE ESTILOS | Respetar el design system (Tailwind config) |
| VIII | PROTEGERÁS CREDENCIALES | Nada hardcodeado, todo en .env |
| IX | TIPARÁS TODO | N/A (Vanilla JS — usar JSDoc cuando útil) |
| X | VALIDARÁS ANTES DE ENTREGAR | Checklist obligatorio |
| XI | MANTENDRÁS CONSISTENCIA | Seguir convenciones existentes |
| XII | COMUNICARÁS CON CLARIDAD | Resumen de acciones al terminar |

## 4 Leyes de Operación
1. **LEER ANTES DE ACTUAR** — Consultar docs antes de cualquier cambio
2. **NO ROMPER LO QUE FUNCIONA** — Detenerse si hay conflicto con la arquitectura
3. **DOCUMENTACIÓN CONTINUA** — Actualizar docs + CHANGELOG después de cada cambio
4. **SEGURIDAD** — Nunca deploy/push/cambios destructivos sin confirmación

## Documentación del Proyecto
| Doc | Cuándo leerlo |
|-----|--------------|
| `docs/01-project-overview.md` | SIEMPRE (visión, stack, estado) |
| `docs/02-architecture.md` | SIEMPRE (estructura, convenciones) |
| `docs/03-security.md` | Si se toca headers, CDNs, seguridad |
| `docs/04-deployment.md` | Si se toca deploy, Netlify |
| `docs/DB_SCHEMA.md` | N/A (sitio estático) |
| `docs/API_DOCS.md` | Si se agregan servicios externos |
| `docs/SKILLS.md` | ANTES de implementar cualquier feature nueva |
| `docs/features/*.md` | El doc de la feature que se modifica |

## Tabla de Lookup
| Archivo que se modifica | Doc que se debe leer |
|------------------------|---------------------|
| `index.html` | `docs/01-project-overview.md` + `docs/SKILLS.md` |
| `restaurantqr.html` | `docs/features/restaurantqr-showcase.md` + `docs/SKILLS.md` |
| `netlify.toml` | `docs/03-security.md` + `docs/04-deployment.md` |
| `public/**` | `docs/02-architecture.md` |

## Local Server
- Servir en localhost: `node serve.mjs` (puerto 3000)
- Screenshots: `node screenshot.mjs http://localhost:3000`

## Design System
- **Colores:** brand (#2E7BF6), teal (#00CFFF), surface (#070E1A), dark (#040B14)
- **Fuente:** Inter (considerar upgrade a tipografía más distintiva para headings en rediseño)
- **Estilo:** Dark mode, dot grid background, grain overlay, glassmorphism nav
