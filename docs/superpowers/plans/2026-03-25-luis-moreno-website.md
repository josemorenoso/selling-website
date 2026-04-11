# Luis Moreno Website — Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build a single `index.html` high-conversion personal brand website for Luis Moreno that drives Calendly bookings from business owners seeking automation.

**Architecture:** Single `index.html` with all styles inline via Tailwind CDN + custom `<style>` block. Node.js `serve.mjs` serves the file at localhost:3000. Puppeteer `screenshot.mjs` captures full-page screenshots for visual review. No build step, no framework.

**Tech Stack:** Tailwind CSS CDN, Space Grotesk + Inter (Google Fonts), Puppeteer (npm), Node.js ESM modules.

**Spec:** `docs/superpowers/specs/2026-03-25-luis-moreno-website-design.md`

**Photo asset:** `Photo of my self.jpg` (project root) — reference as `/Photo of my self.jpg` from the server.

---

## File Map

| File | Purpose |
|---|---|
| `index.html` | Single deliverable — all HTML, CSS (inline Tailwind + custom), JS |
| `serve.mjs` | Node.js static file server at localhost:3000 |
| `screenshot.mjs` | Puppeteer full-page screenshot script |
| `package.json` | npm config for Puppeteer dependency |
| `temporary screenshots/` | Auto-created by screenshot.mjs |

---

## Task 1: Infrastructure — serve.mjs, screenshot.mjs, package.json, Puppeteer

**Files:**
- Create: `package.json`
- Create: `serve.mjs`
- Create: `screenshot.mjs`

- [ ] **Step 1: Create package.json**

```json
{
  "name": "luis-moreno-website",
  "version": "1.0.0",
  "type": "module",
  "scripts": {
    "serve": "node serve.mjs",
    "screenshot": "node screenshot.mjs http://localhost:3000"
  }
}
```

- [ ] **Step 2: Install Puppeteer**

Run from project root (`c:/Users/luisr/Downloads/Web desing v.2/`):
```bash
npm install puppeteer
```
Expected: Downloads Puppeteer + Chrome binary (~170MB). Takes 1-3 minutes. Output ends with `added X packages`.

- [ ] **Step 3: Create serve.mjs**

```javascript
import { createServer } from 'http';
import { readFile } from 'fs/promises';
import { extname, join } from 'path';
import { fileURLToPath } from 'url';
import { dirname } from 'path';

const __dirname = dirname(fileURLToPath(import.meta.url));
const PORT = 3000;

const mime = {
  '.html': 'text/html', '.css': 'text/css', '.js': 'application/javascript',
  '.json': 'application/json', '.png': 'image/png', '.jpg': 'image/jpeg',
  '.jpeg': 'image/jpeg', '.svg': 'image/svg+xml', '.ico': 'image/x-icon',
  '.woff2': 'font/woff2', '.webp': 'image/webp',
};

createServer(async (req, res) => {
  const url = decodeURIComponent(req.url === '/' ? '/index.html' : req.url);
  const filePath = join(__dirname, url);
  try {
    const data = await readFile(filePath);
    res.writeHead(200, { 'Content-Type': mime[extname(filePath)] || 'text/plain' });
    res.end(data);
  } catch {
    res.writeHead(404);
    res.end('Not found');
  }
}).listen(PORT, () => console.log(`Server: http://localhost:${PORT}`));
```

- [ ] **Step 4: Create screenshot.mjs**

```javascript
import puppeteer from 'puppeteer';
import { mkdir, access } from 'fs/promises';
import { join, dirname } from 'path';
import { fileURLToPath } from 'url';

const __dirname = dirname(fileURLToPath(import.meta.url));
const dir = join(__dirname, 'temporary screenshots');
const url = process.argv[2] || 'http://localhost:3000';
const label = process.argv[3] || '';

async function nextName() {
  let i = 1;
  while (true) {
    const name = label ? `screenshot-${i}-${label}.png` : `screenshot-${i}.png`;
    try { await access(join(dir, name)); i++; }
    catch { return { i, name }; }
  }
}

(async () => {
  await mkdir(dir, { recursive: true });
  const { name } = await nextName();
  const out = join(dir, name);
  const browser = await puppeteer.launch({ headless: true });
  const page = await browser.newPage();
  await page.setViewport({ width: 1440, height: 900 });
  await page.goto(url, { waitUntil: 'networkidle0', timeout: 30000 });
  await page.screenshot({ path: out, fullPage: true });
  await browser.close();
  console.log(`Saved: ${out}`);
})().catch(console.error);
```

- [ ] **Step 5: Verify server works**

Run in background: `node serve.mjs`
Expected: `Server: http://localhost:3000`
(No index.html yet — 404 is fine. Verify the server starts without crashing.)

---

## Task 2: HTML Shell + Design System

**Files:**
- Create: `index.html`

- [ ] **Step 1: Create the HTML shell with Tailwind config, fonts, and design system styles**

Create `index.html` with this exact content:

