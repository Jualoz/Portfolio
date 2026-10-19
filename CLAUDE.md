# CLAUDE.md

Contexto del proyecto para Claude Code.

## Qué es

CV / portfolio personal de **Juan Pablo Lozada Gómez** (Desarrollador Fullstack, Bucaramanga, Colombia).
Es una sola página estática publicada con **GitHub Pages** en https://jualoz.github.io/Portfolio/
(repo: `github.com/Jualoz/Portfolio`, rama `main`).

## Estructura

- `index.html` — todo el sitio: HTML + CSS embebido en `<style>` + un poco de JavaScript vanilla al final. Sin build, dependencias ni tests.
- Recursos externos por CDN: Google Fonts (Inter, Space Grotesk, JetBrains Mono) y Font Awesome `6.5.2` (cdnjs).

Para verlo basta con abrir `index.html` en el navegador. Cada push a `main` se publica en GitHub Pages.

## Secciones (en orden)

1. Barra de navegación fija: logo "JL", enlaces a secciones, botón de tema claro/oscuro y "Descargar CV" (`window.print()`).
2. Hero: estado de disponibilidad, nombre, rol, resumen, botones y datos de contacto (`.hero-meta`); a la derecha, tarjeta de código decorativa (`.code-card`, `aria-hidden`).
3. `#perfil` — texto del perfil + tres tarjetas `.highlight`.
4. `#habilidades` — tres `.skill-card` con `.chip`: Frontend, Backend & APIs, Herramientas & Metodologías.
5. `#experiencia` — línea de tiempo (`.timeline` / `.tl-item`): Transforsweb, 03/2024 – Actualidad.
6. `#educacion` — tres `.edu-card`: título (Campuslands, 2023), formación continua, idiomas y disponibilidad.
7. `#contacto` — bloque `.cta` oscuro con botones y redes; pie con año dinámico.

## Diseño

- Tokens de color en `:root` (claro); el oscuro se define dos veces: en `@media (prefers-color-scheme: dark)` con `:root:not([data-theme="light"])` y en `:root[data-theme="dark"]`. Al cambiar un color, actualizar ambos bloques.
- El tema elegido se guarda en `localStorage` (`theme`) y se aplica en un script del `<head>` para evitar parpadeo.
- Acento: degradado cian → índigo (`--grad` para texto/decoración, `--btn-grad` más oscuro para botones con texto blanco).
- Animación de aparición: clase `.reveal` en contenedores (usa `translate`, no `transform`, para no chocar con el hover de `.card`). Solo se activa si existe `IntersectionObserver` (clase `js` en `<html>`). Se respeta `prefers-reduced-motion`.
- Breakpoints: 900px (columnas → 1–2), 820px (se ocultan los enlaces del nav), 620px (móvil). Los hijos de las grids llevan `min-width: 0` para que la tarjeta de código no desborde en móvil.
- `@media print` genera un CV limpio: fuerza colores claros y oculta nav, decoración, botones, highlights y contacto. Verificarlo al cambiar el layout.

## Convenciones

- Todo el contenido y los comentarios están en **español**; mantenerlo así.
- Reutilizar las clases existentes (`.section`, `.section-head`, `.eyebrow`, `.card`, `.icon-tile`, `.chips`/`.chip`, `.item-list`, `.date-pill`) al añadir contenido.
- No inventar datos del CV (proyectos, cifras, empresas): solo lo que el usuario haya dado.
- Iconos con Font Awesome 6.5 (`fas` / `far` / `fab`).
- Commits cortos en inglés, en imperativo (p. ej. `Update job title ...`, `Add portfolio link ...`).

## Ideas pendientes

- Sección de proyectos destacados (necesita los proyectos reales del usuario).
- Foto o avatar en el hero.
- Imagen `og:image` para la vista previa al compartir el enlace.
