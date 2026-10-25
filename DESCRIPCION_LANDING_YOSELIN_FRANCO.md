# Landing Page — Yoselin Franco · Coach Personal y Mentora Financiera

## Guía técnica de construcción y replicación — v2 (25 oct 2026)

> **Propósito de este documento:** ser la **fuente de verdad** del proyecto. Permite que cualquier agente de IA o desarrollador **replicue `index.html` exactamente**, comprendiendo el proceso, los lenguajes, la metodología, los estilos, los formatos y cada detalle de cómo está creado. Todo dato marcado como *verbatim* debe copiarse carácter por carácter.
>
> **Regla de oro:** si el código y este documento difieren, se corrige **ambos**. Este archivo se actualiza en cada cambio sobre `index.html` (ver §15).

| Dato | Valor |
|---|---|
| **Archivo fuente único** | `index.html` (HTML5 + CSS3 + JS vanilla, un solo archivo, ~117 KB / 1.621 líneas) |
| **Dominio** | yoselinfranco.com |
| **Idiomas** | Español (ES) · Inglés (EN) · Francés (FR) — selector en la navegación |
| **Tagline principal** | "Nunca es tarde para reinventarte." |
| **Asset de imagen** | `Image.png` (foto en sección 03) — única imagen del sitio |
| **Dependencias externas** | Solo Google Fonts (CDN). Sin frameworks, sin build, sin npm |
| **Estado actual (25 oct 2026)** | **Cabecera (nav): sin CTA** — el botón "Agenda tu sesión" está comentado. Sección 02: solo visible **"Programa Ordena tu Dinero"** (precio oculto). Sección 04: solo visible **"Talleres en Vivo"**. Modal: sin la fila **"Saldar tus Deudas"**. Las demás tarjetas/filas/botón están **comentados, no borrados** → ver §10 |

---

## 0. Cómo usar esta guía (instrucciones para una IA)

1. **Leer en orden:** §1 (arquitectura) → §2 (metodología) → §3–§5 (estilos) → §6–§7 (i18n y comportamiento) → §8 (responsive) → §9 (contenido por sección) → §10 (estado actual) → §11 (limitaciones) → §14 (checklist) → §15 (historial).
2. **Bloques `verbatim`:** los apartados marcados como verbatim (§4.1 Google Fonts, §4.3 variables, §4.4 reset, §1.3 meta) se copian tal cual, sin reescribirlos con otro estilo.
3. **No "arreglar" lo que está oculto:** las tarjetas de servicios y cursos que no se ven están **comentadas a propósito** (§10). No borrar ese código ni sus claves `data-i18n`; para reactivarlas, seguir el procedimiento de §10.
4. **Todo cambio de texto vivo** se hace en el HTML **y** en los tres idiomas del diccionario `translations` (§6).
5. **Al terminar cualquier tarea:** pasar el checklist de §14 y registrar el cambio en §15.

---

## 1. Stack, lenguajes y arquitectura

### 1.1 Roles de cada lenguaje

| Lenguaje | Rol en el archivo | Dónde vive |
|---|---|---|
| **HTML5** | Estructura semántica + contenido + atributos `data-i18n` (ganchos de traducción) + `aria-*` | `<body>` (líneas ~540–1090) |
| **CSS3** | Todo el diseño: variables, grid, `clamp`, `backdrop-filter`, keyframes, breakpoints | `<style>` dentro del `<head>` |
| **JavaScript ES6+** | i18n, splash, cursor, nav, reveal, modal, toggle, año dinámico. **Sin dependencias** | `<script>` al final del `<body>` |

- **Sin frameworks:** ni React, ni Tailwind, ni Bootstrap. Sin build, sin npm, sin paso de compilación: se abre `index.html` y funciona.
- **Página única (one-pager)** con anclajes `#hero`, `#intro`, `#value`, `#services`, `#about`, `#courses`, `#testimonials`, `#contact`.

### 1.2 Orden exacto de bloques dentro de `index.html`

1. `<!DOCTYPE html>` → `<html lang="es">` → `<head>`: charset UTF-8, viewport, `<title>`, `<meta name="description">`, preconnects + Google Fonts, `<style>` (todo el CSS, en este orden temático: tokens → reset → cursor → splash → utilidades (`.sec-label`, `.reveal`) → nav → hero → intro → secciones numeradas → services → about → courses → testimonials → contact → footer → marquee → modal → responsive).
2. `<body>`: `div#cursor.custom-cursor` → Splash `#splash` → `nav#nav` → `header#hero` → `section#intro` → `.marquee-wrap` → `section#value` (01) → `section#services` (02) → `section#about` (03) → `section#courses` (04) → `section#testimonials` (05) → `section#contact` (06) → `footer` → modal `#talleresModal` → `<script>`.

### 1.3 Meta head verbatim

```html
<title>Yoselin Franco | Coach Personal y Mentora Financiera</title>
<meta name="description" content="Acompaño a personas en transición a reinventarse personal y financieramente. Mentora en reinvención personal y financiera para migrantes y personas que empiezan de nuevo.">
```

No hay favicon ni etiquetas Open Graph (limitación conocida, ver §11).

---

## 2. Metodología de construcción (proceso paso a paso)

Esta es la secuencia usada para crear el archivo y la que debe seguirse para recrearlo desde cero. Cada fase deja un resultado verificable antes de pasar a la siguiente.

### Fase 1 — Esqueleto HTML
Crear el `index.html` vacío con el orden de §1.2: `<head>` con meta + fuentes, `<style>` vacío, `<body>` con las secciones como contenedores vacíos (`<section id="...">`) y `<script>` vacío. **Primero estructura, luego estilo, luego comportamiento.**

### Fase 2 — Tokens y reset
Definir `:root` (§4.3) y el reset base (§4.4). Todo color del sitio sale de una variable; prohibido hardcodear el coral/marrón/nude en reglas nuevas.

### Fase 3 — Tipografía base
`body { font-family: var(--font) }`, tamaños de encabezados con `clamp()`, kickers `.sec-label` con `::before { content: '// '; }`, mono para microtexto.

### Fase 4 — Componentes globales
Construir en este orden: `.reveal` (+ retardos `.d1`–`.d5`) → `.numbered-section` + `.ns-header` + `.ns-ghost-num` → `.btn` (variantes `dark`, `solid`, `line`) → `.badge` → grillas hairline → `.marquee`.

### Fase 5 — Secciones y contenido
Rellenar secciones en orden DOM (§9), alternando fondos claro/oscuro. Cada elemento traducible recibe `data-i18n="clave"`.

### Fase 6 — Sistema i18n
Crear el diccionario `translations` con `es`, `en` y `fr` **con las mismas 206 claves** (§6). El HTML es la fuente del idioma por defecto (ES).

### Fase 7 — Comportamiento JavaScript
Implementar en orden: i18n/selector de idioma → año dinámico → cursor → splash → nav (ocultar + indicador + menú móvil) → reveal (IntersectionObserver) → modal de talleres → toggle de testimonios (§7).

### Fase 8 — Responsive
Aplicar los breakpoints de §8 de mayor a menor (1280 → 980 → 700 → 640 → 480).

### Fase 9 — QA
Checklist de §14 + revisión en 3 anchos (desktop 1440, tablet 768, móvil 375) + prueba de los 3 idiomas.