```html
<!DOCTYPE html>
<html lang="es" class="scroll-smooth">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Luis Moreno — Automatización para Negocios</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@400;500;600;700&family=Inter:wght@400;500;600&display=swap" rel="stylesheet">
  <script>
    tailwind.config = {
      theme: {
        extend: {
          colors: {
            brand: '#2E7BF6',
            surface: '#0d0d14',
            dark: '#060609',
          },
          fontFamily: {
            sans: ['Inter', 'system-ui', 'sans-serif'],
            display: ['"Space Grotesk"', 'system-ui', 'sans-serif'],
          },
        }
      }
    }
  </script>
  <style>
    *, *::before, *::after { box-sizing: border-box; }
    html { scroll-behavior: smooth; }
    body {
      background-color: #060609;
      color: #F0F0F5;
      font-family: 'Inter', system-ui, sans-serif;
      -webkit-font-smoothing: antialiased;
      min-width: 320px;
      overflow-x: hidden;
    }

    /* Grain overlay */
    body::before {
      content: '';
      position: fixed;
      inset: 0;
      background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='300' height='300'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.75' numOctaves='4' stitchTiles='stitch'/%3E%3CfeColorMatrix type='saturate' values='0'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)'/%3E%3C/svg%3E");
      opacity: 0.035;
      pointer-events: none;
      z-index: 9998;
    }

    /* Scroll animation base */
    [data-animate] {
      opacity: 0;
      transform: translateY(28px);
      transition: opacity 0.65s cubic-bezier(0.16,1,0.3,1), transform 0.65s cubic-bezier(0.16,1,0.3,1);
    }
    [data-animate].in { opacity: 1; transform: translateY(0); }
    [data-animate][data-delay="1"] { transition-delay: 0.1s; }
    [data-animate][data-delay="2"] { transition-delay: 0.2s; }
    [data-animate][data-delay="3"] { transition-delay: 0.3s; }
    [data-animate][data-delay="4"] { transition-delay: 0.4s; }

    /* Navbar */
    #navbar {
      transition: background-color 0.3s ease, border-color 0.3s ease, backdrop-filter 0.3s ease;
    }
    #navbar.scrolled {
      background-color: rgba(6,6,9,0.85);
      border-bottom: 1px solid rgba(255,255,255,0.07);
      backdrop-filter: blur(16px);
      -webkit-backdrop-filter: blur(16px);
    }

    /* Primary button */
    .btn-primary {
      display: inline-flex;
      align-items: center;
      gap: 0.375rem;
      background: #2E7BF6;
      color: #fff;
      font-family: 'Space Grotesk', system-ui, sans-serif;
      font-weight: 600;
      font-size: 0.9375rem;
      padding: 0.75rem 1.5rem;
      border-radius: 0.5rem;
      border: none;
      cursor: pointer;
      text-decoration: none;
      transition: transform 0.18s cubic-bezier(0.16,1,0.3,1), box-shadow 0.18s cubic-bezier(0.16,1,0.3,1);
      position: relative;
    }
    .btn-primary:hover {
      transform: translateY(-2px);
      box-shadow: 0 8px 32px rgba(46,123,246,0.45), 0 0 0 1px rgba(46,123,246,0.25);
    }
    .btn-primary:focus-visible {
      outline: 2px solid #2E7BF6;
      outline-offset: 3px;
    }
    .btn-primary:active { transform: translateY(0); }

    /* Secondary button */
    .btn-secondary {
      display: inline-flex;
      align-items: center;
      gap: 0.375rem;
      background: transparent;
      color: #F0F0F5;
      font-family: 'Space Grotesk', system-ui, sans-serif;
      font-weight: 500;
      font-size: 0.9375rem;
      padding: 0.75rem 1.5rem;
      border-radius: 0.5rem;
      border: 1px solid rgba(255,255,255,0.12);
      cursor: pointer;
      text-decoration: none;
      transition: border-color 0.18s ease, background-color 0.18s ease;
    }
    .btn-secondary:hover { border-color: rgba(255,255,255,0.28); background-color: rgba(255,255,255,0.04); }
    .btn-secondary:focus-visible { outline: 2px solid #2E7BF6; outline-offset: 3px; }
    .btn-secondary:active { background-color: rgba(255,255,255,0.07); }

    /* Card */
    .card {
      background: #0d0d14;
      border: 1px solid rgba(255,255,255,0.07);
      border-radius: 1rem;
      transition: border-color 0.3s ease, box-shadow 0.3s ease;
    }
    .card:hover { border-color: rgba(46,123,246,0.28); box-shadow: 0 0 40px rgba(46,123,246,0.07); }

    /* Section heading */
    .section-label {
      font-family: 'Space Grotesk', system-ui, sans-serif;
      font-size: 0.75rem;
      font-weight: 600;
      letter-spacing: 0.12em;
      text-transform: uppercase;
      color: #2E7BF6;
    }
    .section-heading {
      font-family: 'Space Grotesk', system-ui, sans-serif;
      font-weight: 700;
      letter-spacing: -0.03em;
      line-height: 1.15;
      color: #F0F0F5;
    }
    .section-sub {
      color: #6B7280;
      line-height: 1.7;
    }

    /* Bento grid */
    .bento { display: grid; grid-template-columns: repeat(3, 1fr); gap: 1rem; }
    .bento-wide { grid-column: span 2; }
    @media (max-width: 768px) {
      .bento { grid-template-columns: 1fr; }
      .bento-wide { grid-column: span 1; }
    }

    /* Steps connector line */
    .steps-wrap { position: relative; }
    .steps-wrap::before {
      content: '';
      position: absolute;
      top: 2rem;
      left: calc(16.5% + 2rem);
      right: calc(16.5% + 2rem);
      height: 1px;
      background: linear-gradient(to right, rgba(46,123,246,0.6), rgba(46,123,246,0.15));
      pointer-events: none;
    }
    @media (max-width: 768px) { .steps-wrap::before { display: none; } }

    /* Photo treatment */
    .photo-wrap { position: relative; border-radius: 1rem; overflow: hidden; }
    .photo-wrap img { display: block; width: 100%; height: 100%; object-fit: cover; }
    .photo-wrap::after {
      content: '';
      position: absolute;
      inset: 0;
      background: linear-gradient(to top, rgba(6,6,9,0.7) 0%, transparent 55%);
      pointer-events: none;
    }
    .photo-blue-layer {
      position: absolute;
      inset: 0;
      background: rgba(46,123,246,0.1);
      mix-blend-mode: color;
      pointer-events: none;
    }

    /* Guarantee glow */
    .guarantee-card {
      background: #0d0d14;
      border: 1px solid rgba(46,123,246,0.25);
      border-radius: 1.25rem;
      box-shadow: 0 0 60px rgba(46,123,246,0.08), inset 0 1px 0 rgba(255,255,255,0.05);
    }

    /* Tech logos strip */
    .tech-item { transition: opacity 0.2s ease; cursor: default; }
    .tech-item:hover { opacity: 0.7; }

    /* Counter */
    .counter { font-variant-numeric: tabular-nums; }

    /* Hero radial glow */
    .hero-glow {
      position: absolute;
      width: 800px;
      height: 600px;
      top: -100px;
      right: -100px;
      background: radial-gradient(ellipse at center, rgba(46,123,246,0.14) 0%, transparent 70%);
      pointer-events: none;
    }
    .hero-glow-2 {
      position: absolute;
      width: 500px;
      height: 400px;
      bottom: 0;
      left: -100px;
      background: radial-gradient(ellipse at center, rgba(139,92,246,0.07) 0%, transparent 70%);
      pointer-events: none;
    }

    /* Instagram card */
    .instagram-card {
      background: linear-gradient(135deg, #0d0d14 0%, #12101a 100%);
      border: 1px solid rgba(255,255,255,0.07);
      border-radius: 1rem;
      transition: border-color 0.3s ease;
    }
    .instagram-card:hover { border-color: rgba(193,53,132,0.3); }
  </style>
</head>
<body>

  <!-- SECTIONS WILL BE ADDED HERE -->

  <script>
    // JS WILL BE ADDED HERE
  </script>
</body>
</html>
```

- [ ] **Step 2: Take first screenshot to verify server + shell load**

```bash
node screenshot.mjs http://localhost:3000 shell
```
Expected: All-black page saved to `temporary screenshots/screenshot-1-shell.png`.
Read the file with Read tool and confirm it's black/empty — no errors.

---

## Task 3: Navbar

**Files:**
- Modify: `index.html` — replace `<!-- SECTIONS WILL BE ADDED HERE -->` comment

- [ ] **Step 1: Add the navbar HTML — replace the sections comment with:**

