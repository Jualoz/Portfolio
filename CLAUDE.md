# CLAUDE.md

Contexto del proyecto para Claude Code.

## Qué es

CV / portfolio personal de **Juan Pablo Lozada Gómez** (Desarrollador Fullstack, Bucaramanga, Colombia).
Es una sola página estática publicada con **GitHub Pages** en https://jualoz.github.io/Portfolio/
(repo: `github.com/Jualoz/Portfolio`, rama `main`).

## Estructura

- `index.html` — todo el sitio: HTML + CSS embebido en `<style>` + un poco de JavaScript vanilla al final. Sin build, dependencias ni tests.
- Recursos externos por CDN: Google Fonts (Archivo, Manrope, JetBrains Mono, Caveat) y Font Awesome `6.5.2` (cdnjs).

Para verlo basta con abrir `index.html` en el navegador. Cada push a `main` se publica en GitHub Pages.

## Secciones (en orden)

1. Barra de navegación fija (`.nav`, transparente hasta hacer scroll): marca "JL · LOZADA", enlaces, botón PDF (`window.print()`) y "Contacto".
2. Hero (`#hero`): titular grande (sin etiqueta encima) con palabra destacada en el color de acento (color sólido, sin degradado), resumen que empieza con el nombre ("Soy Juan Pablo Lozada…"), `.tag`s, botones y línea `.areas` con el estado "Disponible". A la derecha, mockups decorativos de laptop y móvil hechos en CSS (`.devices`, `aria-hidden`) con notas manuscritas (`.note`).
3. Índice numerado 01–04 (`.index`), que sirve de navegación.
4. `#perfil` (01) — texto + estadísticas (`.stats`; los años se calculan en JS desde 03/2024 con `data-years`).
5. `#stack` (02) — "Caja de herramientas": bento `.bento` (6 columnas) con cinco `.tool` (Frontend ancho `.tool-wide`, Bases de datos `.tool-db` con órbita, Backend, APIs, Herramientas & Metodologías). Cada tarjeta: diagrama decorativo `.tool-art` (nodos `.node`/`.node-core` posicionados con `--x`/`--y` en % y líneas SVG `.wires` con `viewBox 0 0 100 100`), `h3`, `.tool-list` y nota manuscrita `.tool-note`. Inspirado en un diseño "My Tech Toolbox" que pasó el usuario.
   Después, bandas cruzadas `.ribbons` (`.band-back` gris y `.band-front` en el acento) con las tecnologías; se mueven solo con el scroll (`animation-timeline: view()`), nunca en bucle.
6. `#experiencia` (03) — filas `.job` (fecha a la izquierda, detalle a la derecha): Transforsweb, 03/2024 – Actualidad.
7. `#educacion` (04) — tres `.edu-card`: título (Campuslands, 2023), formación continua, idiomas y disponibilidad.
8. `#contacto` (05) — titular grande, email destacado (`.big-mail`) y `.contact-list`; pie con año dinámico.

## Diseño

