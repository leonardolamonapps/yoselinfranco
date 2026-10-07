# Landing Page — Yoselin Franco · Coach Personal y Mentora Financiera

**Especificación técnica de replicación**

> **Propósito de este documento:** permitir que cualquier agente de IA o desarrollador **replique `index.html` exactamente**, con el mismo diseño, contenido, idiomas y comportamiento. Todo dato marcado como *verbatim* debe copiarse carácter por carácter.

| Dato | Valor |
|---|---|
| **Archivo fuente único** | `index.html` (HTML5 + CSS3 + JS vanilla, un solo archivo, ~115 KB) |
| **Dominio** | yoselinfranco.com |
| **Idiomas** | Español (ES) · Inglés (EN) · Francés (FR) — selector en la navegación |
| **Tagline principal** | "Nunca es tarde para reinventarte." |
| **Asset de imagen** | `Image.png` (foto en sección 03) — única imagen del sitio |
| **Dependencias externas** | Solo Google Fonts (CDN). Sin frameworks, sin build, sin npm. |

---

## 1. Stack, arquitectura y orden del archivo

- **Lenguajes:** HTML5, CSS3 (variables, grid, clamp, backdrop-filter), JavaScript ES6+ sin dependencias.
- **Sin frameworks:** ni React, ni Tailwind, ni Bootstrap. Todo CSS vive en un `<style>` en el `<head>`; todo JS en un `<script>` al final del `<body>`.
- **Página única (one-pager)** con anclajes `#hero`, `#about`, `#services`, `#courses`, `#testimonials`, `#contact`.

**Orden exacto de bloques dentro de `index.html`:**

1. `<!DOCTYPE html>` → `<html lang="es">` → `<head>`: charset UTF-8, viewport, `<title>`, `<meta name="description">`, preconnects + Google Fonts, `<style>` (todo el CSS).
2. `<body>`: `div#cursor.custom-cursor` → Splash `#splash` → `nav#nav` → `header#hero` → `section#intro` → `.marquee-wrap` → `section#value` (01) → `section#services` (02) → `section#about` (03) → `section#courses` (04) → `section#testimonials` (05) → `section#contact` (06) → `footer` → modal `#talleresModal` → `<script>`.

**Meta head verbatim:**

```html
<title>Yoselin Franco | Coach Personal y Mentora Financiera</title>
<meta name="description" content="Acompaño a personas en transición a reinventarse personal y financieramente. Mentora en reinvención personal y financiera para migrantes y personas que empiezan de nuevo.">
```

No hay favicon ni etiquetas Open Graph (limitación conocida).

---

## 2. Paleta de colores

### 2.1 Tokens principales (`:root`)

| Variable | Hex | Uso |
|---|---|---|
| `--off-white` | `#E6D9CF` | Fondo general claro (nude), secciones luz, modal |
| `--black` | `#4A3728` | Texto principal, fondo de secciones oscuras, splash, footer |
| `--accent` | `#DD675D` | Coral: CTAs, precios, kickers, decoraciones, links |
| `--gold` | `#DFB65B` | Dorado: hover de filas de tabla (con opacidad) |
| `--white` | `#ffffff` | Tarjetas sobre fondo claro, texto sobre oscuro |
| `--mid` | `#CAB19F` | Nude medio (secundario) |
| `--grey-brown` | `#7A6255` | Texto secundario sobre claro (modal, subtítulos) |
| `--border-light` | `rgba(74,55,40,0.14)` | Bordes sobre fondo claro |
| `--border-dark` | `rgba(255,255,255,0.14)` | Bordes sobre fondo oscuro |

### 2.2 Colores derivados (usados directamente en CSS, no en variables)

| Color | Uso |
|---|---|
| `#e58278` | Hover claro de botones/acentos coral |
| `#553f2e` | Hover de tarjetas (`service-card`, `course-card`) |
| `rgba(221,103,93,0.92)` | Indicador de nav activo, botón de idioma activo |
| `rgba(221,103,93,0.4)` / `0.35` / `0.08` | Bordes y fondos de badges/fase coral translúcidos |
| `#3d2d21` → `#2b1f16` | Degradado del hero: `linear-gradient(160deg, var(--black) 0%, #3d2d21 55%, #2b1f16 100%)` |
| `rgba(17,17,17,0.62 / 0.12)` | Viñeta superior/inferior del hero |
| `rgba(17,17,17,0.55)` y `rgba(17,17,17,0.97)` | Fondo de nav (con blur) y menú móvil |
| `rgba(232,64,32,0.7 / 0.9 / 0.18)` | Glow del cursor personalizado (rojo distinto al accent) |
| `rgba(223,182,91,0.10)` | Hover de filas de la tabla del modal (gold translúcido) |
| `#22c55e` | Punto verde "disponible" (`live-dot`) |
| Texto oscuro secundario | `#666`, `#777`, `#999`, `#aaa` |
| Texto claro secundario | `rgba(255,255,255,0.35 / 0.4 / 0.45 / 0.5 / 0.6 / 0.7 / 0.75)` |

---

## 3. Tipografía

