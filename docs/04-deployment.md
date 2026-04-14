# Deployment — Luis Moreno Website

## Repositorios Git
| Remote | URL | Uso |
|--------|-----|-----|
| `selling` (principal) | https://github.com/josemorenoso/selling-website.git | Conectado a Vercel — deploy automático |
| `origin` (legacy) | https://github.com/josemorenoso/My-website.git | Repo original, backup |

## Vercel Project
- **Dashboard:** https://vercel.com/josemorenosos-projects/selling-website
- **Deploy:** Automático en push a `main` del repo `selling-website`
- **Comando push:** `git push selling main`

## Plataforma
**Vercel** — Deploy automático desde GitHub

## Proceso de Deploy
1. Push a rama `main` en GitHub
2. Vercel detecta el cambio automáticamente
3. No hay build step — se sirven los archivos estáticos directamente
4. Headers de seguridad se aplican desde `vercel.json`

## Configuración
- **Framework preset:** Other (static)
- **Build command:** Ninguno
- **Output directory:** `.` (raíz del proyecto)
- **Headers:** Definidos en `vercel.json`

## Dominio
- Pendiente de configuración con dominio personalizado
- Vercel provee dominio `.vercel.app` por defecto

## Checklist Pre-Deploy
- [ ] Todas las imágenes optimizadas (WebP cuando posible)
- [ ] Links de Calendly verificados y funcionales
- [ ] Links de Instagram actualizados (no `YOUR_HANDLE`)
- [ ] `vercel.json` con headers de seguridad correctos
- [ ] `robots.txt` actualizado
- [ ] Meta tags (title, description, OG) en todas las páginas
- [ ] Responsive verificado en mobile, tablet y desktop
- [ ] Performance > 90 en Lighthouse
- [ ] Sin errores en consola del navegador
- [ ] URL de demo RestaurantQR funcional (iframe embed)
