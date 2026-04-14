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
6. Si se implementa UI → LEER `docs/SKILLS.md`

## Los 12 Mandamientos del Vibe Coding (INVIOLABLES)
| # | Mandamiento | Regla |
|---|-------------|-------|
| I | NO ALUCINARÁS | Solo implementar exactamente lo pedido |
| II | SEPARARÁS LÓGICA DE ESTILOS | Nunca mezclar |
| III | DOCUMENTARÁS CADA CAMBIO | Ningún cambio sin doc |
| IV | ACTUALIZARÁS EL CHANGELOG | Cada request → nueva entrada |
| V | DOCUMENTARÁS LA DB | N/A (sitio estático) |
| VI | SEGUIRÁS LA ESTRUCTURA | No crear fuera de estructura |
| VII | USARÁS EL SISTEMA DE ESTILOS | Respetar design system |
| VIII | PROTEGERÁS CREDENCIALES | Nada hardcodeado |
| IX | TIPARÁS TODO | N/A (Vanilla JS) |
| X | VALIDARÁS ANTES DE ENTREGAR | Checklist obligatorio |
| XI | MANTENDRÁS CONSISTENCIA | Seguir convenciones |
| XII | COMUNICARÁS CON CLARIDAD | Resumen al terminar |

## 4 Leyes de Operación
1. **LEER ANTES DE ACTUAR**
2. **NO ROMPER LO QUE FUNCIONA**
3. **DOCUMENTACIÓN CONTINUA**
4. **SEGURIDAD** — Nunca deploy/push sin confirmación

## Design System
- **Colores:** brand (#2E7BF6), teal (#00CFFF), surface (#070E1A), dark (#040B14)
- **Fuente:** Inter (upgrade planificado)
- **Estilo:** Dark mode, dot grid, grain overlay, glassmorphism

## Tabla de Lookup
| Archivo | Doc a leer |
|---------|-----------|
| `index.html` | `docs/01-project-overview.md` + `docs/SKILLS.md` |
| `restaurantqr.html` | `docs/features/restaurantqr-showcase.md` + `docs/SKILLS.md` |
| `netlify.toml` | `docs/03-security.md` + `docs/04-deployment.md` |