**Carga verbatim (Google Fonts):**

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Dancing+Script:wght@600;700&family=Playfair+Display:ital,wght@0,700;0,900;1,700&family=Space+Grotesk:wght@300;400;500;600;700&family=DM+Mono:wght@400;500;700&display=swap" rel="stylesheet">
```

> **Nota:** `Dancing Script` y `Playfair Display` se cargan pero **no se usan en ningún CSS** (carga residual). Las únicas familias aplicadas son:

| Variable | Familia | Rol |
|---|---|---|
| `--font` | `Space Grotesk, sans-serif` | Todo el texto (body, títulos, botones) |
| `--mono` | `DM Mono, monospace` | Kickers, fechas, badges, tabla, marquee, stats, códigos |

**Escala tipográfica (donde no usa `rem`):**

| Elemento | Tamaño |
|---|---|
| H1 hero `.hero-name` | `clamp(40px, 11.5vw, 200px)`, weight 700, `letter-spacing: -0.04em`, `line-height: 0.82`, `white-space: nowrap` |
| Ghost number `.ns-ghost-num` | `clamp(80px, 14vw, 180px)`, transparente con `-webkit-text-stroke: 2px` |
| H2 secciones `.ns-h2` | `clamp(28px, 4vw, 52px)`, weight 700, `-0.04em` |
| Statement intro `.intro-statement` | `clamp(30px, 3.6vw, 54px)`, weight 600 |
| H2 about `.about-h2` | `clamp(28px, 3.5vw, 48px)` |
| Lista `.h-item-name` | `clamp(16px, 1.8vw, 22px)`, weight 600 |
| Kicker `.sec-label` | 12px, uppercase, weight 600, `0.08em`, color accent, **prefijo `::before { content: '// '; }`** |
| Body/genérico | 13–16px, `line-height` 1.7–1.82 |
| Mono etiquetas | 10–12px, uppercase, `letter-spacing` 0.06–0.18em |
| Precio tarjetas | `2rem`/`2.2rem` (cursos/servicios), accent, weight 700 |
| Título tarjeta | `1.4rem`/`1.5rem`, weight 700, `-0.03em` |

---

## 4. Variables CSS (`:root`) — verbatim

```css
:root {
  --off-white: #E6D9CF;
  --black: #4A3728;
  --accent: #DD675D;
  --gold: #DFB65B;
  --white: #ffffff;
  --mid: #CAB19F;
  --grey-brown: #7A6255;
  --border-light: rgba(74,55,40,0.14);
  --border-dark: rgba(255,255,255,0.14);
  --font: 'Space Grotesk', sans-serif;
  --mono: 'DM Mono', monospace;
}
```

**Reset base verbatim:**

```css
*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
html { scroll-behavior: smooth; overflow-x: hidden; }
body { font-family: var(--font); background: var(--off-white); color: var(--black); overflow-x: hidden; -webkit-font-smoothing: antialiased; }
a { text-decoration: none; color: inherit; }
img, video { display: block; max-width: 100%; }
```

---

## 5. Convenciones de diseño globales

| Convención | Regla |
|---|---|
| **Contenedor** | `max-width: 1200px; margin: 0 auto` (`.ns-body`, `.intro-inner`, `.quotes`, `.footer-grid`, `.copyright`, headers) |
| **Padding de sección** | `.numbered-section { padding: 80px 40px 100px; }`; `#intro { 120px 40px }`; `#about`/`.testimonial-bg`/`#contact` `100px 40px` (contacto `+120px` inferior) |
| **Header de sección** | `.ns-header`: borde superior 1px + `padding-top: 24px`, flex con número fantasma a la izquierda y bloque de título (`padding-left: 48px`), `margin-bottom: 64px` |
| **Números fantasma** | `01`–`06`, texto transparente con stroke 2px: `rgba(255,255,255,0.30)` en oscuro, `rgba(74,55,40,0.40)` en claro |
| **Kicker** | `.sec-label` siempre con prefijo `// ` en coral |
| **Palabra decorativa** | `<span class="deco">` o `<em>` dentro de títulos → color `--accent` |
| **Reveal** | `.reveal` inicia `opacity:0; translateY(28px)`, transición `0.7s cubic-bezier(0.16,1,0.3,1)`; retardos `.d1`–`.d5` = 80 ms escalonados; se activan con IntersectionObserver |
| **Grillas con separación de 1px** | `display:grid; gap:1px; background: var(--border-dark); border: 1px solid var(--border-dark);` con tarjetas de fondo sólido (efecto hairline) |
| **Tarjetas oscuras** | fondo `#4A3728`, hover `#553f2e`, sin border-radius (esquinas rectas) |
| **Tarjetas claras** | fondo `#fff`, borde `--border-light`, hover borde accent + `translateY(-4px)` + `box-shadow: 0 20px 50px rgba(0,0,0,0.06)` |
| **Botones (`.btn`)** | `padding: 13px 26px; border-radius: 999px; font-size: 13px; font-weight: 700; letter-spacing: 0.04em` |
| **`.btn.dark`** | fondo accent, texto blanco, hover `#e58278` + `translateY(-2px)` |
| **`.btn.line` / `.btn-line`** | borde `rgba(255,255,255,0.3)`, texto `rgba(255,255,255,0.8)`, hover blanco |
| **Badges** | mono 10px uppercase, `letter-spacing: 0.1em`, borde 1px, `padding: 4px 12px`; variante `.accent`/`.gratis` en coral |
| **Bullets de listas** | `li::before { content: '→' }` en coral (tarjetas) o `'✓'` (política) o `'›'` (contacto, como `<span class="ico">`) |
| **Radios** | pills/botones/nav `999px`; modal `18px`; menú móvil `20px`; el resto `0` |
| **Curva de animación estándar** | `cubic-bezier(0.16, 1, 0.3, 1)` |

