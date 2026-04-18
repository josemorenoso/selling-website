# Portafolio de Automatizaciones — Diseño

**Fecha:** 2026-04-16  
**Autor:** Luis Moreno  
**Estado:** Aprobado para implementación

---

## Problema

El sitio web actualmente tiene solo un producto de showcase (RestaurantQR). Para convencer a nuevos clientes, Luis necesita demostrar capacidad con múltiples herramientas reales y funcionales que pueda mostrar en reuniones de venta.

## Objetivo

Agregar una sección `#portafolio` al sitio con 5 herramientas de automatización funcionando en vivo, protegidas por PIN para que solo Luis pueda acceder a las demos durante reuniones con clientes.

---

## Las 5 Herramientas

### 1. Fidelización de Clientes para Restaurantes
- **Contexto:** Plataforma completa de fidelización para restaurantes.
- **Estado:** Ya existe (app Next.js en Vercel + Supabase + Twilio)
- **Demo:** iframe embed del dashboard real
- **Tags:** Restaurantes, WhatsApp, CRM

### 2. Asistente IA de Reservas Hoteleras
- **Contexto:** Chatbot inteligente para hoteles conectado a QloApps (software hotelero open-source) vía n8n en VPS de Luis.
- **Estado:** Ya existe en n8n, necesita pulido mínimo
- **Demo:** Widget de chat nativo de n8n embebido
- **Tags:** Hoteles, IA, Reservas

### 3. Captador Automático de Clientes
- **Contexto:** Una agencia de marketing captura leads de sus campañas. Cada prospecto que llena el formulario activa una secuencia: Luis recibe el lead calificado por correo y el prospecto recibe un mensaje de confirmación automático.
- **Estado:** Por crear (workflow n8n JSON)
- **Demo:** Formulario → correo a Luis + auto-reply al prospecto
- **Tags:** Leads, Email, Prospección

### 4. Reporte Semanal de Negocio
- **Contexto:** Un negocio de retail quiere recibir cada lunes un resumen ejecutivo de su semana. Con un clic (o programado), el dueño recibe un reporte HTML estructurado con KPIs, análisis y acciones recomendadas.
- **Estado:** Por crear (workflow n8n JSON)
- **Demo:** Formulario con nombre del negocio + período → email con reporte
- **Tags:** Reportes, Email, Análisis

### 5. Cotizador Profesional Instantáneo
- **Contexto:** Un consultor necesita enviar propuestas rápidas a sus clientes. Llena un formulario con los servicios, y en segundos el cliente recibe una cotización profesional por correo y Luis recibe una copia.
- **Estado:** Por crear (workflow n8n JSON)
- **Demo:** Formulario con servicios + precios dinámicos → 2 correos (cliente + Luis)
- **Tags:** Ventas, Email, Cotizaciones

---

## Arquitectura del Sistema de Demos

### Acceso Público (index.html)
- Sección `#portafolio` visible para todos
- 5 cards con título, descripción, tags y botón "Ver Demo"
- El botón abre `/demos/` con el parámetro `?tool=X`

### Acceso Protegido (/demos/)
```
/demos/index.html          → PIN gate (JS puro, sessionStorage)
/demos/shared.css          → estilos oscuros compartidos
/demos/restaurantes.html   → iframe Vercel
/demos/hoteles.html        → embed widget chat n8n
/demos/prospectos.html     → formulario lead → email
/demos/reporte.html        → trigger reporte → email
/demos/presupuestos.html   → formulario cotización → 2 emails
```

### Flujo de Autenticación
1. Usuario llega a `/demos/?tool=prospectos`
2. `demos/index.html` verifica `sessionStorage.getItem('demo_access')`
3. Si no hay acceso → muestra pantalla de PIN
4. PIN correcto → `sessionStorage.setItem('demo_access', 'true')` + redirect a la tool
5. Cada demo page verifica el flag al cargar; si no existe → redirige a `/demos/`
6. El PIN se define como constante JS en `demos/index.html` (Luis lo cambia)

---

## Workflows n8n (JSON importables)

### captador-prospectos.json
```
Nodos:
  Webhook (POST) → Code (formatear + score) → Gmail (a Luis) → Gmail (auto-reply al lead)
Inputs: nombre, email, telefono, empresa, servicio, presupuesto
Output email a Luis: card HTML con datos del lead + puntuación de calificación
Output email al lead: confirmación + próximos pasos
```

### reporte-negocio.json
```
Nodos:
  Webhook (POST) → Code (generar reporte con datos demo) → Gmail
Inputs: nombre_negocio, periodo
Output: email HTML con métricas, análisis, recomendaciones (datos ficticios para demo)
```

### creador-presupuestos.json
```
Nodos:
  Webhook (POST) → Code (calcular totales + fecha expiración) → Gmail (cliente) → Gmail (Luis)
Inputs: cliente_nombre, cliente_email, servicios[], notas
Output cliente: cotización profesional HTML con líneas, total, vigencia
Output Luis: copia exacta con confirmación de envío
```

### Configuración requerida por Luis
Cada demo page tiene al inicio:
```javascript
const WEBHOOK_URL = "https://TU_VPS/webhook/NOMBRE_WORKFLOW";
```
Luis reemplaza estas URLs después de importar los workflows en su n8n.

---

## Diseño Visual

### Sección #portafolio en index.html
- Posición: después de `#metodologia`, antes de `#sobre-mi`
- Grid: `repeat(3, 1fr)` desktop → `repeat(2, 1fr)` tablet → `1fr` mobile
- Cards: reutilizar clase `.card` existente + `.glass-card` para hover
- Cada card: icono SVG inline, título, descripción 2 líneas, 3 chips de tags, botón `.btn-cta`
- Animaciones: reutilizar `[data-a]` y `[data-d]` existentes

### Demo Pages
- Background: `#040B14` (idéntico al sitio)
- Fuente: Inter (Google Fonts)
- Formularios: inputs oscuros, borde `rgba(255,255,255,0.1)`, radio `0.5rem`
- Botón submit: clase `.btn-cta` replicada
- Estados: success (verde), error (rojo), loading (spinner azul)
- Max-width: `480px` centrado para formularios

---

## Consideraciones de Seguridad

- PIN en JavaScript es seguridad por oscuridad, suficiente para este caso de uso (demo en reuniones, no datos sensibles)
- sessionStorage se limpia al cerrar el navegador — Luis necesita ingresar PIN en cada sesión nueva
- Los workflows n8n están en VPS privado de Luis (no expuestos públicamente más allá del webhook URL)
- No se almacenan datos sensibles en el frontend

---

## Verificación

1. `/demos/` sin PIN → pantalla de PIN
2. PIN incorrecto → mensaje de error
3. PIN correcto → redirige a la tool solicitada
4. Formulario prospectos → correo llega a inbox de Luis
5. Trigger reporte → correo con reporte HTML llega
6. Formulario presupuestos → correo al cliente + copia a Luis
7. Actualizar navegador en demo page sin nuevo PIN → redirige (sessionStorage vacío)
8. Sección portafolio: 5 cards visibles, grid correcto en mobile
9. Nav link "Portafolio" → scroll a la sección
10. Screenshot: `node screenshot.mjs http://localhost:3000`
