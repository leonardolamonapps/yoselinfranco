# Landing Page — Yoselin Franco · Coach Personal y Mentora Financiera

**Documento descriptivo completo**

- **Archivo fuente:** `index.html`
- **Dominio:** yoselinfranco.com
- **Idiomas:** Español (ES) · Inglés (EN) · Francés (FR) — selector de idiomas en la navegación
- **Tagline principal:** "Nunca es tarde para reinventarte."

---

## 1. Aspectos generales del sitio

### 1.1 Identidad visual
La paleta de colores (variables CSS `:root`) es la que define toda la estética:

| Variable | Color | Uso |
|---|---|---|
| `--off-white` | `#E6D9CF` | Fondo principal (nude claro) |
| `--black` | `#4A3728` | Texto principal / headers oscuros |
| `--accent` | `#DD675D` | CTAs, títulos destacados, botones (coral) |
| `--gold` | `#DFB65B` | Acentos, líneas decorativas (dorado) |
| `--white` | `#ffffff` | Fondos de tarjetas |
| `--mid` | `#CAB19F` | Elementos secundarios (nude medio) |
| `--grey-brown` | `#7A6255` | Texto secundario |

### 1.2 Tipografías
- **Texto principal:** `Space Grotesk` (400–700)
- **Etiquetas / kickers / fechas:** `DM Mono` monospace (400, 500, 700)
- También se cargan `Dancing Script` y `Playfair Display` vía Google Fonts.

### 1.3 Funcionalidades técnicas implementadas
- **Interfaz trilingüe (ES / EN / FR):** selector de idioma en la barra de navegación que cambia todos los textos con `data-i18n` y también el idioma de la página (`lang`).
- **Cursor personalizado:** el cursor del mouse se sustituye por un punto coral con anillo que se agranda sobre enlaces y botones (solo en dispositivos con mouse; se oculta en táctiles).
- **Pantalla de carga (splash):** breve animación que muestra el nombre y una barra de progreso antes de la página.
- **Animaciones de aparición (reveal):** los bloques entran en escena al hacer scroll con retardo escalonado (`d1`, `d2`...).
- **Scroll suave** entre secciones (ancoraje).
- **Menú de hamburguesa** en móvil.
- **Indicador de sección activa** en la navegación.

---

## 2. Estructura de la página (recorrido)

La página es una landing de una sola página con **7 bloques + navegación + pie**, numerados 01–06 en las secciones principales.

1. Navegación (menú superior fijo)
2. Hero (Inicio)
3. Sección 01 — "Por qué Yoselin" (tres razones)
4. Sección 02 — Servicios (Mentorías y paquetes)
5. Sección 03 — Quién Soy (historia)
6. Sección 04 — Cursos y Talleres (+ modal de talleres)
7. Sección 05 — Testimonios
8. Sección 06 — Contacto / Agenda
9. Pie de página (footer)

---

## 3. Detalle por sección

### 3.1 Navegación (Nav)
Barra superior fija con:
- **Logo:** "Yoselin." a la izquierda, enlaza a la parte superior.
- **Enlaces de navegación:** Inicio · Quién Soy · Servicios · Cursos · Testimonios.
- **Selector de idiomas (ES / EN / FR):** botones en píldora con indicador deslizante.
- **Botón CTA principal:** "Agenda tu sesión" (enlaza a Calendly, nueva pestaña).
- **Menú hamburguesa ☰** para vista móvil.

### 3.2 Hero (Inicio)
- **Fondo:** fotografía de Yoselin con viñeta.
- **Redes sociales:** iconos SVG de Instagram, YouTube y Email (correo) con enlaces.
- **Kicker / etiqueta:** "Coach Personal y Mentora Financiera" (con barra `/` decorativa).
- **Nombre en grande:** "Yoselin Franco" (título H1).
- **Indicador de scroll:** "Scroll ↓".

### 3.3 Bloque Intro (justo debajo del hero, sin número)
- **Frase principal:** "Nunca es tarde para **reinventarte.**"
- **Párrafo:** "Acompaño a personas en transición a reinventarse personal y financieramente — desde la experiencia real, no desde la teoría perfecta."
- **Dos botones:** "Agenda tu sesión" (sólido) y "Conoce mi historia" (enlace).
- **Estadísticas (3):**
  - **2** → Países donde he vuelto a empezar
  - **+ 10** → Años en finanzas
  - **+ 30K** → Personas inspiradas