---

## 6. Comportamiento JavaScript (un solo `<script>`)

### 6.1 Sistema i18n
- Diccionario `const translations = { es: {...}, en: {...}, fr: {...} }` (**205 claves por idioma, claves idénticas en los tres**).
- Todo el texto traducible lleva `data-i18n="clave"`; `applyLang(lang)` hace `el.innerHTML = translations[lang][key]` (por eso las claves pueden contener HTML: `<span class="deco">`, `<strong>`, `<em>`, `<a>`).
- `applyLang` también actualiza `document.documentElement.lang` y `document.title` (`meta_title`).
- Selector: botones `.lang-btn[data-lang]`; persistencia en `localStorage['yoselin-lang']` (default `es`); se aplica al cargar (`applyLang(savedLang)`).
- **Excepciones (no traducible):** los textos de testimonios (reseñas textuales, siempre en español), los botones "Ver más"/"Ver menos" (hardcodeados en ES) y "Scroll ↓".
- Claves huérfanas/legadas existentes sin uso en HTML: `serv_t1`, `serv_d1`, `serv1_*`, `serv_t6`, `serv_d6`, `serv6_*`, `serv_badge_free`, `serv_badge_phase`, `phase2`, `btn_reserve`, `ctc1_*`, `c2_btn2`.

### 6.2 Splash (pantalla de carga)
- Fondo `#4A3728` a pantalla completa (z-index 9999): kicker `// Coach Personal y Mentora Financiera` (mono, accent), nombre "Yoselin **Franco**" (`clamp(36px, 9vw, 80px)`, "Franco" en accent) y barra de 260px×2px.
- JS: incrementa el ancho aleatoriamente cada 150 ms (`+10 a +26%`); al 100% espera 300 ms y oculta con fade 0.6 s; **máximo 4.5 s**. Al ocultarse agrega `body.is-loaded` (dispara animaciones de entrada del hero) y `cursor.is-ready`.

### 6.3 Cursor personalizado
- Círculo de 24 px, borde 2px accent, glow `rgba(232,64,32,0.7)`, `z-index: 9999`, `pointer-events:none`.
- Sigue al mouse con lerp `0.22` vía `requestAnimationFrame` (vars `--cx/--cy`); sobre `a, button, [data-cursor-hover]` escala a 1.8 con fondo coral translúcido.
- Oculto por CSS/JS en dispositivos táctiles (`pointer: coarse` / sin hover); el cursor nativo se anula con `cursor: none` solo en `@media (hover:hover) and (pointer:fine)`.

### 6.4 Navegación
- **Ocultar al bajar:** si `scrollY > lastScroll && scrollY > 160` → clase `is-hidden` (opacity 0 + translateY(-16px)).
- **Indicador activo:** píldora coral (`nav-indicator`) que se anima (`left/width` 0.45 s) bajo el link de la sección visible; usa `sections = ['hero','about','services','courses','testimonials','contact']` y considera activa la cuya `top <= 40%` del viewport; deshabilitado `≤980px`.
- **Menú móvil:** `☰` alterna `.open` en `.nav-pill` (dropdown vertical, fondo `rgba(17,17,17,0.97)`, radio 20px).

### 6.5 Reveal on scroll
- `IntersectionObserver` con `threshold: 0.12`, agrega `.in` y se desuscribe (una sola vez).

### 6.6 Modal de talleres
- Abre con `[data-open-talleres]` (tarjeta "Talleres en Vivo"): agrega `.open` al overlay, `aria-hidden="false"` y `body.style.overflow = hidden`.
- Cierra con: botón ✕, clic en el overlay (`e.target === modal`) o tecla `Escape`.

### 6.6 Testimonios (toggle)
- `.quote-toggle` alterna la clase `.expanded` en `.quote-text` (rompe el `-webkit-line-clamp: 4`) y cambia el texto del botón a "Ver menos"/"Ver más" (hardcoded ES).

### 6.7 Misceláneos
- `#year` rellena el año actual en el copyright.
- Animación `livePulse` infinita en el punto verde de disponibilidad.
- Marquee: `translateX(0 → -50%)` en 26 s lineales infinitos (contenido duplicado ×2 para loop perfecto).

---

## 7. Responsive (breakpoints exactos)

