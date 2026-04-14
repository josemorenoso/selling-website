# Seguridad — Luis Moreno Website

## Autenticación
No aplica — sitio estático público sin login ni áreas protegidas.

## Autorización
No aplica — no hay roles ni permisos.

## Variables de Entorno
No hay variables de entorno en runtime. El sitio es 100% estático.
- URLs de Calendly y redes sociales son públicas y están en el HTML
- No hay API keys, tokens ni secretos

## Headers de Seguridad (Netlify)
Configurados en `netlify.toml`:
- **X-Frame-Options:** DENY (previene clickjacking)
- **X-Content-Type-Options:** nosniff (previene MIME sniffing)
- **Referrer-Policy:** strict-origin-when-cross-origin
- **Permissions-Policy:** camera=(), microphone=(), geolocation=(), payment=()
- **Strict-Transport-Security:** max-age=31536000; includeSubDomains
- **Content-Security-Policy:** Permite scripts inline (Tailwind config), CDNs usados (tailwindcss, cloudflare), Google Fonts

## Reglas INVIOLABLES
- NUNCA hardcodear credenciales (no aplica actualmente pero regla preventiva)
- NUNCA agregar formularios que envíen datos sin validación
- NUNCA incluir scripts de terceros no verificados
- SIEMPRE servir por HTTPS (Netlify lo maneja automáticamente)
- SIEMPRE mantener los headers de seguridad en `netlify.toml`
- Si se agrega un formulario en el futuro → usar Netlify Forms o servicio externo validado

## CDNs Externos Permitidos
| CDN | Recurso | Justificación |
|-----|---------|---------------|
| cdn.tailwindcss.com | TailwindCSS runtime | Sistema de estilos |
| cdnjs.cloudflare.com | Three.js r134 | Background 3D |
| fonts.googleapis.com | Inter font | Tipografía |
| fonts.gstatic.com | Font files | Archivos de fuentes |