- **Marquee (cinta animada):** texto corrido repetido con frases destacadas ("Finanzas que funcionan", "Reinvención desde la experiencia", "Acompañamiento en español e inglés", "Mentoría Personal", "Mentoría Financiera", "Finanzas Personales desde Cero").

### 3.4 Sección 01 — "Por qué Yoselin" (luz)
- **Número fantasma:** 01
- **Etiqueta:** "Por qué Yoselin"
- **Título:** "Tres razones para **empezar**"
- **Lista de tres razones numeradas (01, 02, 03):**
  1. "Finanzas que **funcionan**"
  2. "Reinvención desde la **experiencia**"
  3. "Acompañamiento **en español e inglés**"

### 3.5 Sección 02 — Servicios: "Mentorías y paquetes" (fondo oscuro)
- **Número fantasma:** 02
- **Etiqueta:** "Qué ofrezco"
- **Título:** "Mentorías y **paquetes**"
- **Subtítulo:** "100% online vía Google Meet, en español e inglés, disponible donde quiera que estés."
- **Grilla de 4 tarjetas de servicio**, cada una con badge, título, precio en USD, descripción, lista de "incluye" y botón CTA:

| Servicio | Precio | Incluye | CTA / Link |
|---|---|---|---|
| **Mentoría Personal** (Mentoría 1:1) | $75 USD | · 60 min Google Meet · Sesión grabada · Plan de acción al cierre · Seguimiento WhatsApp 48hs | "Agenda tu sesión" → Calendly `new-meeting-1` |
| **Mentoría Financiera** (Mentoría 1:1) | $85 USD | · 60 min Google Meet · Análisis de situación real · Plan financiero personalizado · Plantillas de presupuesto | "Agenda tu sesión" → Calendly `mentoria-1-1-financiera` |
| **Paquete Reinvención** (3 sesiones) | $197 USD | · 3 sesiones de 60 min · Plan de acción progresivo · Seguimiento entre sesiones · Materiales incluidos | "Agenda tu sesión" → Calendly `paquete-3-sesiones-reinvencion` |
| **Paquete Financiero** (3 sesiones) | $220 USD | · 3 sesiones de 60 min · Análisis completo de presupuesto · Plan financiero a 6 meses · Plantillas y guías | "Agenda tu sesión" → Calendly `paquete-reinvencion-3-sesiones-` |

- **Nota al cierre (destacada):** "**Importante:** Todos los servicios son 100% online, en español e inglés, disponibles donde quiera que estés."

> **Compatibilidad con el brief:** el brief describe 4 productos de mentoría (Personal 1:1, Financiera 1:1, Paquete Reinvención, Paquete Financiero) con los mismos precios e inclusiones. La landing los replica exactamente.

### 3.6 Sección 03 — Quién Soy: "Mi historia es mi método" (luz)
- **Número fantasma:** 03
- **Etiqueta:** "Quién Soy"
- **Título:** "Mi historia es **mi método**"
- **Layout:** foto (imagen `Gemini_Generated_Image_...png`) con etiqueta "Quién Soy" + bloque de texto.
- **Párrafos de historia:**
  1. "Soy **Yoselin Franco**. Venezolana. Contadora Pública egresada de la UCAB. Más de 10 años en finanzas, incluyendo el Gobierno de Canadá. Vivo en Montreal en una relación multicultural con un canadiense de Quebec que me enseñó que el tiempo libre existe — y yo le enseñé a comer arepas."
  2. "He migrado dos veces — Panamá, Canadá. He empezado de cero en cada país. He sobrevivido un accidente devastador con más de 9 operaciones en un año. He vivido el duelo de perder a mi hermano. He estado endeudada hasta el cuello y he reconstruido mis finanzas desde cero. He pasado por una relación que me borró — y he vuelto a escribirme."
  3. **Cita destacada:** "Todo eso no es mi historia de fondo. Es mi método."
  4. "Hoy acompaño a personas en transición — especialmente migrantes — a reinventarse personal y financieramente. Trabajo desde la coherencia entre identidad y dinero, porque he comprobado que no puedes transformar tus finanzas sin transformar primero cómo te ves a ti mismo/a. No desde la teoría perfecta. Desde la experiencia real de quien ya lo vivió."
  5. "Mi misión es ayudar a migrantes y personas en transición a reorganizar su dinero, reconectar con su identidad y construir una vida que eligieron — con herramientas concretas, acompañamiento real y sin juicio."
  6. **Llamada a la acción:** "¿Listo/a para empezar? Agenda tu sesión" (enlaza a la sección de Contacto 06).