| Breakpoint | Efectos |
|---|---|
| **≤1280px** | `.services-grid` → 2 columnas |
| **≤980px** | `intro-inner`, `about-grid`, `contact-grid`, `quotes` → 1 columna; `services-grid`, `courses-grid` → 1 columna; aparece `.menu-toggle` ☰; `.nav-pill` pasa a dropdown vertical oculto (`.open` lo muestra); se oculta `.nav-indicator`; `.ns-header` en wrap; `.hero-social` a `left:24px` |
| **≤700px** | Se oculta el `.nav-cta` ("Agenda tu sesión") |
| **≤640px** | `.intro-stats` vertical y `.stat-pipe` ocultos; `footer-grid` 1 columna; `policy ul` 1 columna; `.hero-social` oculto; `ns-ghost-num` 64px; botones de tarjetas a 100% de ancho; modal `padding: 26px 18px` y tabla con `min-width: 700px` (scroll horizontal interno) |
| **≤480px** | Paddings reducidos a 20px; `ns-h2` 30px; `ns-desc` 14px; tarjetas con padding 26px 22px; `intro-statement` 30px; ajustes finos de hero/lang buttons |

---

## 8. Detalle por sección (orden del DOM)

### 8.0 Splash
Ver §6.2.

### 8.1 Navegación (`nav#nav`)
- **Pill flotante fija:** `position: fixed; top: 22px; left: 50%; transform: translateX(-50%)`, fondo `rgba(17,17,17,0.55)` + `backdrop-filter: blur(20px) saturate(140%)`, borde 1px blanco translúcido, `border-radius: 999px`, `z-index: 100`.
- **Logo:** "Yoselin" + punto coral (`.nav-dot`), con borde derecho separador → enlaza a `#hero`.
- **Links:** Inicio · Quién Soy · Servicios · Cursos · Testimonios (`data-i18n: nav_home, nav_about, nav_services, nav_courses, nav_testimonials`), 12.5px, `rgba(255,255,255,0.6)` → blanco en hover/activo.
- **Selector:** botones `ES | EN | FR` (mono 10px uppercase; activo con fondo coral).
- **CTA:** "Agenda tu sesión" → `https://calendly.com/hola-yoselinfranco/new-meeting-1` (nueva pestaña), fondo coral, mono 10.5px uppercase.
- **Hamburguesa:** botón `☰` (solo ≤980px), `aria-label="Menú"`.

### 8.2 Hero (`header#hero`)
- `min-height: 100dvh`, fondo oscuro, `justify-content: flex-end`.
- **Fondo:** *no hay foto*; `.hero-photo-wrap` es un degradado `linear-gradient(160deg, #4A3728 0%, #3d2d21 55%, #2b1f16 100%)` + `.hero-vignette` (`linear-gradient(to top, rgba(17,17,17,0.62) 0%, rgba(17,17,17,0.12) 40%, transparent 70%)`).
- **Columna social izquierda** (`left: 40px`, centrada vertical, oculta ≤640px): Instagram, YouTube y Email — cada uno con SVG inline 16×16 (`fill="currentColor"`) + label 12px `rgba(255,255,255,0.72)`.
- **Kicker derecho:** `/ Coach Personal y Mentora Financiera` (la `/` en coral), alineado a la derecha, `clamp(14px, 1.4vw, 20px)`.
- **H1:** "Yoselin Franco" — `clamp(40px, 11.5vw, 200px)`, blanco, `nowrap`, padding lateral 28px, alineado a la derecha (envuelto en `.hero-name-wrap` no seleccionable).
- **Scroll hint:** "Scroll ↓" centrado abajo (mono 11px, uppercase, `0.18em`), animación de flote `scrollBob` 2.2 s.
- **Entradas (solo tras `body.is-loaded`):** nombre `heroNameIn` 1.2 s delay 0.1 s; social `heroSocialIn` 1 s delay 0.35 s; kicker `heroFadeIn` 1 s delay 0.5 s.

### 8.3 Intro (`section#intro`) + Marquee
- Fondo `--black`, grid 2 columnas `1fr 1fr` con `gap: 80px`, centrado vertical, `max-width: 1200px`.
- **Izquierda:** statement "Nunca es tarde para **reinventarte.**" (`clamp(30px,3.6vw,54px)`, weight 600, `.deco` coral).
- **Derecha:** lead "Acompaño a personas en transición a reinventarse personal y financieramente — desde la experiencia real, no desde la teoría perfecta." (16px, `rgba(255,255,255,0.45)`, max 44ch) + fila de CTAs (`.intro-cta.solid` "Agenda tu sesión" → `#contact`; `.intro-cta` outline "Conoce mi historia" → `#about`) + estadísticas con separadores `stat-pipe` de 1px:
  - **2** (coral) — Países donde he vuelto a empezar
  - **+ 10** (blanco) — Años en finanzas
  - **+ 30K** (coral) — Personas inspiradas
- **Marquee:** banda blanca con bordes 1px, 6 frases duplicadas ×2 (cada span mono 11px uppercase `0.14em` opacidad 0.55, separador `·` coral con `margin-left: 48px`): "Finanzas que funcionan" · "Reinvención desde la experiencia" · "Acompañamiento en español e inglés" · "Mentoría Personal" · "Mentoría Financiera" · "Finanzas Personales desde Cero".