```html
  <!-- NAVBAR -->
  <nav id="navbar" class="fixed top-0 left-0 right-0 z-50 px-6 py-4">
    <div class="max-w-6xl mx-auto flex items-center justify-between">
      <a href="#" class="font-display font-bold text-lg text-white tracking-tight" style="font-family:'Space Grotesk',system-ui,sans-serif; letter-spacing:-0.02em;">
        Luis Moreno
      </a>
      <a href="https://calendly.com/YOUR_LINK" target="_blank" rel="noopener" class="btn-primary text-sm py-2 px-5">
        Agendar Llamada →
      </a>
    </div>
  </nav>

  <!-- SECTIONS WILL BE ADDED HERE -->
```

- [ ] **Step 2: Screenshot and verify**

```bash
node screenshot.mjs http://localhost:3000 navbar
```
Read screenshot. Verify: "Luis Moreno" wordmark visible top-left, blue "Agendar Llamada →" button top-right, transparent background over black page.

---

## Task 4: Hero Section

**Files:**
- Modify: `index.html` — replace `<!-- SECTIONS WILL BE ADDED HERE -->` comment

- [ ] **Step 1: Add Hero HTML — replace the sections comment with:**

```html
  <!-- HERO -->
  <section class="relative min-h-screen flex items-center overflow-hidden pt-20">
    <div class="hero-glow"></div>
    <div class="hero-glow-2"></div>
    <div class="max-w-6xl mx-auto px-6 py-24 relative z-10">
      <div class="max-w-3xl">
        <div class="section-label mb-6" data-animate>Automatización Done For You</div>
        <h1 class="section-heading text-5xl md:text-7xl mb-6" data-animate data-delay="1"
            style="font-size: clamp(2.8rem, 7vw, 5.5rem);">
          Tu negocio debería trabajar para ti —<br>
          <span style="color:#2E7BF6;">no al revés.</span>
        </h1>
        <p class="section-sub text-lg md:text-xl mb-8 max-w-xl" data-animate data-delay="2">
          Implemento sistemas de automatización con IA que eliminan el trabajo repetitivo de tu equipo. Tú enfocas tu energía en crecer, mientras el sistema trabaja por ti.
        </p>
        <div class="flex flex-wrap gap-4 mb-16" data-animate data-delay="3">
          <a href="https://calendly.com/YOUR_LINK" target="_blank" rel="noopener" class="btn-primary">
            Agendar Auditoría Gratuita (20 min) →
          </a>
          <a href="#metodologia" class="btn-secondary">
            Ver cómo funciona ↓
          </a>
        </div>
        <!-- Stat bar -->
        <div class="flex flex-wrap gap-8" data-animate data-delay="4">
          <div>
            <div class="text-3xl font-bold text-white counter" style="font-family:'Space Grotesk',system-ui,sans-serif; letter-spacing:-0.03em;">
              <span id="counter-hours">0</span>+ hrs/semana
            </div>
            <div class="text-sm mt-1" style="color:#6B7280;">recuperadas por cliente</div>
          </div>
          <div style="width:1px; background:rgba(255,255,255,0.1);"></div>
          <div>
            <div class="text-3xl font-bold text-white" style="font-family:'Space Grotesk',system-ui,sans-serif; letter-spacing:-0.03em;">3 semanas</div>
            <div class="text-sm mt-1" style="color:#6B7280;">implementación completa</div>
          </div>
          <div style="width:1px; background:rgba(255,255,255,0.1);"></div>
          <div>
            <div class="text-3xl font-bold text-white" style="font-family:'Space Grotesk',system-ui,sans-serif; letter-spacing:-0.03em;">&lt; 30 días</div>
            <div class="text-sm mt-1" style="color:#6B7280;">el sistema se paga solo</div>
          </div>
        </div>
      </div>
    </div>
  </section>

  <!-- SECTIONS WILL BE ADDED HERE -->
```

- [ ] **Step 2: Screenshot and verify**

```bash
node screenshot.mjs http://localhost:3000 hero
```
Read screenshot. Check: large headline visible, blue accent on "no al revés.", two CTA buttons, 3 stat items, radial glow effect in background.

---

## Task 5: Problem Agitation Section

**Files:**
- Modify: `index.html` — replace `<!-- SECTIONS WILL BE ADDED HERE -->`

- [ ] **Step 1: Add Problem Agitation HTML:**

```html
  <!-- PROBLEM AGITATION -->
  <section class="py-24 px-6" style="background: linear-gradient(to bottom, #060609, #080810, #060609);">
    <div class="max-w-6xl mx-auto">
      <div class="text-center mb-16" data-animate>
        <div class="section-label mb-4">El costo de no actuar</div>
        <h2 class="section-heading text-4xl md:text-5xl mb-4" style="font-size:clamp(2rem,5vw,3.2rem);">
          Cada día sin automatizar<br>te cuesta más de lo que crees
        </h2>
        <p class="section-sub text-lg max-w-xl mx-auto">
          Los negocios con procesos manuales no pierden tiempo — pierden dinero, talento y ventaja competitiva.
        </p>
      </div>
      <div class="grid md:grid-cols-3 gap-6 mb-12">
        <!-- Stat 1 -->
        <div class="card p-8 text-center" data-animate data-delay="1">
          <div class="text-5xl font-bold mb-3 counter" style="font-family:'Space Grotesk',system-ui,sans-serif; letter-spacing:-0.03em; color:#2E7BF6;">
            <span id="counter-hours-lost">0</span>h
          </div>
          <div class="text-white font-semibold mb-2" style="font-family:'Space Grotesk',system-ui,sans-serif;">por semana en tareas manuales</div>
          <div class="section-sub text-sm">El promedio de un equipo de 5–10 personas pierde 23 horas semanales en trabajo repetitivo que puede automatizarse hoy.</div>
        </div>
        <!-- Stat 2 -->
        <div class="card p-8 text-center" data-animate data-delay="2">
          <div class="text-5xl font-bold mb-3" style="font-family:'Space Grotesk',system-ui,sans-serif; letter-spacing:-0.03em; color:#2E7BF6;">
            <span id="counter-pct">0</span>%
          </div>
          <div class="text-white font-semibold mb-2" style="font-family:'Space Grotesk',system-ui,sans-serif;">sin ningún nivel de automatización</div>
          <div class="section-sub text-sm">De las PYMEs en Latinoamérica operan hoy con cero automatización en sus procesos internos clave.</div>
        </div>
        <!-- Stat 3 -->
        <div class="card p-8 text-center" data-animate data-delay="3">
          <div class="text-5xl font-bold mb-3" style="font-family:'Space Grotesk',system-ui,sans-serif; letter-spacing:-0.03em; color:#2E7BF6;">
            $<span id="counter-cost">0</span>
          </div>
          <div class="text-white font-semibold mb-2" style="font-family:'Space Grotesk',system-ui,sans-serif;">al mes en ineficiencia operativa</div>
          <div class="section-sub text-sm">Es el costo estimado mensual en salarios invertidos en tareas que debería manejar un sistema automatizado.</div>
        </div>
      </div>
      <div class="text-center" data-animate>
        <p class="section-sub mb-6">La pregunta no es si puedes permitirte automatizar — es si puedes permitirte <em>no</em> hacerlo.</p>
        <a href="https://calendly.com/YOUR_LINK" target="_blank" rel="noopener" class="btn-primary">
          Ver cómo recupero ese tiempo →
        </a>
      </div>
    </div>
  </section>

  <!-- SECTIONS WILL BE ADDED HERE -->
```