### 2.1 Formatos y convenciones de escritura

| Aspecto | Formato |
|---|---|
| **Indentación** | 2 espacios (HTML y CSS y JS) |
| **Comentario de bloque CSS/JS** | `/* ===== NOMBRE ===== */` |
| **Comentario de bloque HTML** | `<!-- ===== NOMBRE ===== ... ===== -->` (nunca anidar `<!--` dentro) |
| **Nomenclatura CSS** | Plana y descriptiva en minúsculas con guiones: `.service-card`, `.course-card`, `.quote-toggle`. Prefijo `ns-` = bloques de secciones numeradas; `hero-`/`intro-`/`about-`/`contact-` = por sección; `nav-` = navegación |
| **Nomenclatura i18n** | Prefijo por bloque: `nav_`, `hero_`, `st`, `value_`, `serv_`, `c1_`/`c3_` (cursos), `mc1_`/`mc2_` (masterclasses grabadas), `combo_`, `c2_` (talleres en vivo), `ws1_`–`ws4_` (filas del modal), `modal_`, `test_`, `contact_`, `ctc2_`, `policy_`, `footer_`, `p_` (tabla de perfil), `c_` (copyright) |
| **Orden dentro de una tarjeta** | badge → `<h3>` → `.price` → `.desc` → `ul` (4 bullets) → `.foot` con botón |
| **Imagen** | `<img src="Image.png" alt="Yoselin Franco">` con `aspect-ratio: 3/4` y `filter: grayscale(100%)` |
| **Iconos** | SVG inline 16×16 con `fill="currentColor"` y `aria-hidden="true"`; bullets como `::before` (`→`, `✓`, `›`) |
| **Enlaces externos** | `target="_blank" rel="noopener"` (ver §11 sobre `noreferrer`) |
| **Radios** | 999px pills/botones/nav · 18px modal · 20px menú móvil · 0 el resto |
| **Curva de animación** | `cubic-bezier(0.16, 1, 0.3, 1)` (la del sistema) |

### 2.2 Cómo agregar un elemento nuevo (receta)

1. **Tarjeta nueva en grilla:** copiar una tarjeta existente, cambiar textos, asignar claves `data-i18n` nuevas (`xx_título`, `xx_desc`, `xx_l1..l4`, `xx_btn`) y agregarlas a `es`, `en` y `fr`. Si la grilla está en 1 columna por §10, restaurar el `repeat(n, 1fr)` original.
2. **Texto visible nuevo:** siempre con `data-i18n`; si no se traduce, justificarlo en §6.2 (excepciones).
3. **Precio nuevo:** `<div class="price">$NN <small>USD</small></div>` (con `<s>$AAA</s>` para precio tachado).
4. **Sección nueva:** usar `.numbered-section`, `.ns-header` con `.ns-ghost-num`, kicker `.sec-label` y numeración consecutiva; registrarla en el orden de §1.2 y en `sections` del indicador de nav (§7.3).

---

## 3. Paleta de colores

### 3.1 Tokens principales (`:root`)

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

### 3.2 Colores derivados (usados directamente en CSS, no en variables)

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

## 4. Tipografía, variables y reset

### 4.1 Carga verbatim (Google Fonts)

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Dancing+Script:wght@600;700&family=Playfair+Display:ital,wght@0,700;0,900;1,700&family=Space+Grotesk:wght@300;400;500;600;700&family=DM+Mono:wght@400;500;700&display=swap" rel="stylesheet">
```

> **Nota:** `Dancing Script` y `Playfair Display` se cargan pero **no se usan en ningún CSS** (carga residual, ver §11). Las únicas familias aplicadas son:

| Variable | Familia | Rol |
|---|---|---|
| `--font` | `Space Grotesk, sans-serif` | Todo el texto (body, títulos, botones) |
| `--mono` | `DM Mono, monospace` | Kickers, fechas, badges, tabla, marquee, stats, códigos |

### 4.2 Escala tipográfica

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

### 4.3 Variables CSS (`:root`) — verbatim

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

### 4.4 Reset base verbatim

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
| **Grillas con separación de 1px** | `display:grid; gap:1px; background: var(--border-dark); border: 1px solid var(--border-dark);` con tarjetas de fondo sólido (efecto hairline). **⚠ Estado actual:** `.services-grid` y `.courses-grid` están forzadas a **1 columna** por §10 |
| **Tarjetas oscuras** | fondo `#4A3728`, hover `#553f2e`, sin border-radius (esquinas rectas) |
| **Tarjetas claras** | fondo `#fff`, borde `--border-light`, hover borde accent + `translateY(-4px)` + `box-shadow: 0 20px 50px rgba(0,0,0,0.06)` |
| **Botones (`.btn`)** | `padding: 13px 26px; border-radius: 999px; font-size: 13px; font-weight: 700; letter-spacing: 0.04em` |
| **`.btn.dark`** | fondo accent, texto blanco, hover `#e58278` + `translateY(-2px)` |
| **`.btn-line`** | borde `rgba(255,255,255,0.3)`, texto `rgba(255,255,255,0.8)`, hover blanco (⚠ ver bug en §11) |
| **Badges** | mono 10px uppercase, `letter-spacing: 0.1em`, borde 1px, `padding: 4px 12px`; variante `.accent`/`.gratis` en coral |
| **Bullets de listas** | `li::before { content: '→' }` en coral (tarjetas) o `'✓'` (política) o `'›'` (contacto, como `<span class="ico">`) |
| **Radios** | pills/botones/nav `999px`; modal `18px`; menú móvil `20px`; el resto `0` |
| **Curva de animación estándar** | `cubic-bezier(0.16, 1, 0.3, 1)` |

---

## 6. Sistema i18n

### 6.1 Cómo funciona
- Diccionario `const translations = { es: {...}, en: {...}, fr: {...} }` — **206 claves por idioma, claves idénticas en los tres** (verificado).
- Todo texto traducible lleva `data-i18n="clave"`; `applyLang(lang)` hace `el.innerHTML = translations[lang][key]` (por eso las claves pueden contener HTML: `<span class="deco">`, `<strong>`, `<em>`, `<a>`).
- `applyLang` también actualiza `document.documentElement.lang` y `document.title` (`meta_title`).
- Selector: botones `.lang-btn[data-lang]`; persistencia en `localStorage['yoselin-lang']` (default `es`); se aplica al cargar (`applyLang(savedLang)`).
- **Claves dentro de comentarios HTML** no existen en el DOM: `applyLang` las ignora, pero **las claves permanecen en el diccionario** (necesario para reactivar tarjetas sin reescribir traducciones).

### 6.2 Excepciones (no traducible, por diseño)
- Los textos de testimonios (reseñas textuales, siempre en español).
- Botones "Ver más"/"Ver menos" (hardcodeados en ES) y "Scroll ↓".
- Nombres propios de programa: **"Programa Ordena tu Dinero"** se mantiene en español también en EN y FR (decisión de marca).

### 6.3 Claves huérfanas (definidas pero sin uso en el HTML)
`meta_title`* , `serv_badge_free`, `serv_badge_phase`, `serv_t1`, `serv_d1`, `serv1_l1..l3`, `serv_t6`, `serv_d6`, `serv6_l1..l4`, `btn_reserve`, `phase2`, `c2_btn2`, `contact_sub`, `ctc1_title`, `ctc1_desc`, `ctc1_l1..l4`, `ctc1_btn`.
(* `meta_title` sí se usa desde JS.) Se conservan por si se reactivan bloques (§10).

