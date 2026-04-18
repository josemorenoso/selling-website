# FASE 3 — Rediseño para Autoridad, Confianza y Credibilidad

**Fecha inicio:** 2026-04-18
**Estado:** EN PROGRESO
**Archivo persistente:** Este documento mantiene el contexto completo entre sesiones.

---

## OBJETIVO PRINCIPAL (NO CAMBIAR)

Crear una página web que genere **confianza, credibilidad y autoridad inmediata**, ultra profesional y empresarial. Debe:

- Enfocarse en qué gana el cliente ("qué hago por ti", "cómo ganas si me contratas")
- Generar dopamina con métricas que enamoren
- Vender futuro, crecimiento, cambio y transformación
- Al leerla, el visitante debe pensar: **"Sabe exactamente lo que hace"**
- Llevar al usuario a querer agendar cita YA
- NO comunicación vacía, NO palabras puestas por poner

**Referencia de lenguaje y estructura:** `https://admirable-liger-25cfe0.netlify.app/#nosotros` (ver `Guide/admirable-liger-25cfe0.netlify.app_ (1).png`)

---

## ERRORES CRÍTICOS A CORREGIR

### 1. Legibilidad (ERROR GARRAFAL)
- Fondo transparente + letras grises disminuye lectura
- Debe ser **legible** y **profesional**

### 2. Zona "Qué hago" (Servicios)
- Falta claridad y métricas
- Los 3 recuadros deben tener formato del primero (ver `Guide/Captura de pantalla 2026-04-18 131425.png`)
- Cada card debe tener:
  - Chip superior (ej. "ATENCIÓN 24/7")
  - Título claro
  - Descripción corta y directa
  - **Métricas visuales** tipo `98% tasa de respuesta`, `<3s tiempo respuesta`, `3x más conversiones`
  - Tech chips al final

### 3. Sección Producto Estrella (ERROR GARRAFAL)
- "Restaurant QR" es nombre vacío
- Cambiar narrativa: **software replicable a escala, +30% ventas, retención, facilita vida al cliente**
- **ELIMINAR iframe actual** (muestra métricas vacías en cero, parece Excel)
- Reemplazar por iframe del link real: `https://restaurant-fidelity-system.vercel.app/`
- Usuarios entrarán con credenciales demo:
  - `demo@gmail.com` / `123456789`
- Pre-llenar credenciales SOLO si es fácil (no hacer si requiere muchos cambios al sistema)

### 4. Zona "Costo de no actuar" (ZONA MÁS CRÍTICA)
- Lenguaje vacío, métricas poco claras
- **RECONCEPTUALIZAR** como "Por qué debes trabajar conmigo"
- Reciclar contenido pero con palabras que resuenen
- Generar autoridad, confianza y credibilidad inmediata

### 5. Zona "Quién soy"
- **ELIMINAR "Ingeniero"** — NO es ingeniero
- Correcto: **Especialista en automatizaciones, desarrollo de web apps y sistemas de IA**

### 6. Portafolio
- Añadir separación visual clara del resto del sitio
- Mejorar vocabulario de cada tarjeta — "diamante en bruto"
- Arreglar conexión web ↔ n8n (credenciales ya cargadas por Luis)

### 7. Workflows n8n — URLs actualizadas
- `https://n8n.almojabananet.me/webhook/presupuestos`
- `https://n8n.almojabananet.me/webhook/reporte-negocio`
- `https://n8n.almojabananet.me/webhook-test/captador-prospectos` (¡webhook-test, no webhook!)
- `https://n8n.almojabananet.me/webhook/7b5ada29-dc7b-44fb-b094-37c753ed69b6/chat`

### 8. PIN Gate
- Debe pedir PIN **cada vez** que se sale y vuelve a entrar a `/demos/`

### 9. Zona "Cómo lo hacemos" (Metodología)
- PERFECTA — solo aumentar legibilidad (no cambiar estructura)

---

## TO-DO LIST DETALLADA (ESTADO)