- **Tabla de perfil (credenciales):**
  - Nombre: Yoselin Franco
  - Ubicación: Montreal, Canadá
  - Formación: Contadora Pública — UCAB · Diplomado Coaching con PNL
  - Experiencia: Más de 10 años en finanzas · Gobierno de Canadá
  - Idiomas: Español · Inglés
  - Redes: @soyyoselinfranco (Instagram) · YouTube: Yoselin Franco | Nunca es tarde (enlace)
  - Email: hola@yoselinfranco.com
- **Indicador de disponibilidad:** punto verde y texto "Actualmente en Montreal, Canadá · Disponible online".

### 3.7 Sección 04 — Cursos y Talleres: "Aprende a tu propio ritmo" (fondo oscuro)
- **Número fantasma:** 04
- **Etiqueta:** "Cursos y Talleres"
- **Título:** "Aprende a tu **propio ritmo**"
- **Subtítulo:** "Cursos, talleres y masterclases en vivo para reinventarte personal y financieramente"
- **Grilla de 3 tarjetas de curso:**

| Curso | Tipo | Precio | Incluye | CTA |
|---|---|---|---|---|
| **Finanzas Personales desde Cero** | Curso grabado | $34 USD | · Video en 4 módulos · Workbook + plantillas · Lista de 50 creencias sobre el dinero · Acceso de por vida | "Comprar" → Hotmart `U106706696X` |
| **Inversiones desde Cero** | Curso grabado | $62 USD | · 4 módulos en video · Workbook + plantillas · Guía de inversiones: Canadá, EE.UU. y Latinoamérica · Acceso de por vida | "Comprar" → Hotmart `I107427455H` |
| **Talleres en Vivo** | En vivo | Desde $27 USD | · 60–90 min en vivo · Grabación incluida · Workbook y materiales · Preguntas en tiempo real | "Agenda tu taller" → abre modal |

- La tarjeta "Talleres en Vivo" abre un **modal** (ventana emergente) con la programación.

#### Modal de Talleres en Vivo
Al hacer clic en "Agenda tu taller" se abre un modal con:
- Título: "Talleres en Vivo"
- Subtítulo: "Masterclasses en vivo de 60 a 90 minutos. Desde $27 USD."
- Aviso: "Agenda tu cupo escribiendo la palabra clave por DM en Instagram."
- **Tabla programación** (columnas: Masterclass / Fecha / Subtítulo / Palabra clave):

| Masterclass | Fecha | Subtítulo | Palabra clave |
|---|---|---|---|
| Ahorro Inteligente | Sáb 12 sep 2026 · 11:00 AM Montreal | Cómo empezar a ahorrar aunque sientas que no te alcanza | Comenta **AHORRO** |
| Elígete | Sáb 26 sep 2026 | Cómo construir la identidad que tus metas necesitan | Comenta **ELIGETE** |
| Sal de tus Deudas | Sáb 17 oct 2026 | Un plan real para liberarte de lo que te pesa | Comenta **DEUDA** |
| Crea Metas y Síguelas | Sáb 14 nov 2026 | Cómo convertir lo que quieres en un plan que funciona | Comenta **META** |
| Tu Presupuesto 2027 | Sáb 28 nov 2026 | Crea tu plan financiero para el próximo año paso a paso | Comenta **PRESUPUESTO** |
| Tu Visión Board 2027 | Sáb 5 dic 2026 | Cierra el año con intención y diseña tu 2027 con propósito | Comenta **VISIÓN** |

- **Nota:** "Todos los talleres son en vivo, en español y quedan grabados."
- El modal se cierra con el botón ✕, clic fuera de la ventana o la tecla Escape.

### 3.8 Sección 05 — Testimonios: "Resultados reales" (luz)
- **Número fantasma:** 05
- **Etiqueta:** "Testimonios"
- **Título:** "Resultados **reales**"
- **Subtítulo:** "Historias de personas que decidieron reinventarse y dieron el primer paso."
- **Grilla 2×2 de 4 reseñas** (5 estrellas + cita textual + nombre + rol). Cada tarjeta muestra la cita recortada a 4 líneas con el botón **"Ver más"** para expandirla al texto completo y **"Ver menos"** para volver a colapsarla. Todas las tarjetas tienen el mismo tamaño.