- [ ] **Step 2: Screenshot and verify**

```bash
node screenshot.mjs http://localhost:3000 problem
```
Read screenshot. Check: 3 stat cards with blue large numbers, card backgrounds slightly lighter than page, readable body text.

---

## Task 6: Methodology Section

**Files:**
- Modify: `index.html` — replace `<!-- SECTIONS WILL BE ADDED HERE -->`

- [ ] **Step 1: Add Methodology HTML:**

```html
  <!-- METHODOLOGY -->
  <section id="metodologia" class="py-24 px-6">
    <div class="max-w-6xl mx-auto">
      <div class="text-center mb-16" data-animate>
        <div class="section-label mb-4">El sistema</div>
        <h2 class="section-heading text-4xl md:text-5xl mb-4" style="font-size:clamp(2rem,5vw,3.2rem);">
          Cómo lo hacemos
        </h2>
        <p class="section-sub text-lg max-w-lg mx-auto">
          Modelo Done For You. Tú no aprendes herramientas — yo construyo, implemento y entreno.
        </p>
      </div>

      <!-- 3 steps -->
      <div class="steps-wrap grid md:grid-cols-3 gap-8 mb-12" data-animate>
        <div class="text-center">
          <div class="w-12 h-12 rounded-full flex items-center justify-center mx-auto mb-6 text-white font-bold text-lg"
               style="background:#2E7BF6; font-family:'Space Grotesk',system-ui,sans-serif; box-shadow: 0 0 20px rgba(46,123,246,0.4);">1</div>
          <h3 class="text-white font-semibold text-lg mb-3" style="font-family:'Space Grotesk',system-ui,sans-serif;">Identificar Procesos</h3>
          <p class="section-sub text-sm">Auditoría Express de 20 minutos. Mapeamos qué tareas consumen más tiempo y tienen mayor impacto al automatizarse.</p>
        </div>
        <div class="text-center">
          <div class="w-12 h-12 rounded-full flex items-center justify-center mx-auto mb-6 text-white font-bold text-lg"
               style="background:#2E7BF6; font-family:'Space Grotesk',system-ui,sans-serif; box-shadow: 0 0 20px rgba(46,123,246,0.4);">2</div>
          <h3 class="text-white font-semibold text-lg mb-3" style="font-family:'Space Grotesk',system-ui,sans-serif;">Documentar Flujos</h3>
          <p class="section-sub text-sm">Diseño el blueprint completo de automatización: entradas, salidas, reglas de negocio y puntos de control humano.</p>
        </div>
        <div class="text-center">
          <div class="w-12 h-12 rounded-full flex items-center justify-center mx-auto mb-6 text-white font-bold text-lg"
               style="background:#2E7BF6; font-family:'Space Grotesk',system-ui,sans-serif; box-shadow: 0 0 20px rgba(46,123,246,0.4);">3</div>
          <h3 class="text-white font-semibold text-lg mb-3" style="font-family:'Space Grotesk',system-ui,sans-serif;">Implementar y Capacitar</h3>
          <p class="section-sub text-sm">Construyo el sistema en tu infraestructura, lo pruebo en producción y entreno a tu equipo para operarlo.</p>
        </div>
      </div>

      <!-- Badge row -->
      <div class="flex flex-wrap justify-center gap-3 mb-10" data-animate>
        <span class="px-4 py-2 rounded-full text-sm font-medium" style="background:rgba(46,123,246,0.12); border:1px solid rgba(46,123,246,0.25); color:#7DAAFF; font-family:'Space Grotesk',system-ui,sans-serif;">Done For You</span>
        <span class="px-4 py-2 rounded-full text-sm font-medium" style="background:rgba(255,255,255,0.05); border:1px solid rgba(255,255,255,0.1); color:#9CA3AF;">Sin curva de aprendizaje</span>
        <span class="px-4 py-2 rounded-full text-sm font-medium" style="background:rgba(255,255,255,0.05); border:1px solid rgba(255,255,255,0.1); color:#9CA3AF;">Sin fricción</span>
        <span class="px-4 py-2 rounded-full text-sm font-medium" style="background:rgba(255,255,255,0.05); border:1px solid rgba(255,255,255,0.1); color:#9CA3AF;">Auditoría Gratis</span>
      </div>

      <div class="text-center" data-animate>
        <a href="https://calendly.com/YOUR_LINK" target="_blank" rel="noopener" class="btn-primary">
          Empieza con la Auditoría Express Gratuita →
        </a>
      </div>
    </div>
  </section>

  <!-- SECTIONS WILL BE ADDED HERE -->
```

- [ ] **Step 2: Screenshot and verify**

```bash
node screenshot.mjs http://localhost:3000 methodology
```
Read screenshot. Check: 3 numbered steps with blue circles, connector line between them (desktop), badge row below.

---

## Task 7: Unstoppable Promise Section

**Files:**
- Modify: `index.html` — replace `<!-- SECTIONS WILL BE ADDED HERE -->`

- [ ] **Step 1: Add Promise HTML:**