| # | Tarea | Archivo | Estado |
|---|-------|---------|--------|
| 1 | Crear progress file y todo list | `docs/progress/fase-3-...md` | ✅ DONE |
| 2 | Fix legibilidad global (contraste texto/fondo) | `index.html` (CSS `.muted`, `.dimmed`) | ⏳ |
| 3 | Rediseñar zona Servicios con 3 cards simétricas + métricas | `index.html` sección servicios | ⏳ |
| 4 | Rediseñar Producto Estrella: nuevo nombre + iframe real | `index.html` sección #producto | ⏳ |
| 5 | Reemplazar "Costo de no actuar" por "Por qué trabajar conmigo" | `index.html` sección cost | ⏳ |
| 6 | Aumentar legibilidad en "Metodología" | `index.html` sección #metodologia | ⏳ |
| 7 | Separar Portafolio visualmente + mejorar vocabulario | `index.html` sección #portafolio | ⏳ |
| 8 | Eliminar "Ingeniero" de "Quién soy" | `index.html` sección #sobre-mi | ⏳ |
| 9 | Arreglar PIN gate (siempre pedir al re-entrar) | `demos/index.html` | ⏳ |
| 10 | Actualizar webhook URLs (captador-prospectos → /webhook-test/) | `demos/prospectos.html` | ⏳ |
| 11 | Verificar que los demos envían JSON correcto al webhook n8n | todas las `demos/*.html` | ⏳ |
| 12 | Actualizar CHANGELOG a v0.5.0 | `CHANGELOG.md` | ⏳ |
| 13 | Actualizar `docs/features/portfolio.md` + crear `docs/features/redesign-autoridad.md` | `docs/features/` | ⏳ |

---

## CONTEXTO TÉCNICO

### Paleta (inmutable)
- Brand: `#2E7BF6`
- Teal: `#00CFFF`
- Surface: `#070E1A`
- Dark: `#040B14`
- Text principal: `#F0F5FF` / `#E8EDF5`
- Text secundario: `#B0BFCF` (más legible que gris)
- Dimmed: `#8A9BB0`

### Sobre legibilidad
Los colores `.muted` y `.dimmed` actualmente son muy tenues sobre fondos transparentes. La corrección consiste en:
- Subir opacidad/luminosidad de estos colores
- Asegurar contraste mínimo 4.5:1 (WCAG AA) en body text
- Headings deben ir en `#F0F5FF` sólido

### Referencia admirable-liger
- CTAs naranjas brillantes
- Cards blancas con shadow suave
- Bullet lists dentro de cards (claridad)
- Stats bar con métricas grandes: "+50", "80%", "3x", "100%"
- Heading patterns: "Soluciones integrales para hacer crecer tu negocio"
- Sección "Del diagnóstico a los resultados en cuatro pasos"

### Referencia de métricas en cards (imagen 131425)
```
┌─────────────────────┐
│ ● ATENCIÓN 24/7     │
│                     │
│ Agentes de IA para  │
│ Atención al Cliente │
│                     │
│ [descripción]       │
│                     │
│ ┌──────┬──────┐     │
│ │ 98%  │ <3s  │     │
│ │ tasa │ resp │     │
│ └──────┴──────┘     │
│                     │
│ [WhatsApp] [IG]     │
└─────────────────────┘
```

---

## DECISIONES TOMADAS

- **RestaurantQR** → renombrar (propuesta: mantener como producto principal pero con copy más fuerte)
- **Pre-fill credenciales demo**: investigar si la app acepta `?email=demo@gmail.com&password=123456789` como query params; si no, NO modificar
- **Workflow n8n Captador Prospectos**: cambiar de `/webhook/` a `/webhook-test/` en la URL del form

---

## LOG DE SESIÓN

### Sesión 2026-04-18 (en curso)
- Creado este progress file
- Analizadas 3 imágenes de referencia
- Pendiente: ejecutar tareas 2-13 en orden
