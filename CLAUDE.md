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
2. Hero (`#hero`): kicker con nombre y rol, titular grande con palabra destacada en gris, resumen, `.tag`s, botones y áreas. A la derecha, mockups decorativos de laptop y móvil hechos en CSS (`.devices`, `aria-hidden`) con notas manuscritas (`.note`).
3. Cinta de tecnologías animada (`.marquee`) e índice numerado 01–04 (`.index`).
4. `#perfil` (01) — texto + estadísticas (`.stats`; los años se calculan en JS desde 03/2024 con `data-years`).
5. `#stack` (02) — tres `.stack-card` con `.chip`: Frontend, Backend & APIs, Herramientas & Metodologías.
6. `#experiencia` (03) — filas `.job` (fecha a la izquierda, detalle a la derecha): Transforsweb, 03/2024 – Actualidad.
7. `#educacion` (04) — tres `.edu-card`: título (Campuslands, 2023), formación continua, idiomas y disponibilidad.
8. `#contacto` (05) — titular grande, email destacado (`.big-mail`) y `.contact-list`; pie con año dinámico.

## Diseño

- Estética oscura "cinematográfica" inspirada en el shot de Dribbble *Spidey – Interactive Developer Portfolio*: fondo casi negro, acento gris oscuro (monocromo), tipografía display muy pesada, notas a mano y grano de película (`body::after`).
- Solo tema oscuro (no hay selector de tema). Tokens en `:root`: `--accent` (decoración, líneas), `--accent-text` (texto destacado con buen contraste), `--accent-btn` (fondo de botones con texto blanco), `--accent-glow` y `--accent-soft`. El acento era rojo y se cambió a gris oscuro; no reintroducir rojo.
- Fuentes: `--font-display` (Archivo 800/900, títulos), `--font-body` (Manrope), `--font-mono` (etiquetas, números, chips), `--font-script` (Caveat, notas).
- Títulos de sección: `.sec-num` ("0N — Nombre") + `h2` con punto final en `.accent`.
- Mockups: se escalan con unidades de contenedor (`cqw`) dentro de `.devices` (`container-type: inline-size`). Al pasar el ratón, JS mueve el foco de luz (`--mx`/`--my` en `.hero`) y gira los dispositivos (`--rx`/`--ry`), solo con puntero fino y sin `prefers-reduced-motion`.
- Usar `overflow: clip` (no `hidden`) en contenedores: con `hidden` el hero se convertía en contenedor con scroll y el contenido se desplazaba solo.
- Animación de aparición: clase `.reveal` en contenedores (usa `translate`, no `transform`, para no chocar con el hover de `.card`). Solo se activa si existe `IntersectionObserver` (clase `js` en `<html>`).
- Breakpoints: 980px (columnas → 1–2), 860px (se ocultan los enlaces del nav), 620px (móvil). Los hijos de las grids llevan `min-width: 0`.
- `@media print` genera un CV claro y limpio: muestra `.print-header` (nombre y contacto, solo impresión) y oculta nav, mockups, cinta, índice, notas, estadísticas y contacto. Verificarlo al cambiar el layout.

## Convenciones

- Todo el contenido y los comentarios están en **español**; mantenerlo así.
- Reutilizar las clases existentes (`.section`, `.sec-head`, `.sec-num`, `.card`, `.icon-tile`, `.chips`/`.chip`, `.tag`, `.item-list`, `.btn-accent`/`.btn-ghost`/`.btn-outline`) al añadir contenido.
- No inventar datos del CV (proyectos, cifras, empresas): solo lo que el usuario haya dado.
- Iconos con Font Awesome 6.5 (`fas` / `far` / `fab`).
- Commits cortos en inglés, en imperativo (p. ej. `Update job title ...`, `Add portfolio link ...`).

## Ideas pendientes

- Sección de proyectos destacados con capturas y vista previa en `iframe` bajo demanda (necesita los proyectos reales del usuario). Encaja como "05 — Proyectos" y los mockups del hero podrían mostrar capturas reales.
- Foto del usuario en el hero (la referencia usa un retrato en blanco y negro con luz roja).
- Imagen `og:image` para la vista previa al compartir el enlace.