```html
  <!-- PROMISE -->
  <section class="py-24 px-6" style="background: linear-gradient(to bottom, #060609, #07070f, #060609);">
    <div class="max-w-6xl mx-auto">
      <div class="text-center mb-16" data-animate>
        <div class="section-label mb-4">La promesa</div>
        <h2 class="section-heading text-4xl md:text-5xl mb-4" style="font-size:clamp(2rem,5vw,3.2rem);">
          Lo que obtienes
        </h2>
        <p class="section-sub text-lg max-w-lg mx-auto">
          No prometo tecnología. Prometo transformación medible en tu operación.
        </p>
      </div>
      <div class="grid md:grid-cols-2 gap-6">
        <div class="card p-8" data-animate data-delay="1">
          <div class="text-3xl mb-4">⏱</div>
          <div class="text-2xl font-bold text-white mb-2" style="font-family:'Space Grotesk',system-ui,sans-serif; letter-spacing:-0.02em;">10+ horas por semana</div>
          <p class="section-sub">Tu equipo deja de hacer tareas repetitivas y empieza a hacer trabajo que realmente importa. Horas que vuelven a ser tuyas.</p>
        </div>
        <div class="card p-8" data-animate data-delay="2">
          <div class="text-3xl mb-4">🏖</div>
          <div class="text-2xl font-bold text-white mb-2" style="font-family:'Space Grotesk',system-ui,sans-serif; letter-spacing:-0.02em;">Tu negocio funciona sin ti</div>
          <p class="section-sub">Los procesos corren solos. El seguimiento es automático. Tú decides cuándo trabajar — y cuándo desconectarte.</p>
        </div>
        <div class="card p-8" data-animate data-delay="3">
          <div class="text-3xl mb-4">⚡</div>
          <div class="text-2xl font-bold text-white mb-2" style="font-family:'Space Grotesk',system-ui,sans-serif; letter-spacing:-0.02em;">Implementación en 3 semanas</div>
          <p class="section-sub">Sin meses de consultoría ni proyectos que nunca terminan. En 21 días tienes el sistema corriendo en producción.</p>
        </div>
        <div class="card p-8" data-animate data-delay="4">
          <div class="text-3xl mb-4">💰</div>
          <div class="text-2xl font-bold text-white mb-2" style="font-family:'Space Grotesk',system-ui,sans-serif; letter-spacing:-0.02em;">El sistema se paga solo</div>
          <p class="section-sub">En menos de 30 días, el tiempo recuperado y los errores eliminados generan más valor del que costó la implementación.</p>
        </div>
      </div>
    </div>
  </section>

  <!-- SECTIONS WILL BE ADDED HERE -->
```

- [ ] **Step 2: Screenshot and verify**

```bash
node screenshot.mjs http://localhost:3000 promise
```
Check: 2×2 grid of cards, emojis visible, bold metric text, muted body text.

---

## Task 8: Services Bento Grid

**Files:**
- Modify: `index.html` — replace `<!-- SECTIONS WILL BE ADDED HERE -->`

- [ ] **Step 1: Add Services HTML:**

```html
  <!-- SERVICES -->
  <section class="py-24 px-6">
    <div class="max-w-6xl mx-auto">
      <div class="text-center mb-16" data-animate>
        <div class="section-label mb-4">Servicios</div>
        <h2 class="section-heading text-4xl md:text-5xl mb-4" style="font-size:clamp(2rem,5vw,3.2rem);">
          Qué construyo para ti
        </h2>
        <p class="section-sub text-lg max-w-lg mx-auto">
          Sistemas de IA y automatización que corren en infraestructura real — no en herramientas de arrastrar y soltar.
        </p>
      </div>
      <div class="bento">
        <!-- Large card 1 -->
        <div class="card bento-wide p-8 relative overflow-hidden" data-animate data-delay="1" style="min-height:240px;">
          <div style="position:absolute; top:-40px; right:-40px; width:200px; height:200px; background:radial-gradient(circle, rgba(46,123,246,0.1) 0%, transparent 70%); pointer-events:none;"></div>
          <div class="text-2xl mb-4">🤖</div>
          <h3 class="text-xl font-bold text-white mb-3" style="font-family:'Space Grotesk',system-ui,sans-serif; letter-spacing:-0.02em;">Agentes de IA para Atención al Cliente</h3>
          <p class="section-sub">Agentes inteligentes que responden al instante, 24/7, en WhatsApp, Instagram y web. Calificación de leads, resolución de FAQs y escalamiento inteligente — sin intervención humana.</p>
          <div class="mt-4 flex gap-2">
            <span class="text-xs px-3 py-1 rounded-full" style="background:rgba(46,123,246,0.12); color:#7DAAFF; border:1px solid rgba(46,123,246,0.2);">24/7</span>
            <span class="text-xs px-3 py-1 rounded-full" style="background:rgba(46,123,246,0.12); color:#7DAAFF; border:1px solid rgba(46,123,246,0.2);">Multi-canal</span>
            <span class="text-xs px-3 py-1 rounded-full" style="background:rgba(46,123,246,0.12); color:#7DAAFF; border:1px solid rgba(46,123,246,0.2);">IA</span>
          </div>
        </div>
        <!-- Large card 2 -->
        <div class="card bento-wide p-8 relative overflow-hidden" data-animate data-delay="2" style="min-height:240px;">
          <div style="position:absolute; top:-40px; right:-40px; width:200px; height:200px; background:radial-gradient(circle, rgba(139,92,246,0.08) 0%, transparent 70%); pointer-events:none;"></div>
          <div class="text-2xl mb-4">🎯</div>
          <h3 class="text-xl font-bold text-white mb-3" style="font-family:'Space Grotesk',system-ui,sans-serif; letter-spacing:-0.02em;">Agentes de Generación de Leads</h3>
          <p class="section-sub">Scraping automatizado de LinkedIn y Google Maps para encontrar prospectos calificados. El agente los contacta, los calienta y los entrega listos para venta.</p>
          <div class="mt-4 flex gap-2">
            <span class="text-xs px-3 py-1 rounded-full" style="background:rgba(139,92,246,0.12); color:#C4B5FD; border:1px solid rgba(139,92,246,0.2);">LinkedIn</span>
            <span class="text-xs px-3 py-1 rounded-full" style="background:rgba(139,92,246,0.12); color:#C4B5FD; border:1px solid rgba(139,92,246,0.2);">Google Maps</span>
            <span class="text-xs px-3 py-1 rounded-full" style="background:rgba(139,92,246,0.12); color:#C4B5FD; border:1px solid rgba(139,92,246,0.2);">Outreach</span>
          </div>
        </div>
        <!-- Small card 1 -->
        <div class="card p-6" data-animate data-delay="3">
          <div class="text-xl mb-3">⚙️</div>
          <h3 class="text-lg font-bold text-white mb-2" style="font-family:'Space Grotesk',system-ui,sans-serif; letter-spacing:-0.02em;">Automatización Interna</h3>
          <p class="section-sub text-sm">Elimina tareas repetitivas del equipo: facturas, reportes, notificaciones, sincronización entre herramientas.</p>
        </div>
        <!-- Small card 2 -->
        <div class="card p-6" data-animate data-delay="4">
          <div class="text-xl mb-3">📊</div>
          <h3 class="text-lg font-bold text-white mb-2" style="font-family:'Space Grotesk',system-ui,sans-serif; letter-spacing:-0.02em;">CRM y Seguimiento Automático</h3>
          <p class="section-sub text-sm">Ningún lead se enfría por falta de seguimiento. El sistema califica, recuerda y convierte en piloto automático.</p>
        </div>
      </div>
    </div>
  </section>

  <!-- SECTIONS WILL BE ADDED HERE -->
```

- [ ] **Step 2: Screenshot and verify**

```bash
node screenshot.mjs http://localhost:3000 services
```
Check: 2 wide cards on top row, 2 small cards on bottom row, badge chips, radial glow accents inside cards.

---

## Task 9: Tech Stack Section