| Autor | Rol | Servicio del que opina |
|---|---|---|
| Jose Luis Solano | Taller Inversiones desde Cero | Reseña sobre el taller de inversiones para principiantes |
| Mariana Leon | Mentoría Financiera 1:1 | Reseña sobre la transformación emocional y financiera tras la mentoría |
| Genesis Hernández | Taller Finanzas desde Cero | Reseña sobre el taller de finanzas: antes y después |
| Eliana Alvarez | Mentoría Financiera 1:1 | Reseña sobre el acompañamiento en las 3 sesiones |

> Los textos de los testimonios son **textuales** (tomados de reseñas reales de Google) y se mantienen **en español** en los tres idiomas del sitio; el contenido de la cita no se traduce.

- **Botón final:** "Deja tu reseña en Google" → enlaza a la página de reseñas de Google Business (`g.page`).

### 3.9 Sección 06 — Contacto / Agenda: "Da el primer paso" (fondo claro)
- **Número fantasma:** 06
- **Etiqueta:** "Contacto · Agenda"
- **Título:** "Da el primer paso hacia tu **reinvención**"
- **Tarjeta única: "Cómo funcionan las sesiones"**
  - Descripción: "Mentoría y coaching personal 100% online. Aquí te cuento cómo es el proceso."
  - Lista:
    - Sesiones vía Google Meet
    - Disponible donde quiera que estés
    - En español e inglés, con calidez y sin filtros
    - Pago con tarjeta vía Stripe
  - Botón: "Ver servicios y precios" → enlaza a la sección de Servicios (02).
- **Panel: "Política de sesiones"** (con "sesiones" en color decorativo):
  - Reagendamiento: mínimo 48 horas de anticipación
  - Cancelación: mínimo 24 horas de anticipación
  - Espera máxima: 15 minutos. Pasado ese tiempo la sesión se considera realizada
  - Reembolsos: no se realizan una vez agendada la sesión
  - Alcance: mentoría y coaching personal. No reemplaza atención psicológica profesional
  - Nota: "Tus datos y conversaciones son tratados con confidencialidad."

> **Cambios recientes aplicados:** se eliminó el subtítulo anterior y la tarjeta "Agenda tu sesión" (con sus datos de Calendly, email, Instagram, YouTube y el botón "Agendar en Calendly"). Ahora solo queda la tarjeta "Cómo funcionan las sesiones", alineada a todo el ancho de la landing.

### 3.10 Pie de página (Footer)
- **Columna 1 — Marca y lema:** logo "Yoselin." + descripción: "Coach personal y mentora financiera para migrantes y personas que empiezan de nuevo. Desde la experiencia real, no desde la teoría perfecta."
- **Columna 2 — "Explora":** Quién Soy · Servicios · Cursos y Talleres · Testimonios.
- **Columna 3 — "Contacto":** hola@yoselinfranco.com (mailto) · Instagram · @soyyoselinfranco · YouTube · Nunca es tarde.
- **Zona de copyright:**
  - "© [año] Yoselin Franco · yoselinfranco.com" (el año se genera automáticamente con JS).
  - Lema: "Nunca es tarde para reinventarte."

---

## 4. Tecnología y estructura del código

- **HTML5 + CSS3 + JavaScript (sin frameworks).**
- **Estilos:** todo en una `<style>` dentro del `<head>` (CSS en línea del archivo).
- **Lógica:** un único bloque `<script>` al final del `<body>` que gestiona:
  - Diccionario de traducciones `{ es, en, fr }` y el cambio de idioma.
  - Pantalla de carga (splash) con barra de progreso.
  - Cursor personalizado.
  - Menú móvil (hamburguesa).
  - Animaciones "reveal" al hacer scroll.
  - Apertura/cierre del modal de talleres.
  - Toggle "Ver más / Ver menos" de los testimonios.
  - Generación del año actual en el copyright.
- **Meta datos SEO:** `title` y `meta description` en español, optimizados para buscadores.
- **Accesibilidad:** etiquetas `aria-label`, `role="dialog"`, `aria-hidden` en el modal, texto alternativo en imágenes.
- **Seguridad de enlaces:** todos los enlaces externos con `target="_blank"` usan `rel="noopener noreferrer"` y los enlaces de YouTube se sirven por `https://`.

---

## 5. Enlaces externos utilizados

