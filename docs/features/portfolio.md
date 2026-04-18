# Feature: Portafolio de Automatizaciones

**Fecha:** 2026-04-16  
**Estado:** En implementación  
**Spec de diseño:** `docs/superpowers/specs/2026-04-16-portfolio-automatizaciones-design.md`

---

## Descripción

Sección `#portafolio` en `index.html` con 5 herramientas de automatización reales. Cada herramienta tiene una card pública descriptiva y una demo protegida por PIN en `/demos/`.

---

## Las 5 Herramientas

| # | Nombre | Slug | Estado | Demo |
|---|--------|------|--------|------|
| 1 | Fidelización de Clientes para Restaurantes | `restaurantes` | ✅ Existe (Next.js + Vercel) | iframe embed |
| 2 | Agente IA de Reservas Hoteleras | `hoteles` | ✅ Existe (n8n + QloApps) | Widget chat n8n |
| 3 | Captador Automático de Clientes | `prospectos` | 🆕 Nuevo (workflow n8n) | Formulario → email |
| 4 | Reporte Semanal de Negocio | `reporte` | 🆕 Nuevo (workflow n8n) | Formulario → email |
| 5 | Cotizador Profesional Instantáneo | `presupuestos` | 🆕 Nuevo (workflow n8n) | Formulario → 2 emails |

---

## Estructura de Archivos

```
demos/
├── index.html              → PIN gate (JS puro, sessionStorage)
├── shared.css              → Estilos oscuros compartidos
├── restaurantes.html       → iframe Vercel
├── hoteles.html            → Widget chat n8n embebido
├── prospectos.html         → Formulario lead → email
├── reporte.html            → Trigger reporte → email
└── presupuestos.html       → Formulario cotización → 2 emails

workflows/
├── captador-prospectos.json
├── reporte-negocio.json
├── creador-presupuestos.json
├── hotel-booking-ai-agent-v3.json        (copiado de existente)
├── qloapps-check-availability-v10.json   (copiado de existente)
└── qloapps-generate-link-v10.json        (copiado de existente)
```

---

## Flujo de PIN

1. Usuario llega a `/demos/?tool=prospectos`
2. `demos/index.html` verifica `sessionStorage.getItem('demo_access')`
3. Si no hay acceso → muestra pantalla de PIN
4. PIN correcto → `sessionStorage.setItem('demo_access', 'true')` + redirect
5. Cada demo page verifica el flag al cargar; si no existe → redirige a `/demos/`
6. PIN se define como constante JS en `demos/index.html`

---

## Configuración Post-Deploy

### Webhook URLs (reemplazar en cada demo page)
- `demos/prospectos.html` → `const WEBHOOK_URL = "https://TU_N8N/webhook/captador-prospectos"`
- `demos/reporte.html` → `const WEBHOOK_URL = "https://TU_N8N/webhook/reporte-negocio"`
- `demos/presupuestos.html` → `const WEBHOOK_URL = "https://TU_N8N/webhook/presupuestos"`
- `demos/hoteles.html` → `const N8N_CHAT_URL = "https://TU_N8N/webhook/hotel-chat"`

### PIN
- `demos/index.html` → `const DEMO_PIN = "0000"` (cambiar por PIN real)

### Workflows n8n
1. Importar los 3 JSON nuevos en n8n
2. Configurar credenciales Gmail en cada workflow
3. Reemplazar `tuemail@gmail.com` por el correo real
4. Activar los workflows

### Credenciales requeridas para workflows de hotel
- Telegram Centauri211
- OpenAI account
- Redis account
- Postgres account
- Supabase account
- HTTP Basic Auth para QloApps (VPS: `http://143.198.21.142:8080/`)