**Files:**
- Modify: `index.html` — replace `<!-- SECTIONS WILL BE ADDED HERE -->`

- [ ] **Step 1: Add Tech Stack HTML:**

```html
  <!-- TECH STACK -->
  <section class="py-20 px-6" style="border-top:1px solid rgba(255,255,255,0.05); border-bottom:1px solid rgba(255,255,255,0.05);">
    <div class="max-w-6xl mx-auto">
      <div class="text-center mb-12" data-animate>
        <div class="section-label mb-3">Infraestructura</div>
        <p class="section-sub">Infraestructura real en VPS — no herramientas básicas de arrastrar y soltar.</p>
      </div>
      <div class="flex flex-wrap justify-center items-center gap-8 md:gap-12" data-animate>
        <!-- n8n -->
        <div class="tech-item flex flex-col items-center gap-2">
          <div class="w-12 h-12 rounded-xl flex items-center justify-center font-bold text-lg"
               style="background:rgba(255,102,51,0.12); border:1px solid rgba(255,102,51,0.2); color:#FF6633; font-family:'Space Grotesk',system-ui,sans-serif;">n</div>
          <span class="text-xs font-medium" style="color:#6B7280;">n8n</span>
        </div>
        <!-- GoHighLevel -->
        <div class="tech-item flex flex-col items-center gap-2">
          <div class="w-12 h-12 rounded-xl flex items-center justify-center font-bold text-sm"
               style="background:rgba(0,136,255,0.12); border:1px solid rgba(0,136,255,0.2); color:#0088FF; font-family:'Space Grotesk',system-ui,sans-serif;">GHL</div>
          <span class="text-xs font-medium" style="color:#6B7280;">GoHighLevel</span>
        </div>
        <!-- Supabase -->
        <div class="tech-item flex flex-col items-center gap-2">
          <div class="w-12 h-12 rounded-xl flex items-center justify-center font-bold text-lg"
               style="background:rgba(62,207,142,0.12); border:1px solid rgba(62,207,142,0.2); color:#3ECF8E; font-family:'Space Grotesk',system-ui,sans-serif;">S</div>
          <span class="text-xs font-medium" style="color:#6B7280;">Supabase</span>
        </div>
        <!-- DigitalOcean -->
        <div class="tech-item flex flex-col items-center gap-2">
          <div class="w-12 h-12 rounded-xl flex items-center justify-center font-bold text-lg"
               style="background:rgba(0,128,255,0.12); border:1px solid rgba(0,128,255,0.2); color:#0080FF; font-family:'Space Grotesk',system-ui,sans-serif;">
            <svg width="22" height="22" viewBox="0 0 24 24" fill="#0080FF"><path d="M12 0C5.373 0 0 5.373 0 12s5.373 12 12 12 12-5.373 12-12S18.627 0 12 0zm0 19.5v-3.375A4.127 4.127 0 0 1 7.875 12H4.5A7.5 7.5 0 0 0 12 19.5zm3.375-3.375H12V12.75h3.375v3.375zm3.375-3.375H15.75V9.375h3v3.375zM12 4.5A7.5 7.5 0 0 1 19.5 12h-3.375A4.127 4.127 0 0 0 12 7.875V4.5z"/></svg>
          </div>
          <span class="text-xs font-medium" style="color:#6B7280;">DigitalOcean</span>
        </div>
        <!-- Hostinger -->
        <div class="tech-item flex flex-col items-center gap-2">
          <div class="w-12 h-12 rounded-xl flex items-center justify-center font-bold text-lg"
               style="background:rgba(103,61,230,0.12); border:1px solid rgba(103,61,230,0.2); color:#673DE6; font-family:'Space Grotesk',system-ui,sans-serif;">H</div>
          <span class="text-xs font-medium" style="color:#6B7280;">Hostinger</span>
        </div>
        <!-- CrewAI -->
        <div class="tech-item flex flex-col items-center gap-2">
          <div class="w-12 h-12 rounded-xl flex items-center justify-center font-bold text-sm"
               style="background:rgba(255,255,255,0.05); border:1px solid rgba(255,255,255,0.1); color:#F0F0F5; font-family:'Space Grotesk',system-ui,sans-serif;">C</div>
          <span class="text-xs font-medium" style="color:#6B7280;">CrewAI</span>
        </div>
      </div>
    </div>
  </section>

  <!-- SECTIONS WILL BE ADDED HERE -->
```

- [ ] **Step 2: Screenshot and verify**

```bash
node screenshot.mjs http://localhost:3000 techstack
```
Check: 6 tech logos in a horizontal row, each with colored icon + name below.

---

## Task 10: About Luis Section

**Files:**
- Modify: `index.html` — replace `<!-- SECTIONS WILL BE ADDED HERE -->`

- [ ] **Step 1: Add About HTML:**

```html
  <!-- ABOUT -->
  <section class="py-24 px-6">
    <div class="max-w-6xl mx-auto">
      <div class="grid md:grid-cols-2 gap-12 items-center">
        <!-- Photo -->
        <div data-animate>
          <div class="photo-wrap" style="max-width:420px; height:520px; border:1px solid rgba(46,123,246,0.2); box-shadow: 0 0 60px rgba(46,123,246,0.08);">
            <img src="/Photo of my self.jpg" alt="Luis Moreno — Automatización para Negocios" loading="lazy">
            <div class="photo-blue-layer"></div>
          </div>
        </div>
        <!-- Text -->
        <div data-animate data-delay="1">
          <div class="section-label mb-4">Quién está detrás del sistema</div>
          <h2 class="section-heading text-4xl mb-6" style="font-size:clamp(1.8rem,4vw,2.8rem);">
            Luis Moreno
          </h2>
          <div class="section-sub space-y-4" style="line-height:1.7;">
            <p>Soy un ingeniero de automatización especializado en construir sistemas de IA que reemplazan trabajo manual en negocios de 5 a 50 personas.</p>
            <p>No vendo herramientas — construyo infraestructura real. Mis sistemas corren en servidores VPS propios, con lógica de negocio diseñada para cada cliente, no plantillas genéricas.</p>
            <p>Trabajo con n8n, GoHighLevel, Supabase y CrewAI para crear flujos que tus competidores tardarán años en alcanzar.</p>
            <p style="color:#F0F0F5;">Si tu negocio depende de que tú estés presente para funcionar, eso tiene solución. Y se llama automatización.</p>
          </div>
          <div class="mt-8">
            <a href="https://calendly.com/YOUR_LINK" target="_blank" rel="noopener" class="btn-primary">
              Hablar con Luis →
            </a>
          </div>
        </div>
      </div>
    </div>
  </section>

  <!-- SECTIONS WILL BE ADDED HERE -->
```

- [ ] **Step 2: Screenshot and verify**

```bash
node screenshot.mjs http://localhost:3000 about
```
Check: Photo on left with blue tint/overlay, text on right, photo fills its container cleanly.