---

## 7. Comportamiento JavaScript (un solo `<script>`)

### 7.1 Splash (pantalla de carga)
- Fondo `#4A3728` a pantalla completa (z-index 9999): kicker `// Coach Personal y Mentora Financiera` (mono, accent), nombre "Yoselin **Franco**" (`clamp(36px, 9vw, 80px)`, "Franco" en accent) y barra de 260px×2px.
- JS: incrementa el ancho aleatoriamente cada 150 ms (`+10 a +26%`); al 100% espera 300 ms y oculta con fade 0.6 s; **máximo 4.5 s**. Al ocultarse agrega `body.is-loaded` (dispara animaciones de entrada del hero) y `cursor.is-ready`.

### 7.2 Cursor personalizado
- Círculo de 24 px, borde 2px accent, glow `rgba(232,64,32,0.7)`, `z-index: 9999`, `pointer-events:none`.
- Sigue al mouse con lerp `0.22` vía `requestAnimationFrame` (vars `--cx/--cy`); sobre `a, button, [data-cursor-hover]` escala a 1.8 con fondo coral translúcido.
- Oculto por CSS/JS en dispositivos táctiles (`pointer: coarse` / sin hover); el cursor nativo se anula con `cursor: none` solo en `@media (hover:hover) and (pointer:fine)`.

### 7.3 Navegación
- **Ocultar al bajar:** si `scrollY > lastScroll && scrollY > 160` → clase `is-hidden` (opacity 0 + translateY(-16px)).
- **Indicador activo:** píldora coral (`nav-indicator`) que se anima (`left/width` 0.45 s) bajo el link de la sección visible; usa `sections = ['hero','about','services','courses','testimonials','contact']` y considera activa la cuya `top <= 40%` del viewport; deshabilitado `≤980px`. ⚠ Orden no visual, ver §11.
- **Menú móvil:** `☰` alterna `.open` en `.nav-pill` (dropdown vertical, fondo `rgba(17,17,17,0.97)`, radio 20px).

### 7.4 Reveal on scroll
`IntersectionObserver` con `threshold: 0.12`, agrega `.in` y se desuscribe (una sola vez).

### 7.5 Modal de talleres
- Abre con `[data-open-talleres]` (tarjeta "Talleres en Vivo"): agrega `.open` al overlay, `aria-hidden="false"` y `body.style.overflow = hidden`.
- Cierra con: botón ✕, clic en el overlay (`e.target === modal`) o tecla `Escape`.

### 7.6 Testimonios (toggle)
`.quote-toggle` alterna la clase `.expanded` en `.quote-text` (rompe el `-webkit-line-clamp: 4`) y cambia el texto del botón a "Ver menos"/"Ver más" (hardcoded ES).

### 7.7 Misceláneos
- `#year` rellena el año actual en el copyright.
- Animación `livePulse` infinita en el punto verde de disponibilidad.
- Marquee: `translateX(0 → -50%)` en 26 s lineales infinitos (contenido duplicado ×2 para loop perfecto).

---

## 8. Responsive (breakpoints exactos)

| Breakpoint | Efectos |
|---|---|
| **≤1280px** | `.services-grid` → **1 columna** (estado temporal; en normalidad: 2 columnas — ver §10) |
| **≤980px** | `intro-inner`, `about-grid`, `contact-grid`, `quotes` → 1 columna; `services-grid`, `courses-grid` → 1 columna; aparece `.menu-toggle` ☰; `.nav-pill` pasa a dropdown vertical oculto (`.open` lo muestra); se oculta `.nav-indicator`; `.ns-header` en wrap; `.hero-social` a `left:24px` |
| **≤700px** | Se oculta el `.nav-cta` ("Agenda tu sesión") |
| **≤640px** | `.intro-stats` vertical y `.stat-pipe` ocultos; `footer-grid` 1 columna; `policy ul` 1 columna; `.hero-social` oculto; `ns-ghost-num` 64px; botones de tarjetas a 100% de ancho; modal `padding: 26px 18px` y tabla con `min-width: 700px` (scroll horizontal interno) |
| **≤480px** | Paddings reducidos a 20px; `ns-h2` 30px; `ns-desc` 14px; tarjetas con padding 26px 22px; `intro-statement` 30px; ajustes finos de hero/lang buttons |

---

## 9. Detalle por sección (orden del DOM)

### 9.0 Splash
Ver §7.1.

### 9.1 Navegación (`nav#nav`)
- **Pill flotante fija:** `position: fixed; top: 22px; left: 50%; transform: translateX(-50%)`, fondo `rgba(17,17,17,0.55)` + `backdrop-filter: blur(20px) saturate(140%)`, borde 1px blanco translúcido, `border-radius: 999px`, `z-index: 100`.
- **Logo:** "Yoselin" + punto coral (`.nav-dot`), con borde derecho separador → enlaza a `#hero`.
- **Links:** Inicio · Quién Soy · Servicios · Cursos · Testimonios (`data-i18n: nav_home, nav_about, nav_services, nav_courses, nav_testimonials`), 12.5px, `rgba(255,255,255,0.6)` → blanco en hover/activo.
- **Selector:** botones `ES | EN | FR` (mono 10px uppercase; activo con fondo coral).
- **CTA:** ~~"Agenda tu sesión"~~ **COMENTADO (oculto, §10)** — el `<a>` con `data-i18n="nav_book"` está envuelto en un comentario HTML tras el botón hamburguesa, con la cabecera `<!-- CTA "Agenda tu sesión" ELIMINADO DE LA CABECERA — oculto temporalmente ...`. Al restaurarlo usa las clases **`btn dark nav-cta`** → mismo estilo, tamaño y proporción que "Ver fechas y comprar" (coral, 13px bold, padding 13px 26px, pill 999px). La clase `nav-cta` y su regla `display:none` en ≤700px se conservan para la restauración. La clave `nav_book` sigue en el diccionario i18n.
- **Hamburguesa:** botón `☰` (solo ≤980px), `aria-label="Menú"`.

### 9.2 Hero (`header#hero`)
- `min-height: 100dvh`, fondo oscuro, `justify-content: flex-end`.
- **Fondo:** *no hay foto*; `.hero-photo-wrap` es un degradado `linear-gradient(160deg, #4A3728 0%, #3d2d21 55%, #2b1f16 100%)` + `.hero-vignette` (`linear-gradient(to top, rgba(17,17,17,0.62) 0%, rgba(17,17,17,0.12) 40%, transparent 70%)`).
- **Columna social izquierda** (`left: 40px`, centrada vertical, oculta ≤640px): Instagram, YouTube y Email — cada uno con SVG inline 16×16 (`fill="currentColor"`) + label 12px `rgba(255,255,255,0.72)`.
- **Kicker derecho:** `/ Coach Personal y Mentora Financiera` (la `/` en coral), alineado a la derecha, `clamp(14px, 1.4vw, 20px)`.
- **H1:** "Yoselin Franco" — `clamp(40px, 11.5vw, 200px)`, blanco, `nowrap`, padding lateral 28px, alineado a la derecha (envuelto en `.hero-name-wrap` no seleccionable).
- **Scroll hint:** "Scroll ↓" centrado abajo (mono 11px, uppercase, `0.18em`), animación de flote `scrollBob` 2.2 s.
- **Entradas (solo tras `body.is-loaded`):** nombre `heroNameIn` 1.2 s delay 0.1 s; social `heroSocialIn` 1 s delay 0.35 s; kicker `heroFadeIn` 1 s delay 0.5 s.