### 8.4 Sección 01 — "Por qué Yoselin" (`#value`, luz)
- Header: ghost `01`, kicker "Por qué Yoselin", H2 "Tres razones para **empezar**".
- Lista `.h-list` de 3 filas (borde inferior 1px, `padding: 18px 0`, nombre izquierda con `<em>` coral, número mono coral a la derecha):
  1. Finanzas que *funcionan* — 01
  2. Reinvención desde la *experiencia* — 02
  3. Acompañamiento *en español e inglés* — 03

### 8.5 Sección 02 — Servicios (`#services`, oscura)
- Header: ghost `02`, kicker "Qué ofrezco", H2 "Mentorías y **paquetes**", desc "100% online vía Google Meet, en español e inglés, disponible donde quiera que estés."
- **Grilla de 4 tarjetas** (4 col → 2 col ≤1280 → 1 col ≤980), cada una: badge mono, H3, precio coral con `<small>USD</small>`, descripción, `ul` con flechas `→`, botón `.btn.dark` "Agenda tu sesión" (Calendly, nueva pestaña):

| Badge | Servicio | Precio | Incluye | Link Calendly |
|---|---|---|---|---|
| Mentoría 1:1 | **Mentoría Personal** | $75 USD | 60 min Google Meet · Sesión grabada disponible · Plan de acción al cierre · Seguimiento por WhatsApp 48hs | `new-meeting-1` |
| Mentoría 1:1 | **Mentoría Financiera** | $85 USD | 60 min Google Meet · Análisis de situación financiera real · Plan financiero personalizado · Plantillas de presupuesto incluidas | `mentoria-1-1-financiera` |
| Paquete · 3 sesiones | **Paquete Reinvención** | $197 USD | 3 sesiones de 60 min · Plan de acción progresivo · Seguimiento entre sesiones · Materiales de trabajo incluidos | `paquete-3-sesiones-reinvencion` |
| Paquete · 3 sesiones | **Paquete Financiero** | $220 USD | 3 sesiones de 60 min · Análisis completo de presupuesto · Plan financiero a 6 meses · Plantillas y guías incluidas | `paquete-reinvencion-3-sesiones-` |

- Descripciones: Personal → "Para reinvención de vida, identidad, propósito, creencias y toma de decisiones."; Financiera → "Para organizar finanzas personales, presupuesto, deudas, ahorro e inversiones."; Reinvención → "3 sesiones de mentoría personal para construir una transformación real y sostenida."; Financiero → "3 sesiones de mentoría financiera para transformar tu relación con el dinero."
- **Nota final:** "**Importante:** Todos los servicios son 100% online, en español e inglés, disponibles donde quiera que estés." (mono, centrada).

### 8.6 Sección 03 — Quién Soy (`#about`, luz)
- Header: ghost `03`, kicker "Quién Soy", H2 "Mi historia es **mi método**".
- **Grid 2 col (`1fr 1fr`, gap 80px):**
  - **Izquierda:** `<img src="Image.png" alt="Yoselin Franco">` con `aspect-ratio: 3/4`, `object-fit: cover; object-position: center top`, **`filter: grayscale(100%) contrast(1.06)`**, y tag coral absoluto abajo-izquierda "QUIÉN SOY" (11px uppercase).
  - **Derecha (5 párrafos + cita + CTA + tabla + estado):**
    1. "Soy **Yoselin Franco**. Venezolana. Contadora Pública egresada de la UCAB. Más de 10 años de experiencia en finanzas, incluyendo el Gobierno de Canadá. Vivo en Montreal en una relación multicultural con un canadiense de Quebec que me enseñó que el tiempo libre existe — y yo le enseñé a comer arepas."
    2. "He migrado dos veces — Panamá, Canadá. He empezado de cero en cada país. He sobrevivido un accidente devastador con más de 9 operaciones en un año. He vivido el duelo de perder a mi hermano. He estado endeudada hasta el cuello y he reconstruido mis finanzas desde cero. He pasado por una relación que me borró — y he vuelto a escribirme."
    3. **Cita** (border-left 3px coral, 19px): "Todo eso no es mi historia de fondo. Es mi método."
    4. "Hoy acompaño a personas en transición — especialmente migrantes — a reinventarse personal y financieramente. Trabajo desde la coherencia entre identidad y dinero, porque he comprobado que no puedes transformar tus finanzas sin transformar primero cómo te ves a ti mismo/a. No desde la teoría perfecta. Desde la experiencia real de quien ya lo vivió."
    5. "Mi misión es ayudar a migrantes y personas en transición a reorganizar su dinero, reconectar con su identidad y construir una vida que eligieron — con herramientas concretas, acompañamiento real y sin juicio."
    6. CTA: "¿Listo/a para empezar? **Agenda tu sesión**" (enlace a `#contact`).
- **Tabla de perfil** (`.cert-block` con borde 1px; etiqueta coral mono 11px uppercase 150px / valor 14px):
  - Nombre: Yoselin Franco · Ubicación: Montreal, Canadá · Formación: Contadora Pública — UCAB · Diplomado Coaching con PNL · Experiencia: Más de 10 años en finanzas · Gobierno de Canadá · Idiomas: Español · Inglés · Redes: @soyyoselinfranco (Instagram) + enlace "YouTube: Yoselin Franco | Nunca es tarde" · Email: hola@yoselinfranco.com