---

## Task 11: Guarantee Section

**Files:**
- Modify: `index.html` — replace `<!-- SECTIONS WILL BE ADDED HERE -->`

- [ ] **Step 1: Add Guarantee HTML:**

```html
  <!-- GUARANTEE -->
  <section class="py-24 px-6" style="background: linear-gradient(to bottom, #060609, #07070f, #060609);">
    <div class="max-w-4xl mx-auto text-center" data-animate>
      <div class="guarantee-card p-12 md:p-16">
        <div class="text-5xl mb-6">🛡</div>
        <div class="section-label mb-4">Garantía absoluta</div>
        <h2 class="section-heading text-3xl md:text-4xl mb-6" style="font-size:clamp(1.8rem,4vw,2.5rem);">
          Garantía de Devolución del 100%
        </h2>
        <p class="text-lg mb-4" style="color:#D1D5DB; line-height:1.7; max-width:540px; margin:0 auto 1.5rem;">
          Si implemento el sistema y no ves los resultados prometidos, te devuelvo cada centavo.
        </p>
        <p class="text-xl font-semibold mb-8" style="color:#F0F0F5; font-family:'Space Grotesk',system-ui,sans-serif;">
          Y te quedas con toda la infraestructura instalada.
        </p>
        <p class="text-sm mb-10" style="color:#6B7280;">Sin letras pequeñas. Sin asteriscos. Sin excusas.</p>
        <a href="https://calendly.com/YOUR_LINK" target="_blank" rel="noopener" class="btn-primary">
          Agendar sin riesgo →
        </a>
      </div>
    </div>
  </section>

  <!-- SECTIONS WILL BE ADDED HERE -->
```

- [ ] **Step 2: Screenshot and verify**

```bash
node screenshot.mjs http://localhost:3000 guarantee
```
Check: Glowing blue-bordered card, shield emoji, centered text, no visual clutter.

---

## Task 12: Instagram Window

**Files:**
- Modify: `index.html` — replace `<!-- SECTIONS WILL BE ADDED HERE -->`

- [ ] **Step 1: Add Instagram HTML:**

```html
  <!-- INSTAGRAM -->
  <section class="py-24 px-6">
    <div class="max-w-4xl mx-auto text-center" data-animate>
      <div class="section-label mb-4">En tiempo real</div>
      <h2 class="section-heading text-3xl md:text-4xl mb-4" style="font-size:clamp(1.8rem,4vw,2.5rem);">
        Sígueme para ver el trabajo en vivo
      </h2>
      <p class="section-sub text-lg mb-10 max-w-lg mx-auto">
        Comparto casos reales, implementaciones y resultados de clientes en Instagram.
      </p>
      <a href="https://instagram.com/YOUR_HANDLE" target="_blank" rel="noopener" class="instagram-card block p-10 max-w-sm mx-auto" style="text-decoration:none;">
        <div class="w-16 h-16 rounded-2xl flex items-center justify-center mx-auto mb-5"
             style="background: linear-gradient(135deg, #f09433 0%, #e6683c 25%, #dc2743 50%, #cc2366 75%, #bc1888 100%);">
          <svg width="28" height="28" viewBox="0 0 24 24" fill="white">
            <path d="M12 2.163c3.204 0 3.584.012 4.85.07 3.252.148 4.771 1.691 4.919 4.919.058 1.265.069 1.645.069 4.849 0 3.205-.012 3.584-.069 4.849-.149 3.225-1.664 4.771-4.919 4.919-1.266.058-1.644.07-4.85.07-3.204 0-3.584-.012-4.849-.07-3.26-.149-4.771-1.699-4.919-4.92-.058-1.265-.07-1.644-.07-4.849 0-3.204.013-3.583.07-4.849.149-3.227 1.664-4.771 4.919-4.919 1.266-.057 1.645-.069 4.849-.069zM12 0C8.741 0 8.333.014 7.053.072 2.695.272.273 2.69.073 7.052.014 8.333 0 8.741 0 12c0 3.259.014 3.668.072 4.948.2 4.358 2.618 6.78 6.98 6.98C8.333 23.986 8.741 24 12 24c3.259 0 3.668-.014 4.948-.072 4.354-.2 6.782-2.618 6.979-6.98.059-1.28.073-1.689.073-4.948 0-3.259-.014-3.667-.072-4.947-.196-4.354-2.617-6.78-6.979-6.98C15.668.014 15.259 0 12 0zm0 5.838a6.162 6.162 0 1 0 0 12.324 6.162 6.162 0 0 0 0-12.324zM12 16a4 4 0 1 1 0-8 4 4 0 0 1 0 8zm6.406-11.845a1.44 1.44 0 1 0 0 2.881 1.44 1.44 0 0 0 0-2.881z"/>
          </svg>
        </div>
        <div class="text-white font-semibold text-lg mb-1" style="font-family:'Space Grotesk',system-ui,sans-serif;">@YOUR_HANDLE</div>
        <div class="text-sm mb-5" style="color:#6B7280;">Ver perfil en Instagram →</div>
        <div class="inline-flex items-center gap-2 px-5 py-2.5 rounded-lg text-sm font-medium text-white"
             style="background: linear-gradient(135deg, #f09433, #dc2743, #bc1888);">
          Seguir →
        </div>
      </a>
    </div>
  </section>

  <!-- SECTIONS WILL BE ADDED HERE -->
```

- [ ] **Step 2: Screenshot and verify**

```bash
node screenshot.mjs http://localhost:3000 instagram
```
Check: Instagram card with gradient icon, handle placeholder, gradient button.

---

## Task 13: Final CTA + Footer

**Files:**
- Modify: `index.html` — replace `<!-- SECTIONS WILL BE ADDED HERE -->`

- [ ] **Step 1: Add Final CTA and Footer — this is the LAST section, replace the comment entirely:**