### 9.3 Intro (`section#intro`) + Marquee
- Fondo `--black`, grid 2 columnas `1fr 1fr` con `gap: 80px`, centrado vertical, `max-width: 1200px`.
- **Izquierda:** statement "Nunca es tarde para **reinventarte.**" (`clamp(30px,3.6vw,54px)`, weight 600, `.deco` coral).
- **Derecha:** lead "Acompaño a personas en transición a reinventarse personal y financieramente — desde la experiencia real, no desde la teoría perfecta." (16px, `rgba(255,255,255,0.45)`, max 44ch) + fila de CTAs (**`btn dark`** "Agenda tu sesión" → `#contact`, mismo estilo que "Ver fechas y comprar"; `.intro-cta` outline "Conoce mi historia" → `#about`) + estadísticas con separadores `stat-pipe` de 1px:
  - **2** (coral) — Países donde he vuelto a empezar
  - **+ 10** (blanco) — Años en finanzas
  - **+ 30K** (coral) — Personas inspiradas
- **Marquee:** banda blanca con bordes 1px, 6 frases duplicadas ×2 (cada span mono 11px uppercase `0.14em` opacidad 0.55, separador `·` coral con `margin-left: 48px`): "Finanzas que funcionan" · "Reinvención desde la experiencia" · "Acompañamiento en español e inglés" · "Mentoría Personal" · "Mentoría Financiera" · "Finanzas Personales desde Cero".

### 9.4 Sección 01 — "Por qué Yoselin" (`#value`, luz)
- Header: ghost `01`, kicker "Por qué Yoselin", H2 "Tres razones para **empezar**".
- Lista `.h-list` de 3 filas (borde inferior 1px, `padding: 18px 0`, nombre izquierda con `<em>` coral, número mono coral a la derecha):
  1. Finanzas que *funcionan* — 01
  2. Reinvención desde la *experiencia* — 02
  3. Acompañamiento *en español e inglés* — 03

### 9.5 Sección 02 — Mentorías y paquetes (`#services`, oscura) ⚠ ESTADO ACTUAL
- Header: ghost `02`, kicker "Qué ofrezco", H2 "Mentorías y **paquetes**", desc "100% online vía Google Meet, en español e inglés, disponible donde quiera que estés."
- **Grilla:** actualmente **1 columna** (ver §10). En normalidad: `repeat(4, 1fr)` → 2 col ≤1280 → 1 col ≤980.
- **Tarjeta VISIBLE (sin precio, §10.2):**

| Badge | Servicio | Precio | Descripción | Incluye | Link Calendly |
|---|---|---|---|---|---|
| Paquete · 3 sesiones | **Programa Ordena tu Dinero** (antes "Paquete Financiero") | ~~$220 USD~~ **OCULTO** (comentado) | "3 sesiones de mentoría financiera para transformar tu relación con el dinero." | 3 sesiones de 60 min · Análisis completo de presupuesto · Plan financiero a 6 meses · Plantillas y guías incluidas | `paquete-reinvencion-3-sesiones-` |

- **CTA "Agenda tu sesión"** (`btn dark` → Calendly `paquete-reinvencion-3-sesiones-`): **píldora compacta alineada a la izquierda**, del ancho de su texto — idéntico en estilo, tamaño y proporción al botón "Ver fechas y comprar" de la tarjeta "Talleres en Vivo". Esto se logra con `.service-card .btn { margin-top: auto; align-self: flex-start; text-align: center; }`: sin `align-self`, el `flex-direction: column` de `.service-card` (con `align-items` por defecto `stretch`) estiraba el botón a todo el ancho de la tarjeta. En ≤640px ambos botones pasan a `width: 100%` (regla compartida).

- **Tarjetas COMENTADAS (código íntegro, listo para reactivar):**

| Badge | Servicio | Precio | Link Calendly |
|---|---|---|---|
| Mentoría 1:1 | **Mentoría Personal** | $75 USD | `new-meeting-1` |
| Mentoría 1:1 | **Mentoría Financiera** | $85 USD | `mentoria-1-1-financiera` |
| Paquete · 3 sesiones | **Paquete Reinvención** | $197 USD | `paquete-3-sesiones-reinvencion` |

- Descripciones de las comentadas: Personal → "Para reinvención de vida, identidad, propósito, creencias y toma de decisiones."; Financiera → "Para organizar finanzas personales, presupuesto, deudas, ahorro e inversiones."; Reinvención → "3 sesiones de mentoría personal para construir una transformación real y sostenida."
- **Nota final (visible):** "**Importante:** Todos los servicios son 100% online, en español e inglés, disponibles donde quiera que estés." (mono, centrada).

### 9.6 Sección 03 — Quién Soy (`#about`, luz)
- Header: ghost `03`, kicker "Quién Soy", H2 "Mi historia es **mi método**".
- **Grid 2 col (`1fr 1fr`, gap 80px):**
  - **Izquierda:** `<img src="Image.png" alt="Yoselin Franco">` con `aspect-ratio: 3/4`, `object-fit: cover; object-position: center top`, **`filter: grayscale(100%) contrast(1.06)`**, y tag coral absoluto abajo-izquierda "QUIÉN SOY" (11px uppercase).
  - **Derecha (4 párrafos + cita + CTA + tabla + estado):**
    1. "Soy **Yoselin Franco**. Venezolana. Contadora Pública egresada de la UCAB. Más de 10 años de experiencia en finanzas, incluyendo el Gobierno de Canadá. Vivo en Montreal en una relación multicultural con un canadiense de Quebec que me enseñó que el tiempo libre existe — y yo le enseñé a comer arepas."
    2. "He migrado dos veces — Panamá, Canadá. He empezado de cero en cada país. He sobrevivido un accidente devastador con más de 9 operaciones en un año. He vivido el duelo de perder a mi hermano. He estado endeudada hasta el cuello y he reconstruido mis finanzas desde cero. He pasado por una relación que me borró — y he vuelto a escribirme."
    3. **Cita** (border-left 3px coral, 19px): "Todo eso no es mi historia de fondo. Es mi método."
    4. "Hoy acompaño a personas en transición — especialmente migrantes — a reinventarse personal y financieramente. Trabajo desde la coherencia entre identidad y dinero, porque he comprobado que no puedes transformar tus finanzas sin transformar primero cómo te ves a ti mismo/a. No desde la teoría perfecta. Desde la experiencia real de quien ya lo vivió."
    5. "Mi misión es ayudar a migrantes y personas en transición a reorganizar su dinero, reconectar con su identidad y construir una vida que eligieron — con herramientas concretas, acompañamiento real y sin juicio."
    6. CTA: "¿Listo/a para empezar? **Agenda tu sesión**" (enlace a `#contact`).