- **Estado:** punto verde pulsante + "Actualmente en Montreal, Canadá · Disponible online".

### 8.7 Sección 04 — Cursos y Talleres (`#courses`, oscura)
- Header: ghost `04`, kicker "Cursos y Talleres", H2 "Aprende a tu **propio ritmo**", desc "Cursos, talleres y masterclases en vivo para reinventarte personal y financieramente."
- **Grilla de 6 tarjetas** (3 col → 1 col ≤980). Estructura de cada tarjeta: badge → H3 → precio → descripción → `ul` (4 bullets con `→`) → `.foot` con borde superior y botón "Comprar"/CTA:

| # | Badge | Tarjeta | Precio | CTA → destino |
|---|---|---|---|---|
| 1 | Curso grabado | **Finanzas Personales desde Cero** | $34 USD | Comprar → Hotmart `U106706696X` |
| 2 | Curso grabado | **Inversiones desde Cero** | $62 USD | Comprar → Hotmart `I107427455H` |
| 3 | Masterclass grabada | **Ahorro Inteligente** | $17 USD | Comprar → Hotmart `O107694194G` |
| 4 | Masterclass grabada | **Elígete** | $17 USD | Comprar → Hotmart `M107826405M` |
| 5 | Combo grabado | **Combo Metas 2027 – 4 Masterclasses** | $79 USD ~~$108~~ (`<s>`) | Comprar → Hotmart `H107827023X` |
| 6 | En vivo | **Talleres en Vivo** | Desde $27 USD | "Ver fechas y comprar" → abre modal |

- Contenido de bullets:
  - **c1:** Video completo en 4 módulos · Workbook + plantillas imprimibles · Lista de 50 creencias sobre el dinero · Acceso de por vida. Desc: "Curso grabado de 90min. El taller completo con workbook, plantillas y más."
  - **c3:** 4 módulos en video · Workbook + plantillas imprimibles · Guía de inversiones: Canadá, EE.UU. y Latinoamérica · Acceso de por vida. Desc: "Curso grabado de 75 min para empezar a invertir sin importar tu edad o cuánto tienes."
  - **mc1 (Ahorro Inteligente):** Disponible ya · acceso inmediato · Masterclass grabada · Método simple de ahorro · Sin importar cuánto ganes hoy. Desc: "Masterclass grabada para empezar a ahorrar con un método simple, aunque sientas que el dinero no te alcanza."
  - **mc2 (Elígete):** Disponible ya · acceso inmediato · Guía + workbook incluidos · Tarjetas «Soy alguien que…» · Recursos extra. Desc: "Vuelve a ti y crea la identidad que tus metas necesitan. Incluye guía, workbook, tarjetas «Soy alguien que…» y recursos extra."
  - **combo:** Incluye Saldar tus Deudas, Tu Presupuesto 2027, Crea tus Metas 2027 y Vision Board 2027 · En lugar de $108 · ahorras $29 · Incluye todas las grabaciones · Las 4 masterclasses en vivo. Desc: "Las 4 masterclasses en vivo a precio especial. Ahorras $29. Incluye todas las grabaciones."
  - **c2 (Talleres en Vivo):** 90 minutos en vivo · Grabación incluida · Workbook y materiales · Preguntas en tiempo real. Desc: "Próximas masterclasses en vivo: Saldar tus Deudas, Tu Presupuesto 2027, Crea tus Metas 2027 y Vision Board 2027."

### 8.8 Modal "Talleres en Vivo" (`#talleresModal`)
- **Overlay:** `rgba(20,14,10,0.6)` + `backdrop-filter: blur(4px)`; modal `max-width: 860px`, `max-height: 86vh`, fondo `--off-white`, `border-radius: 18px`, `padding: 40px 36px`, entrada `translateY(20px) scale(0.98)` → normal.
- **Botón ✕** circular arriba-derecha (38px, fondo blanco → hover coral).
- Título "Talleres en Vivo" (1.9rem) · Subtítulo "Masterclasses en vivo de 90 minutos. Desde $27 USD. Grabación incluida." · Línea coral mono "Compra tu lugar directamente en Hotmart".
- **Tabla** (`table-layout: fixed`, `min-width: 640px`; columnas 18% / 22% / 40% / 20%; thead mono 11px uppercase con borde inferior 2px; filas con hover gold `rgba(223,182,91,0.10)`):

| Masterclass | Fecha | Subtítulo | Link de compra |
|---|---|---|---|
| Saldar tus Deudas | Mié 14 oct 2026 · 7:00 PM Montreal · 90 min | Un plan claro para pagar lo que debes y recuperar tu paz financiera. Incluye la grabación. | Comprar en Hotmart → `F107823801K` |
| Tu Presupuesto 2027 | Mié 18 nov 2026 · 7:00 PM Montreal · 90 min | Organiza tu dinero y empieza el año sabiendo a dónde va cada dólar. Incluye la grabación. | Comprar en Hotmart → `H107825578L` |
| Crea tus Metas 2027 | Mié 25 nov 2026 · 7:00 PM Montreal · 90 min | Define lo que quieres lograr y conviértelo en pasos que sí vas a cumplir. Incluye la grabación. | Comprar en Hotmart → `D107825979J` |
| Vision Board 2027 | Sáb 5 dic 2026 · 11:00 AM Montreal · 90 min | Crea en vivo el tablero que te recuerde cada día la vida que estás eligiendo. Incluye la grabación. | Comprar en Hotmart → `R107826208N` |