- Estética oscura "cinematográfica" inspirada en el shot de Dribbble *Spidey – Interactive Developer Portfolio*: fondo casi negro, acento verde azulado `#327878` y secundario azul claro `#92c6d3`, tipografía display muy pesada, notas a mano y grano de película (`body::after`).
- Solo tema oscuro (no hay selector de tema). Tokens en `:root`: `--accent` (#327878, decoración y líneas), `--accent-rgb` (mismo color en `r, g, b` para los `rgba()` de brillos y bordes), `--accent-text` (#529494, versión más clara con contraste ≥ 5:1 sobre el fondo y sobre los fondos tintados), `--accent-btn` + `--on-accent` (fondo de botones y su texto) y `--accent-soft`. Secundario: `--accent-2` (#92c6d3) y `--accent-2-rgb`, usado en notas manuscritas, cadenas del código, hover de chips/tags, nombre de la empresa, los "+" de las estadísticas, la línea superior de las tarjetas y parte de los brillos; en impresión se oscurece a #2f6676 (y el acento a #2a6767). Para cambiar el acento basta con editar estos tokens (y el color de la favicon); no hay colores de acento fijos en el resto del CSS. El acento pasó por rojo, gris oscuro y verde fosforescente antes de quedar en #327878.
- Fuentes: `--font-display` (Archivo 800/900, títulos), `--font-body` (Manrope), `--font-mono` (etiquetas, números, chips), `--font-script` (Caveat, notas).
- Títulos de sección: solo `h2` con punto final en `.accent` (sin etiquetas ni números encima; Impeccable los prohíbe). Títulos de tarjeta de educación con icono en línea (`.card-title`), sin caja de icono.
- Sombras neutras con desplazamiento (negras); nada de halos de color alrededor de botones, tarjetas o mockups. La luz de color solo como degradados radiales de fondo.
- Mockups: se escalan con unidades de contenedor (`cqw`) dentro de `.devices` (`container-type: inline-size`). Al pasar el ratón, JS mueve el foco de luz (`--mx`/`--my` en `.hero`) y gira los dispositivos (`--rx`/`--ry`), solo con puntero fino y sin `prefers-reduced-motion`.
- Usar `overflow: clip` (no `hidden`) en contenedores: con `hidden` el hero se convertía en contenedor con scroll y el contenido se desplazaba solo.
- Animación de aparición: clase `.reveal` en contenedores (usa `translate`, no `transform`, para no chocar con el hover de `.card`). Solo se activa si existe `IntersectionObserver` (clase `js` en `<html>`).
- Breakpoints: 980px (columnas → 1–2), 860px (se ocultan los enlaces del nav), 620px (móvil). Los hijos de las grids llevan `min-width: 0`.
- `@media print` genera un CV claro y limpio: muestra `.print-header` (nombre y contacto, solo impresión) y oculta nav, mockups, bandas, índice, notas, diagramas `.tool-art`, estadísticas y contacto; el bento pasa a 3 columnas. Verificarlo al cambiar el layout.

## Convenciones

- Todo el contenido y los comentarios están en **español**; mantenerlo así.
- Reutilizar las clases existentes (`.section`, `.sec-head`, `.card`, `.card-title`, `.tool`/`.node`, `.chips`/`.chip`, `.tag`, `.item-list`, `.btn-accent`/`.btn-ghost`/`.btn-outline`) al añadir contenido.
- No inventar datos del CV (proyectos, cifras, empresas): solo lo que el usuario haya dado.
- Iconos con Font Awesome 6.5 (`fas` / `far` / `fab`).
- Commits cortos en inglés, en imperativo (p. ej. `Update job title ...`, `Add portfolio link ...`).

## Ideas pendientes

- Sección de proyectos destacados con capturas y vista previa en `iframe` bajo demanda (necesita los proyectos reales del usuario). Encaja como "05 — Proyectos" y los mockups del hero podrían mostrar capturas reales.
- Foto del usuario en el hero (la referencia usa un retrato en blanco y negro con luz roja).
- Imagen `og:image` para la vista previa al compartir el enlace.

## Impeccable

- Instalado en el proyecto (`.claude/skills/impeccable/`, agentes en `.claude/agents/`, hooks en `.claude/settings.local.json`). Las auditorías se guardan con `impeccable audit-storage`.
- Para revisar, usar el escaneo renderizado (`impeccable detect --viewport 1280x800 file:///.../index.html` y `--viewport 390x844`): el escaneo estático del archivo mezcla los colores de `@media print` con los de pantalla y da falsos positivos de contraste y tracking.
- Mínimos de contraste: `--text-3` #85858d y `--accent-text` #529494 (≥ 4.5:1 también sobre tarjetas y fondos tintados). Sin texto en degradado.
- Ya corregidos: kickers sobre los h2, eyebrow del hero, cajas de icono sobre los h3, marquee en bucle, halos de color y titular del hero demasiado grande (ahora `clamp(2.4rem, 5.2vw, 4.4rem)`).
- Único hallazgo que se mantiene: `ai-color-palette` ("Cyan gradient background"), porque el verde azulado #327878 lo eligió el usuario.