- **Tabla de perfil** (`.cert-block` con borde 1px; etiqueta coral mono 11px uppercase 150px / valor 14px):
  - Nombre: Yoselin Franco · Ubicación: Montreal, Canadá · Formación: Contadora Pública — UCAB · Diplomado Coaching con PNL · Experiencia: Más de 10 años en finanzas · Gobierno de Canadá · Idiomas: Español · Inglés · Redes: @soyyoselinfranco (Instagram) + enlace "YouTube: Yoselin Franco | Nunca es tarde" · Email: hola@yoselinfranco.com
- **Estado:** punto verde pulsante + "Actualmente en Montreal, Canadá · Disponible online".

### 9.7 Sección 04 — Cursos y Talleres (`#courses`, oscura) ⚠ ESTADO ACTUAL
- Header: ghost `04`, kicker "Cursos y Talleres", H2 "Aprende a tu **propio ritmo**", desc "Cursos, talleres y masterclases en vivo para reinventarte personal y financieramente."
- **Grilla:** actualmente **1 columna** con **1 sola tarjeta** (ver §10). En normalidad: `repeat(3, 1fr)` → 1 col ≤980.
- **Tarjeta VISIBLE:**

| Badge | Tarjeta | Precio | CTA → destino |
|---|---|---|---|
| En vivo | **Talleres en Vivo** | Desde $27 USD | "Ver fechas y comprar" → abre modal `#talleresModal` |

  - Desc: "Próximas masterclasses en vivo: Saldar tus Deudas, Tu Presupuesto 2027, Crea tus Metas 2027 y Vision Board 2027."
  - Bullets: 90 minutos en vivo · Grabación incluida · Workbook y materiales · Preguntas en tiempo real.
- **Tarjetas COMENTADAS (código íntegro):**

| # | Badge | Tarjeta | Precio | CTA → destino |
|---|---|---|---|---|
| 1 | Curso grabado | **Finanzas Personales desde Cero** | $34 USD | Comprar → Hotmart `U106706696X` |
| 2 | Curso grabado | **Inversiones desde Cero** | $62 USD | Comprar → Hotmart `I107427455H` |
| 3 | Masterclass grabada | **Ahorro Inteligente** | $17 USD | Comprar → Hotmart `O107694194G` |
| 4 | Masterclass grabada | **Elígete** | $17 USD | Comprar → Hotmart `M107826405M` |
| 5 | Combo grabado | **Combo Metas 2027 – 4 Masterclasses** | $79 USD ~~$108~~ (`<s>`) | Comprar → Hotmart `H107827023X` |

- Contenido de bullets de las comentadas:
  - **c1:** Video completo en 4 módulos · Workbook + plantillas imprimibles · Lista de 50 creencias sobre el dinero · Acceso de por vida. Desc: "Curso grabado de 90min. El taller completo con workbook, plantillas y más."
  - **c3:** 4 módulos en video · Workbook + plantillas imprimibles · Guía de inversiones: Canadá, EE.UU. y Latinoamérica · Acceso de por vida. Desc: "Curso grabado de 75 min para empezar a invertir sin importar tu edad o cuánto tienes."
  - **mc1 (Ahorro Inteligente):** Disponible ya · acceso inmediato · Masterclass grabada · Método simple de ahorro · Sin importar cuánto ganes hoy. Desc: "Masterclass grabada para empezar a ahorrar con un método simple, aunque sientas que el dinero no te alcanza."
  - **mc2 (Elígete):** Disponible ya · acceso inmediato · Guía + workbook incluidos · Tarjetas «Soy alguien que…» · Recursos extra. Desc: "Vuelve a ti y crea la identidad que tus metas necesitan. Incluye guía, workbook, tarjetas «Soy alguien que…» y recursos extra."
  - **combo:** Incluye Saldar tus Deudas, Tu Presupuesto 2027, Crea tus Metas 2027 y Vision Board 2027 · En lugar de $108 · ahorras $29 · Incluye todas las grabaciones · Las 4 masterclasses en vivo. Desc: "Las 4 masterclasses en vivo a precio especial. Ahorras $29. Incluye todas las grabaciones."

### 9.8 Modal "Talleres en Vivo" (`#talleresModal`)
- **Overlay:** `rgba(20,14,10,0.6)` + `backdrop-filter: blur(4px)`; modal `max-width: 860px`, `max-height: 86vh`, fondo `--off-white`, `border-radius: 18px`, `padding: 40px 36px`, entrada `translateY(20px) scale(0.98)` → normal.
- **Botón ✕** circular arriba-derecha (38px, fondo blanco → hover coral).
- Título "Talleres en Vivo" (1.9rem) · Subtítulo "Masterclasses en vivo de 90 minutos. Desde $27 USD. Grabación incluida." · Línea coral mono "Compra tu lugar directamente en Hotmart".
- **Tabla** (`table-layout: fixed`, `min-width: 640px`; columnas 18% / 22% / 40% / 20%; thead mono 11px uppercase con borde inferior 2px; filas con hover gold `rgba(223,182,91,0.10)`):

| Masterclass | Fecha | Subtítulo | Link de compra |
|---|---|---|---|
| ~~Saldar tus Deudas~~ **(fila comentada, ver §10)** | Mié 14 oct 2026 · 7:00 PM Montreal · 90 min | Un plan claro para pagar lo que debes y recuperar tu paz financiera. Incluye la grabación. | Comprar en Hotmart → `F107823801K` |
| Tu Presupuesto 2027 | Mié 18 nov 2026 · 7:00 PM Montreal · 90 min | Organiza tu dinero y empieza el año sabiendo a dónde va cada dólar. Incluye la grabación. | Comprar en Hotmart → `H107825578L` |
| Crea tus Metas 2027 | Mié 25 nov 2026 · 7:00 PM Montreal · 90 min | Define lo que quieres lograr y conviértelo en pasos que sí vas a cumplir. Incluye la grabación. | Comprar en Hotmart → `D107825979J` |
| Vision Board 2027 | Sáb 5 dic 2026 · 11:00 AM Montreal · 90 min | Crea en vivo el tablero que te recuerde cada día la vida que estás eligiendo. Incluye la grabación. | Comprar en Hotmart → `R107826208N` |

> **Visibles hoy: 3 de 4 filas.** La fila "Saldar tus Deudas" (fecha ya transcurrida) está **comentada** en el `<tbody>` con los marcadores `<!-- ===== FILA OCULTA TEMPORALMENTE ... ===== ... ===== FIN FILA OCULTA ===== -->`. Sus claves `ws1_name`, `ws1_date`, `ws1_sub` y su link `F107823801K` se conservan intactos (§10).

- Fecha: mono 12px coral weight 600. Link: mono 12px coral con `text-decoration: underline` (`text-underline-offset: 3px`), hover `--black`.
- **Nota inferior:** "Todas las masterclasses son en vivo, en español y la grabación queda incluida." (mono 11px).
- Cierra con ✕, clic en overlay o `Escape` (ver §7.5).

### 9.9 Sección 05 — Testimonios (`#testimonials`, luz)
- Header: ghost `05`, kicker "Testimonios", H2 "Resultados **reales**", desc "Historias de personas que decidieron reinventarse y dieron el primer paso."
- **Grilla 2×2** (`.quotes`, `gap: 24px`) con 4 tarjetas blancas: 5 estrellas coral (`★★★★★`), cita en español **sin traducir** (clampeada a 4 líneas con `-webkit-line-clamp`), botón "Ver más"/"Ver menos" en coral, y pie con autor (coral bold) + rol (gris 12px):
  1. **Jose Luis Solano** — Taller Inversiones desde Cero
  2. **Mariana Leon** — Mentoría Financiera 1:1
  3. **Genesis Hernández** — Taller Finanzas desde Cero
  4. **Eliana Alvarez** — Mentoría Financiera 1:1