- Fecha: mono 12px coral weight 600. Link: mono 12px coral con `text-decoration: underline` (`text-underline-offset: 3px`), hover `--black`.
- **Nota inferior:** "Todas las masterclasses son en vivo, en español y la grabación queda incluida." (mono 11px).
- Cierra con ✕, clic en overlay o `Escape` (ver §6.6).

### 8.9 Sección 05 — Testimonios (`#testimonials`, luz)
- Header: ghost `05`, kicker "Testimonios", H2 "Resultados **reales**", desc "Historias de personas que decidieron reinventarse y dieron el primer paso."
- **Grilla 2×2** (`.quotes`, `gap: 24px`) con 4 tarjetas blancas: 5 estrellas coral (`★★★★★`), cita en español **sin traducir** (clampeada a 4 líneas con `-webkit-line-clamp`), botón "Ver más"/"Ver menos" en coral, y pie con autor (coral bold) + rol (gris 12px):
  1. **Jose Luis Solano** — Taller Inversiones desde Cero
  2. **Mariana Leon** — Mentoría Financiera 1:1
  3. **Genesis Hernández** — Taller Finanzas desde Cero
  4. **Eliana Alvarez** — Mentoría Financiera 1:1
- CTA final centrado (margin-top 48px): "Deja tu reseña en Google" → `https://g.page/r/Ca3kal9hBJOuEBI/review`.

### 8.10 Sección 06 — Contacto (`#contact`, oscura)
- Header: ghost `06`, kicker "Contacto · Agenda", H2 "Da el primer paso hacia tu **reinvención**".
- **Tarjeta única "Cómo funcionan las sesiones"** (fondo `#4A3728`, padding 36px, borde 1px): desc "Mentoría y coaching personal 100% online. Aquí te cuento cómo es el proceso." + lista con iconos `›`:
  - Sesiones vía Google Meet · Disponible donde quiera que estés · En español e inglés, con calidez y sin filtros · Pago con tarjeta vía Stripe
  - Botón `.btn.line` "Ver servicios y precios" → `#services`.
- **Panel "Política de sesiones"** (título con "sesiones" en coral), `ul` a 2 columnas con `✓` coral:
  - Reagendamiento: mínimo 48 horas de anticipación
  - Cancelación: mínimo 24 horas de anticipación
  - Espera máxima: 15 minutos. Pasado ese tiempo la sesión se considera realizada
  - Reembolsos: no se realizan una vez agendada la sesión
  - Alcance: mentoría y coaching personal. No reemplaza atención psicológica profesional
  - Nota: "Tus datos y conversaciones son tratados con confidencialidad." (itálica)

### 8.11 Footer
- Fondo `--black`, borde superior 1px, `padding: 56px 40px 32px`.
- **Grid 3 col (`1.4fr 1fr 1fr`, gap 48px):**
  1. Marca "Yoselin." (18px bold, punto coral) + desc "Coach personal y mentora financiera para migrantes y personas que empiezan de nuevo. Desde la experiencia real, no desde la teoría perfecta."
  2. **Explora:** Quién Soy (`#about`) · Servicios (`#services`) · Cursos y Talleres (`#courses`) · Testimonios (`#testimonials`).
  3. **Contacto:** hola@yoselinfranco.com (mailto) · Instagram · @soyyoselinfranco · YouTube · Nunca es tarde.
- **Copyright** (borde superior, flex space-between): "© [año dinámico] Yoselin Franco · yoselinfranco.com" + lema coral ""Nunca es tarde para reinventarte."".

---

## 9. Enlaces externos

| Tipo | Destino |
|---|---|
| Agendar sesión (4 variantes) | `calendly.com/hola-yoselinfranco/` → `new-meeting-1`, `mentoria-1-1-financiera`, `paquete-3-sesiones-reinvencion`, `paquete-reinvencion-3-sesiones-` |
| Cursos grabados (Hotmart) | `U106706696X` (Finanzas Personales), `I107427455H` (Inversiones), `O107694194G` (Ahorro Inteligente), `M107826405M` (Elígete), `H107827023X` (Combo Metas 2027) |
| Masterclasses en vivo (Hotmart) | `F107823801K` (Saldar tus Deudas), `H107825578L` (Tu Presupuesto 2027), `D107825979J` (Crea tus Metas 2027), `R107826208N` (Vision Board 2027) |
| Instagram | `instagram.com/soyyoselinfranco` |
| YouTube | `youtube.com/@soyyoselinfranco` (enlaces en `https://`) |
| Email | `hola@yoselinfranco.com` (mailto) |
| Reseñas Google | `g.page/r/Ca3kal9hBJOuEBI/review` |
| Dominio | `yoselinfranco.com` |