```html
  <!-- FINAL CTA -->
  <section class="py-32 px-6 relative overflow-hidden" style="background: linear-gradient(to bottom, #060609, #08081a, #060609);">
    <div style="position:absolute; inset:0; background:radial-gradient(ellipse 1000px 600px at 50% 50%, rgba(46,123,246,0.09) 0%, transparent 70%); pointer-events:none;"></div>
    <div class="max-w-3xl mx-auto text-center relative z-10" data-animate>
      <div class="section-label mb-6">Cero riesgo</div>
      <h2 class="section-heading text-4xl md:text-6xl mb-6" style="font-size:clamp(2.2rem,6vw,4rem);">
        ¿Listo para recuperar<br>tu tiempo?
      </h2>
      <p class="section-sub text-lg mb-4 max-w-xl mx-auto">
        20 minutos de auditoría gratuita. Sin compromisos. Sin presión de ventas.
      </p>
      <p class="mb-10 font-medium" style="color:#7DAAFF; font-family:'Space Grotesk',system-ui,sans-serif;">
        Si no veo cómo ayudarte, te lo digo directo.
      </p>
      <a href="https://calendly.com/YOUR_LINK" target="_blank" rel="noopener" class="btn-primary" style="font-size:1.0625rem; padding:1rem 2rem;">
        Agendar Auditoría Gratuita →
      </a>
    </div>
  </section>

  <!-- FOOTER -->
  <footer class="py-8 px-6" style="border-top:1px solid rgba(255,255,255,0.06);">
    <div class="max-w-6xl mx-auto flex flex-col md:flex-row items-center justify-between gap-4">
      <div class="font-semibold text-white" style="font-family:'Space Grotesk',system-ui,sans-serif;">Luis Moreno</div>
      <div class="text-sm" style="color:#6B7280;">© 2026 Luis Moreno. Todos los derechos reservados.</div>
      <div class="flex gap-5">
        <a href="https://instagram.com/YOUR_HANDLE" target="_blank" rel="noopener"
           class="text-sm transition-colors duration-200 hover:text-white" style="color:#6B7280; text-decoration:none;">Instagram</a>
        <a href="https://calendly.com/YOUR_LINK" target="_blank" rel="noopener"
           class="text-sm transition-colors duration-200 hover:text-white" style="color:#6B7280; text-decoration:none;">Agendar Llamada</a>
      </div>
    </div>
  </footer>
```

- [ ] **Step 2: Screenshot and verify**

```bash
node screenshot.mjs http://localhost:3000 cta-footer
```
Check: Large centered headline, single CTA button, minimal footer below.

---

## Task 14: JavaScript — Animations, Counter, Navbar Scroll

**Files:**
- Modify: `index.html` — replace `// JS WILL BE ADDED HERE` inside the `<script>` tag

- [ ] **Step 1: Add all JavaScript — replace the JS comment with:**

```javascript
    // --- Scroll animations ---
    const observer = new IntersectionObserver((entries) => {
      entries.forEach(e => { if (e.isIntersecting) { e.target.classList.add('in'); observer.unobserve(e.target); } });
    }, { threshold: 0.12 });
    document.querySelectorAll('[data-animate]').forEach(el => observer.observe(el));

    // --- Navbar scroll effect ---
    const nav = document.getElementById('navbar');
    window.addEventListener('scroll', () => {
      nav.classList.toggle('scrolled', window.scrollY > 40);
    }, { passive: true });

    // --- Counter animation ---
    function animateCount(el, target, duration, suffix = '') {
      let start = null;
      const step = (ts) => {
        if (!start) start = ts;
        const progress = Math.min((ts - start) / duration, 1);
        const eased = 1 - Math.pow(1 - progress, 3); // ease-out cubic
        el.textContent = Math.floor(eased * target) + suffix;
        if (progress < 1) requestAnimationFrame(step);
      };
      requestAnimationFrame(step);
    }

    const counterObserver = new IntersectionObserver((entries) => {
      entries.forEach(e => {
        if (!e.isIntersecting) return;
        const id = e.target.id;
        if (id === 'counter-hours') animateCount(e.target, 10, 1800);
        if (id === 'counter-hours-lost') animateCount(e.target, 23, 2000);
        if (id === 'counter-pct') animateCount(e.target, 78, 2000);
        if (id === 'counter-cost') animateCount(e.target, 4200, 2200);
        counterObserver.unobserve(e.target);
      });
    }, { threshold: 0.5 });

    ['counter-hours','counter-hours-lost','counter-pct','counter-cost'].forEach(id => {
      const el = document.getElementById(id);
      if (el) counterObserver.observe(el);
    });
```

- [ ] **Step 2: Screenshot to verify animations initialized (static check)**

```bash
node screenshot.mjs http://localhost:3000 js-check
```
Read screenshot. Since Puppeteer waits for `networkidle0`, scroll animations won't have fired yet (elements start at opacity 0). The hero section IS in the viewport, so it should be visible. Check: hero content visible, navbar present.

---

## Task 15: Full-Page Screenshot Round 1 — Review and Fix

- [ ] **Step 1: Take full-page screenshot at 1440px**

```bash
node screenshot.mjs http://localhost:3000 review-1
```

- [ ] **Step 2: Read the screenshot with the Read tool and audit every section**

Check each section in order:
- Navbar: wordmark + button positioned correctly, transparent bg
- Hero: headline large and bold, blue accent color on "no al revés.", stat row visible
- Problem: 3 cards equal width, blue numbers, surface card color visible
- Methodology: 3 steps with numbered circles, connector line between
- Promise: 2×2 grid, emoji + bold metric + description
- Services: 2 wide + 2 narrow bento layout
- Tech Stack: 6 logos in a row, colored borders
- About: photo left (with blue overlay), text right
- Guarantee: glowing card, shield emoji
- Instagram: gradient card centered
- Final CTA: large headline, big button
- Footer: minimal, 3-column

- [ ] **Step 3: Fix all visible issues**

For each issue found, edit `index.html` to correct it. Common issues to watch for:
- Font not loaded (check Google Fonts CDN loads over network)
- Photo not showing (verify path is `/Photo of my self.jpg`)
- Bento grid collapsed to 1 column at 1440px (check CSS)
- Counter values showing 0 (expected — counters animate on scroll, not on load)
- Colors not matching spec (check hex values against: `#2E7BF6`, `#060609`, `#0d0d14`, `#F0F0F5`, `#6B7280`)

---

## Task 16: Screenshot Round 2 — Final Polish

- [ ] **Step 1: Take second full-page screenshot**

```bash
node screenshot.mjs http://localhost:3000 review-2
```

- [ ] **Step 2: Read and do a final pixel-level audit**

Focus on:
- Spacing consistency: sections should have 96px (`py-24`) vertical padding
- Typography: headings use Space Grotesk, body uses Inter — verify font rendering
- Card borders: `rgba(255,255,255,0.07)` — subtle but present
- Blue accent: exactly `#2E7BF6` — not Tailwind default blue-600 (`#2563EB`)
- Shadows: layered and colored, not flat
- No section breaks/gaps that look unintentional
- Mobile: take a second screenshot at 390px viewport if needed

- [ ] **Step 3: Apply final fixes and confirm done**

Make all remaining adjustments. When no visible differences remain from the design spec, the site is complete.

---

## Post-Build Checklist

- [ ] Swap `https://calendly.com/YOUR_LINK` with real Calendly URL (4 occurrences)
- [ ] Swap `https://instagram.com/YOUR_HANDLE` with real Instagram handle (3 occurrences)
- [ ] Swap `@YOUR_HANDLE` text with real handle (1 occurrence)
- [ ] Test on mobile viewport (390px) — take screenshot
- [ ] Deploy `index.html` + `Photo of my self.jpg` to Hostinger or DigitalOcean