- CTA final centrado (margin-top 48px): "Deja tu reseña en Google" → `https://g.page/r/Ca3kal9hBJOuEBI/review`.

### 9.10 Sección 06 — Contacto (`#contact`, oscura)
- Header: ghost `06`, kicker "Contacto · Agenda", H2 "Da el primer paso hacia tu **reinvención**".
- **Tarjeta única "Cómo funcionan las sesiones"** (fondo `#4A3728`, padding 36px, borde 1px): desc "Mentoría y coaching personal 100% online. Aquí te cuento cómo es el proceso." + lista con iconos `›`:
  - Sesiones vía Google Meet · Disponible donde quiera que estés · En español e inglés, con calidez y sin filtros · Pago con tarjeta vía Stripe
  - Botón `.btn line` "Ver servicios y precios" → `#services` (⚠ ver bug §11.3).
- **Panel "Política de sesiones"** (título con "sesiones" en coral), `ul` a 2 columnas con `✓` coral:
  - Reagendamiento: mínimo 48 horas de anticipación
  - Cancelación: mínimo 24 horas de anticipación
  - Espera máxima: 15 minutos. Pasado ese tiempo la sesión se considera realizada
  - Reembolsos: no se realizan una vez agendada la sesión
  - Alcance: mentoría y coaching personal. No reemplaza atención psicológica profesional
  - Nota: "Tus datos y conversaciones son tratados con confidencialidad." (itálica)

### 9.11 Footer
- Fondo `--black`, borde superior 1px, `padding: 56px 40px 32px`.
- **Grid 3 col (`1.4fr 1fr 1fr`, gap 48px):**
  1. Marca "Yoselin." (18px bold, punto coral) + desc "Coach personal y mentora financiera para migrantes y personas que empiezan de nuevo. Desde la experiencia real, no desde la teoría perfecta."
  2. **Explora:** Quién Soy (`#about`) · Servicios (`#services`) · Cursos y Talleres (`#courses`) · Testimonios (`#testimonials`).
  3. **Contacto:** hola@yoselinfranco.com (mailto) · Instagram · @soyyoselinfranco · YouTube · Nunca es tarde.
- **Copyright** (borde superior, flex space-between): "© [año dinámico] Yoselin Franco · yoselinfranco.com" + lema coral ""Nunca es tarde para reinventarte."".

---

## 10. Estado actual: código oculto y cómo restaurarlo

> **Contexto (25 oct 2026):** se publicó una versión "reducida" de la landing. **No se borró ningún código**: las tarjetas están envueltas en comentarios HTML, las grillas forzadas a 1 columna, los precios y el CTA de la cabecera comentados por separado, y una fila del modal oculta. Las claves i18n siguen en el diccionario.

### 10.1 Qué está oculto hoy

| Sección | Visible | Comentado |
|---|---|---|
| **Cabecera · nav** | Logo · 5 links · selector ES/EN/FR · hamburguesa | CTA **"Agenda tu sesión"** (`nav_book`) |
| **02 · Mentorías y paquetes** | "Programa Ordena tu Dinero" (sin precio) | Mentoría Personal $75 · Mentoría Financiera $85 · Paquete Reinvención $197 |
| **04 · Cursos y Talleres** | "Talleres en Vivo" | Finanzas Personales $34 · Inversiones $62 · Ahorro Inteligente $17 · Elígete $17 · Combo Metas 2027 $79 |
| **Modal · Talleres en Vivo** | 3 filas: Tu Presupuesto 2027 · Crea tus Metas 2027 · Vision Board 2027 | Fila **"Saldar tus Deudas"** (14 oct 2026) |

### 10.2 Marcadores usados (para localizarlos con búsqueda)

- **Cabecera (CTA):** dentro de `<nav id="nav">`, tras el `<button class="menu-toggle">`, comentario `<!-- CTA "Agenda tu sesión" ELIMINADO DE LA CABECERA — oculto temporalmente ...` que envuelve el `<a ... class="btn dark nav-cta" data-i18n="nav_book">` y cierra con `-->` justo antes de `</nav>`.
- **Servicios:** el comentario arranca justo después de `<div class="services-grid reveal">` con la cabecera `<!-- ================ ... TARJETAS OCULTAS TEMPORALMENTE ...` y termina con `===== FIN TARJETAS OCULTAS ===== -->` antes de la tarjeta visible.
- **Cursos:** idéntico patrón dentro de `<div class="courses-grid reveal">`, cerrando antes de la tarjeta "Talleres en Vivo".
- **Precio oculto:** dentro de la tarjeta visible de servicios, comentario propio `<!-- Precio oculto temporalmente ... -->` que envuelve `<div class="price">$220 <small>USD</small></div>`.
- **Modal (fila de masterclass):** dentro del `<tbody>` de `#talleresModal`, comentario `<!-- ===== FILA OCULTA TEMPORALMENTE ... =====` que envuelve el `<tr>` de "Saldar tus Deudas" y cierra con `===== FIN FILA OCULTA ===== -->` antes de la fila "Tu Presupuesto 2027".
- **CSS (3 puntos):** `.services-grid` y `.courses-grid` con `grid-template-columns: 1fr` + comentario `/* TEMPORAL ... */`; media query ≤1280px con `.services-grid { grid-template-columns: 1fr; }`. El comentario `/* CTA "Agenda tu sesión": el botón está COMENTADO en el HTML ... */` documenta el estado del CTA de nav.

### 10.3 Procedimiento de restauración (paso a paso)

**Reactivar el CTA de la cabecera ("Agenda tu sesión"):**
1. En `<nav id="nav">`, buscar `ELIMINADO DE LA CABECERA`.
2. Eliminar el `<!-- CTA "Agenda tu sesión" ELIMINADO ...` de apertura (3 líneas de cabecera) y el `-->` de cierre, dejando el `<a class="btn dark nav-cta">` dentro del nav.
3. Verificar: el botón debe aparecer a la derecha del selector de idiomas; en ≤700px debe ocultarse (regla `.nav-cta { display: none; }` intacta).

**Reactivar una tarjeta:**
1. Buscar `FIN TARJETAS OCULTAS` en la sección correspondiente.
2. Eliminar el `<!-- ...` de apertura (cabecera completa) y el `===== FIN TARJETAS OCULTAS ===== -->` de cierre, dejando solo las tarjetas deseadas fuera del comentario. *(Si se reactivan todas, no debe quedar ningún comentario en la grilla.)*
3. Verificar que el balance `<!--` / `-->` del archivo siga igual (herramienta: contar ocurrencias).

**Mostrar el precio de "Programa Ordena tu Dinero":**
1. Eliminar el comentario `<!-- Precio oculto temporalmente ... -->` que envuelve el `<div class="price">$220 ...`.

**Reactivar la fila del modal ("Saldar tus Deudas"):**
1. En `#talleresModal`, buscar `FIN FILA OCULTA`.
2. Eliminar el `<!-- ===== FILA OCULTA TEMPORALMENTE ...` de apertura y el `===== FIN FILA OCULTA ===== -->` de cierre, dejando el `<tr>` dentro del `<tbody>`.
3. Si la fecha ya no aplica, actualizar `ws1_date` / `ws1_sub` en los tres idiomas antes de reactivarla.