**Seguridad de enlaces:** todo enlace externo con `target="_blank"` lleva `rel="noopener noreferrer"` (previene reverse tabnabbing y envío de `Referer`); los `mailto:` y anclajes internos no lo requieren. El flujo de compra va directo a Hotmart (checkout propio del producto), no por DM en Instagram.

---

## 10. Accesibilidad y metadatos

- `aria-label` en botones (✕ del modal, hamburguesa), `role="dialog"` + `aria-hidden` en el modal, `alt="Yoselin Franco"` en la foto, `aria-hidden` en SVGs decorativos y en capas decorativas del hero.
- `lang="es"` inicial, actualizado por `applyLang`; `<html>` con `scroll-behavior: smooth`.
- SEO: `<title>` y `<meta name="description">` en español (ambos se reescriben con `meta_title` al cambiar idioma).
- **No hay CSP** (archivo único con `<style>`/`<script>` inline); si se despliega en Netlify/Cloudflare/Vercel, recomendar CSP por cabeceras HTTP.

---

## 11. Checklist de replicación

1. Un solo `index.html`; CSS en `<style>` del head, JS en `<script>` final del body.
2. Copiar verbatim: `:root` (§4), Google Fonts (§3), reset base (§4).
3. Reproducir el orden de bloques del §1 y las 7 secciones numeradas 01–06 + intro + marquee + splash + modal.
4. Mantener el sistema `data-i18n` con **205 claves idénticas** en `es`/`en`/`fr` (el contenido ES es el listado en §8; EN/FR son traducciones equivalentes dentro del mismo diccionario).
5. Respetar tokens: radios (999px pills / 18px modal / 0 tarjetas), grillas hairline de 1px, curva `cubic-bezier(0.16,1,0.3,1)`, prefijo `// ` en kickers, números fantasma con stroke.
6. Verificar comportamientos: splash ≤4.5 s, cursor lerp 0.22, nav indicador/ocultar, reveal con IO 0.12, modal con 3 formas de cierre, toggle de testimonios, año dinámico.
7. Verificar breakpoints: 1280 / 980 / 700 / 640 / 480.
8. Assets: solo `Image.png` (grayscale 3:4) y los enlaces externos de la §9.

---

## 12. Historial de cambios aplicados

- **Hero / Inicio (kicker):** "Mentora en Reinvención Personal y Financiera" → "Coach Personal y Mentora Financiera" (también en `<title>` y `meta_title`; traducciones ES / EN / FR).
- **Sección 02 — Servicios:**
  - Subtítulo → "100% online vía Google Meet, en español e inglés, disponible donde quiera que estés."
  - Nota al cierre → "Todos los servicios son 100% online, en español e inglés, disponibles donde quiera que estés."
- **Sección 03 — Quién Soy:** reescritura del bloque de historia (público "especialmente migrantes", párrafo de coherencia entre identidad y dinero, bloque de misión y CTA "¿Listo/a para empezar? Agenda tu sesión").
- **Footer:** descripción → "**Coach personal y mentora financiera** para migrantes y personas que empiezan de nuevo…" (traducciones EN / FR actualizadas).
- **Sección 04 — Cursos:** subtítulo → "Cursos, talleres y masterclases en vivo para reinventarte personal y financieramente".
- **Sección 04 — Actualización de masterclasses:**
  - Grilla de 3 → **6 tarjetas**: Ahorro Inteligente ($17), Elígete ($17) y Combo Metas 2027 ($79 en lugar de $108) con CTA a Hotmart.
  - Tarjeta "Talleres en Vivo": descripción con las 4 próximas masterclasses, duración "90 minutos en vivo", CTA "Ver fechas y comprar".
  - **Modal:** fuera Ahorro Inteligente y Elígete (grabadas); nuevas fechas/links de las 4 en vivo (mié 14 oct, mié 18 nov, mié 25 nov y sáb 5 dic; 90 min, 7:00 PM Montreal salvo Vision Board 11:00 AM).
  - Columna "Palabra clave" (DM Instagram) → **"Link de compra"** con "Comprar en Hotmart"; aviso del modal → "Compra tu lugar directamente en Hotmart".
  - Claves nuevas: `mc1_*`, `mc2_*`, `combo_*`, `mc_btn`, `mc_buy`, `modal_th_link`, `ws1_*`–`ws4_*`; eliminadas `ws5_*`, `ws6_*`, `ws*_key`, `modal_th_key`.
- **Renombramiento:** "Sal de tus Deudas" → **"Saldar tus Deudas"** en toda la landing y en este documento.
- **Sección 01 y marquee:** "Acompañamiento en español" → "Acompañamiento **en español e inglés**".
- **Sección 06:** "Disponible en Canadá, EE.UU. y Latinoamérica" → "Disponible **donde quiera que estés**"; "En español, con calidez y sin filtros" → "**En español e inglés**, con calidez y sin filtros".
- **Seguridad:** `rel="noopener noreferrer"` en los enlaces externos con `target="_blank"`; YouTube de `http://` a `https://`.
- **Nota:** sin CSP estricta por ser landing estática de un solo archivo con código inline; recomendar CSP por cabeceras al desplegar en hosting con soporte HTTP.
