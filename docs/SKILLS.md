# Skills Instaladas

> Última actualización: 2025-04-13
> Este archivo registra todas las skills, extensiones, MCP servers y herramientas
> especializadas disponibles en el entorno de desarrollo.

---

## ¿Qué son las Skills?

Las skills son capacidades especializadas que la IA puede usar para implementar
funcionalidades de forma más eficiente y correcta. Antes de implementar cualquier
feature, la IA DEBE consultar este archivo para verificar si existe una skill
relevante.

---

## Skills Activas

| # | Nombre | Tipo | Descripción | Usar cuando |
|---|--------|------|-------------|-------------|
| 1 | frontend-design | skill | Crea interfaces frontend distintivas de grado producción con alta calidad de diseño. Evita estéticas genéricas "AI slop". Guía creación de UI con tipografía única, colores cohesivos, animaciones, composición espacial asimétrica, fondos con profundidad. | Al construir cualquier componente web, página, landing, dashboard o UI. SIEMPRE invocar antes de escribir código frontend. |

---

## Detalle de Skills

### 1. frontend-design (Anthropic)
**Fuente:** https://github.com/anthropics/skills/tree/main/skills/frontend-design
**Instalada:** 2025-04-13

**Qué hace:**
- Guía la creación de interfaces web que evitan estéticas genéricas de IA
- Enfatiza: tipografía distintiva, paletas de color con carácter, animaciones intencionales, layouts inesperados, fondos con atmósfera
- Prohíbe: fuentes genéricas (Inter como default, Arial, Roboto), esquemas de color cliché, layouts predecibles

**Cuándo usarla:**
- SIEMPRE antes de escribir cualquier código frontend
- Al diseñar nuevas secciones o páginas
- Al rediseñar componentes existentes
- Al crear el dashboard demo de RestaurantQR

**Principios clave:**
1. **Design Thinking primero:** Propósito → Tono → Constraints → Diferenciación
2. **Tipografía:** Fuentes únicas y memorables, NO genéricas. Pair display + body
3. **Color:** Paleta cohesiva con CSS variables. Color dominante + acentos sharp
4. **Motion:** Animaciones CSS-first. Staggered reveals > micro-interactions dispersas
5. **Composición:** Asimetría, overlap, diagonal flow, negative space intencional
6. **Fondos:** Gradient meshes, noise, patrones geométricos, grain overlays
7. **NUNCA:** Inter/Roboto/Arial como default, gradientes purple-on-white, layouts cookie-cutter

**Nota para este proyecto:** El sitio actual usa Inter como fuente principal. En el rediseño (FASE 2) se debe considerar reemplazar con una tipografía más distintiva para headings, manteniendo Inter o similar para body text si es legible.

---

## MCP Servers Conectados

| # | Servidor | Herramientas | Descripción | Usar cuando |
|---|----------|-------------|-------------|-------------|
| - | Ninguno actualmente | - | - | - |

---

## Historial de Skills

| Fecha | Acción | Skill | Motivo |
|-------|--------|-------|--------|
| 2025-04-13 | Instalada | frontend-design | Skill oficial de Anthropic para diseño frontend de alta calidad. Necesaria para lograr el objetivo de que el sitio "parezca de $10K" |