**Restaurar las columnas de las grillas:**
1. `.services-grid` → `grid-template-columns: repeat(4, 1fr);` (y ≤1280px → `repeat(2, 1fr)`).
2. `.courses-grid` → `grid-template-columns: repeat(3, 1fr);`.
3. Borrar los comentarios `/* TEMPORAL ... */` asociados.

**Verificación final:** la cabecera debe mostrar el CTA "Agenda tu sesión" (oculto en ≤700px), en desktop Servicios debe mostrar 4 tarjetas con precios, Cursos 6 tarjetas y el modal de talleres sus 4 filas; en ≤980px ambas grillas a 1 columna.

---

## 11. Limitaciones y deudas técnicas conocidas

> Puntos detectados en la auditoría del 25 oct 2026. **No corregir silenciosamente**: registrar en §15 si se arreglan.

| # | Problema | Detalle / ubicación | Corrección sugerida |
|---|---|---|---|
| 1 | **YouTube en `http://`** | 3 enlaces: columna social del hero, tabla de perfil (about) y footer → `http://www.youtube.com/@soyyoselinfranco` | Cambiar a `https://` |
| 2 | **`rel="noopener"` sin `noreferrer`** | Los 21 enlaces externos con `target="_blank"` usan solo `noopener` | Añadir `noreferrer` si se requiere privacidad del `Referer` |
| 3 | **Botón de contacto sin estilo** | El HTML usa `class="btn line"` pero el CSS define **`.btn-line`** (con guion): no hay regla `.btn.line`, así que el botón "Ver servicios y precios" hereda texto marrón oscuro sobre fondo oscuro y borde transparente | Cambiar el HTML a `class="btn btn-line"` o añadir la regla `.btn.line` |
| 4 | **Indicador de nav nunca marca "Quién Soy"** | `sections = ['hero','about','services',...]` no sigue el orden visual (services 02 va antes que about 03); al evaluar `services` después que `about`, el indicador resalta "Servicios" cuando se está en About | Reordenar el array al orden visual: `['hero','value','services','about','courses','testimonials','contact']` (agregando `value` y renombrando `#value` si se quiere link) |
| 5 | **Sin favicon ni Open Graph** | No hay `<link rel="icon">` ni metas `og:*` / `twitter:*` | Añadir icono + OG para compartir en redes |
| 6 | **Fonts residuales** | `Dancing Script` y `Playfair Display` se descargan sin usarse | Quitarlas del `<link>` de Google Fonts (ahorra descarga) |
| 7 | **Sin CSP** | Archivo único con `<style>`/`<script>` inline | Si se despliega en Netlify/Cloudflare/Vercel, definir CSP por cabeceras HTTP |
| 8 | **`#value` sin link en nav** | La sección 01 no tiene entrada en la navegación ni en el array de indicadores | Opcional: añadir link "Por qué" o ignorar por diseño |
| 9 | **`c2_desc` anuncia un taller ya ocurrido** | La tarjeta visible "Talleres en Vivo" (`c2_desc` en es/en/fr) sigue nombrando "Saldar tus Deudas" entre las próximas masterclasses, pero su fila del modal está comentada (fecha 14 oct 2026 ya transcurrida). Las claves `ws1_*` y el link `F107823801K` permanecen en el diccionario | Decisión pendiente: actualizar `c2_desc` en los 3 idiomas quitando "Saldar tus Deudas", o reactivar la fila con una nueva fecha |

---

## 12. Enlaces externos

| Tipo | Destino |
|---|---|
| Agendar sesión (4 variantes) | `calendly.com/hola-yoselinfranco/` → `new-meeting-1`, `mentoria-1-1-financiera`, `paquete-3-sesiones-reinvencion`, `paquete-reinvencion-3-sesiones-` |
| Cursos grabados (Hotmart) | `U106706696X` (Finanzas Personales), `I107427455H` (Inversiones), `O107694194G` (Ahorro Inteligente), `M107826405M` (Elígete), `H107827023X` (Combo Metas 2027) |
| Masterclasses en vivo (Hotmart) | `F107823801K` (Saldar tus Deudas), `H107825578L` (Tu Presupuesto 2027), `D107825979J` (Crea tus Metas 2027), `R107826208N` (Vision Board 2027) |
| Instagram | `instagram.com/soyyoselinfranco` |
| YouTube | `youtube.com/@soyyoselinfranco` (⚠ aún en `http://` en 3 lugares, ver §11.1) |
| Email | `hola@yoselinfranco.com` (mailto) |
| Reseñas Google | `g.page/r/Ca3kal9hBJOuEBI/review` |
| Dominio | `yoselinfranco.com` |

**Seguridad de enlaces:** todo enlace externo con `target="_blank"` lleva `rel="noopener"` (ver §11.2 sobre `noreferrer`); los `mailto:` y anclajes internos no lo requieren. El flujo de compra va directo a Hotmart (checkout propio del producto), no por DM en Instagram.

---

## 13. Accesibilidad y metadatos

- `aria-label` en botones (✕ del modal, hamburguesa), `role="dialog"` + `aria-hidden` en el modal, `alt="Yoselin Franco"` en la foto, `aria-hidden` en SVGs decorativos y en capas decorativas del hero.
- `lang="es"` inicial, actualizado por `applyLang`; `<html>` con `scroll-behavior: smooth`.
- SEO: `<title>` y `<meta name="description">` en español (ambos se reescriben con `meta_title` al cambiar idioma).
- **No hay CSP** (archivo único con `<style>`/`<script>` inline); ver §11.7.

---

## 14. Checklist de replicación y QA

1. Un solo `index.html`; CSS en `<style>` del head, JS en `<script>` final del body.
2. Copiar verbatim: `:root` (§4.3), Google Fonts (§4.1), reset base (§4.4), meta head (§1.3).
3. Reproducir el orden de bloques del §1.2 y las secciones numeradas 01–06 + intro + marquee + splash + modal.
4. Mantener el sistema `data-i18n` con **206 claves idénticas** en `es`/`en`/`fr` (el contenido ES es el listado en §9; EN/FR son traducciones equivalentes dentro del mismo diccionario).
5. Respetar tokens: radios (999px pills / 18px modal / 0 tarjetas), grillas hairline de 1px, curva `cubic-bezier(0.16,1,0.3,1)`, prefijo `// ` en kickers, números fantasma con stroke.
6. Verificar comportamientos: splash ≤4.5 s, cursor lerp 0.22, nav indicador/ocultar, reveal con IO 0.12, modal con 3 formas de cierre, toggle de testimonios, año dinámico.
7. Verificar breakpoints: 1280 / 980 / 700 / 640 / 480.
8. Assets: solo `Image.png` (grayscale 3:4) y los enlaces externos de la §12.
9. **Estado de ocultamiento (§10):** confirmar que la **cabecera no muestra el CTA** "Agenda tu sesión", Servicios muestra solo "Programa Ordena tu Dinero" **sin precio**, Cursos solo "Talleres en Vivo" y el modal **3 filas** (sin "Saldar tus Deudas"); balance `<!--` = `-->` en todo el archivo.
10. **Consistencia doc↔código:** cualquier cambio en `index.html` debe reflejarse aquí (§9–§11 y §15).