| Tipo | Destino |
|---|---|
| Agendar sesión (varios) | Calendly (new-meeting-1, mentoria-1-1-financiera, paquete-3-sesiones-reinvencion, paquete-reinvencion-3-sesiones-) |
| Cursos digitales | Hotmart (U106706696X, I107427455H) |
| Instagram | instagram.com/soyyoselinfranco |
| YouTube | youtube.com/@soyyoselinfranco |
| Email | hola@yoselinfranco.com |
| Reseñas Google | g.page (Google Business) |
| Dominio | yoselinfranco.com |

### 5.1 Seguridad en enlaces externos
- Todos los enlaces externos que abren en pestaña nueva (`target="_blank"`) llevan **`rel="noopener noreferrer"`**:
  - `noopener`: impide el **reverse tabnabbing** (la página de destino no puede acceder a `window.opener` para redirigir o manipular la pestaña de origen).
  - `noreferrer`: no se envía la cabecera `Referer` con la URL de origen al sitio de destino.
- Los enlaces de **YouTube** se sirven siempre por **`https://`** (cifrado TLS), nunca por `http://`.
- Los enlaces `mailto:` (email) no requieren `rel` porque no abren una ventana nueva.
- Los enlaces internos de anclaje (`#hero`, `#about`, `#services`, etc.) no presentan riesgo de tabnabbing por ser navegación dentro de la misma página.

---

## 6. Notas finales
Este documento describe la versión actual de `index.html`. La landing está diseñada como una experiencia de una sola página que guía al visitante desde la primera impresión (hero), pasando por la propuesta de valor y los servicios, la historia personal para generar confianza, la oferta de cursos, la prueba social (testimonios) y cierra con el contacto y la política de sesiones. Todo el contenido está en **español natural y correcto**, con versiones equivalentes en **inglés y francés** para el selector de idiomas (excepto las citas de los testimonios, que se mantienen en español por ser reseñas textuales reales).

### Cambios recientes aplicados
- **Hero / Inicio (kicker):** "Mentora en Reinvención Personal y Financiera" → "Coach Personal y Mentora Financiera" (también en `<title>` y `meta_title`; traducciones ES / EN / FR).
- **Sección 02 — Servicios ("Qué ofrezco"):**
  - Subtítulo: "100% online vía Google Meet, en español, disponibles para Canadá, EE.UU. y Latinoamérica." → "100% online vía Google Meet, **en español e inglés, disponible donde quiera que estés**."
  - Nota al cierre: "Todos los servicios son 100% online, **en español e inglés, disponibles donde quiera que estés**."
- **Sección 03 — Quién Soy:** se reescribió el bloque de historia: el público objetivo pasa de "migrantes y mujeres" a "especialmente migrantes", se añade el párrafo sobre la "coherencia entre identidad y dinero", el bloque de ayuda concreta ("Mi misión es ayudar a migrantes y personas en transición a reorganizar su dinero… sin juicio") y el CTA final "¿Listo/a para empezar? Agenda tu sesión" (que enlaza a Contacto 06).
- **Footer — descripción:** "Mentora en reinvención personal y financiera para migrantes y personas que empiezan de nuevo. Desde la experiencia real, no desde la teoría perfecta." → "**Coach personal y mentora financiera** para migrantes y personas que empiezan de nuevo. Desde la experiencia real, no desde la teoría perfecta." (traducciones EN / FR actualizadas).
- **Sección 04 — Cursos y Talleres:** subtítulo → "Cursos, talleres y masterclases en vivo para reinventarte personal y financieramente".
- **Sección "Por qué Yoselin" (opción 03) y marquee:** "Acompañamiento en español" → "Acompañamiento **en español e inglés**" (reflejado también en las traducciones ES / EN / FR).
- **Sección 06 — Tarjeta "Cómo funcionan las sesiones":**
  - "Disponible en Canadá, EE.UU. y Latinoamérica" → "Disponible **donde quiera que estés**".
  - "En español, con calidez y sin filtros" → "**En español e inglés**, con calidez y sin filtros".
- **Seguridad de enlaces externos:** se añadió `rel="noopener noreferrer"` a los 14 enlaces externos con `target="_blank"` (Calendly, Hotmart, Instagram, YouTube, Google Reviews y dominio) para prevenir reverse tabnabbing y filtrado de referrer. Los enlaces de YouTube se actualizaron de `http://` a `https://`.
- **Nota:** no se implementó una Content Security Policy (CSP) estricta por ser una landing estática de un solo archivo con `<style>` y `<script>` inline; si se despliega en un hosting que admita cabeceras HTTP (Netlify, Cloudflare, Vercel), se recomienda aplicar la CSP vía cabeceras.