---

## 15. Historial de cambios aplicados

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
- **Seguridad:** `rel="noopener"` en los enlaces externos con `target="_blank"` (el `noreferrer` originalmente previsto **no llegó a aplicarse**, ver §11.2); YouTube pendiente de `https://` (§11.1).
- **Nota:** sin CSP estricta por ser landing estática de un solo archivo con código inline; recomendar CSP por cabeceras al desplegar en hosting con soporte HTTP.

### 25 oct 2026 — Versión reducida + guía v2

1. **Sección 02 — Mentorías y paquetes:**
   - Comentado el código de 3 de las 4 tarjetas de la grilla: **Mentoría Personal** ($75), **Mentoría Financiera** ($85) y **Paquete Reinvención** ($197). Queda visible únicamente la cuarta tarjeta.
   - Comentado el bloque de **precio** (`$220 USD`) de la tarjeta visible.
   - **Renombre:** "Paquete Financiero" → **"Programa Ordena tu Dinero"** en el `<h3>` del HTML y en la clave `serv_t5` de los tres idiomas (ES/EN/FR — en EN y FR se mantiene el nombre en español, decisión de marca). También se actualizó la clave legada `phase2` en los tres idiomas.
   - `.services-grid` forzada a **1 columna** (base + media query ≤1280px) con comentario `/* TEMPORAL ... */`.
2. **Sección 04 — Aprende a tu propio ritmo:**
   - Comentado el código de **5 de las 6 tarjetas** (Finanzas Personales, Inversiones, Ahorro Inteligente, Elígete y Combo Metas 2027). Queda visible solo **"Talleres en Vivo"**.
   - `.courses-grid` forzada a **1 columna** con comentario `/* TEMPORAL ... */`.
3. **Integridad:** las claves `data-i18n` de las tarjetas ocultas **se conservaron** en el HTML (dentro del comentario) y en el diccionario `translations`; no se eliminó ningún enlace de Calendly ni de Hotmart.
4. **Documento:** reescrito como **guía de construcción v2** (§0–§15): metodología por fases, formatos y convenciones, recetas de edición, estado actual y restauración (§10), limitaciones/deudas técnicas detectadas en auditoría (§11) y checklist ampliado.
5. **Verificación (estado al cierre de la primera tanda):** balance de comentarios `<!--`/`-->` = 16/16; 0 ocurrencias de "Paquete Financiero"; 8 ocurrencias del nombre del programa (HTML + 3 idiomas × 2 claves + comentario CSS).

### 25 oct 2026 (tanda 2) — Renombre, CTA unificado y fila de modal oculta

6. **Renombre de mayúscula:** "Programa Ordena **Tu** Dinero" → "Programa Ordena **tu** Dinero" en las 8 apariciones de `index.html` (`<h3>`, `serv_t5` ×3, `phase2` ×3 y comentario CSS) y en las 8 del presente documento.
7. **CTA "Agenda tu sesión" unificado:** el botón de la **navegación** pasó de `class="nav-cta"` (mono 10.5px uppercase, padding 9×16) a **`class="btn dark nav-cta"`** → mismo estilo, tamaño y proporción que "Ver fechas y comprar" (coral, 13px bold, padding 13×26, pill 999px, hover `#e58278` + `translateY(-2px)`). Se eliminaron las reglas visuales de `.nav-cta` (se conserva la clase solo como gancho para el `display:none` de ≤700px). El CTA de la **sección intro** también pasó de `.intro-cta.solid` a **`btn dark`**. El de la tarjeta de servicios ya usaba `btn dark`.
8. **Modal — fila "Saldar tus Deudas" oculta:** comentado el `<tr>` completo (fecha 14 oct 2026, ya transcurrida) con marcadores `FILA OCULTA TEMPORALMENTE` / `FIN FILA OCULTA` dentro del `<tbody>`. Visible 3 de 4 filas; claves `ws1_*` y link `F107823801K` conservados.
9. **Pendiente documentado:** `c2_desc` (tarjeta "Talleres en Vivo") aún anuncia "Saldar tus Deudas" — ver §11.9 (decisión sobre actualizar texto en es/en/fr o reactivar fila con nueva fecha).
10. **Verificación (cierre tanda 2):** balance `<!--`/`-->` = **17/17**; 0 "Programa Ordena Tu Dinero"; 8 "Programa Ordena tu Dinero"; `index.html` = 116.668 bytes / 1.612 líneas.

### 25 oct 2026 (tanda 3) — CTA de cabecera eliminado

11. **Cabecera sin CTA:** el botón **"Agenda tu sesión"** de la navegación (`<a class="btn dark nav-cta" data-i18n="nav_book">`) quedó **comentado** en el HTML, tras el botón hamburguesa y antes de `</nav>`, con la cabecera `<!-- CTA "Agenda tu sesión" ELIMINADO DE LA CABECERA — oculto temporalmente ... -->`. No se borró nada: el enlace completo (Calendly `new-meeting-1`) y su clave `nav_book` siguen intactos dentro del comentario y en el diccionario i18n.
12. **CSS:** se actualizó el comentario que precede a `.menu-toggle` para indicar que el botón está comentado en el HTML; se **conserva** la clase `nav-cta` en el `<a>` y la regla `.nav-cta { display: none; }` del media query ≤700px, de modo que al restaurarlo se oculta correctamente en móvil.
13. **Doc:** cabecera actualizada (estado actual + métricas), §9.1 (CTA marcado como comentado), §10.1/§10.2/§10.3 (fila de nav en la tabla, marcador de búsqueda y **procedimiento de restauración**), §14 (checklist) y §15 (este historial).
14. **Verificación (cierre tanda 3):** balance `<!--`/`-->` = **18/18**; `data-i18n="nav_book"` fuera de comentarios = **0** (no se renderiza); `index.html` = 117.117 bytes / 1.618 líneas.

### 25 oct 2026 (tanda 4) — CTA de "Programa Ordena tu Dinero" igualado al de "Talleres en Vivo"

15. **Problema:** el botón "Agenda tu sesión" de la tarjeta visible "Programa Ordena tu Dinero" ya usaba `btn dark` (mismo color/tipografía/padding) pero **se estiraba a todo el ancho de la tarjeta** en forma de barra, porque `.service-card` es un flex column con `align-items` por defecto `stretch`. El botón "Ver fechas y comprar", en cambio, es hijo de un `.foot` flex row → píldora compacta del ancho de su texto.
16. **Solución (solo CSS, sin tocar HTML):** `.service-card .btn { margin-top: auto; align-self: flex-start; text-align: center; }` — añadido `align-self: flex-start` (con comentario explicativo encima). Ahora el botón es una píldora compacta alineada a la izquierda, idéntica a la de Talleres en Vivo. Aplica también a las 3 tarjetas de servicios comentadas al reactivarlas (misma regla compartida). En ≤640px la regla compartida `.service-card .btn, .course-card .btn { width: 100% }` mantiene ambos a ancho completo en móvil.
17. **Decisión registrada:** se eligió **solo igualar el botón** (no replicar el `<div class="foot">` con `border-top` de la tarjeta de cursos) — decisión del usuario.
18. **Verificación (cierre tanda 4):** balance `<!--`/`-->` = **18/18**; `index.html` = 117.415 bytes / 1.621 líneas.
