# Instrucciones para agentes AI (Copilot)

Breve: este repositorio es un sitio web estático (HTML/CSS/JS). Cambios habituales son de UI, estilos y pequeños scripts del lado cliente.

Arquitectura rápida
- Tipo: sitio estático sin backend. Páginas principales: [index.html](index.html), [blog.html](blog.html), [eventos.html](eventos.html), [recursos.html](recursos.html).
- Estilos: Tailwind cargado vía CDN en la cabeza de [index.html](index.html) y CSS adicional en [css/style.css](css/style.css). Busca la clase `.glass` en `css/style.css` para estilos reutilizables.
- JavaScript: lógica cliente en [js/main.js](js/main.js). Funciones clave: menú móvil (`mobile-menu-button` / `mobile-menu`), contador (`days`,`hours`,`minutes`,`seconds`) y `addToCalendar(...)` para abrir Google Calendar.

Patrones y convenciones del proyecto
- Idioma: contenido en español; conserva la voz y copy existentes al editar textos.
- Estructura: archivos estáticos en la raíz, recursos en `css/` y `js/`.
- Tailwind: el marcado usa utilidades Tailwind directamente (CDN). Evita reemplazar utilidades por CSS salvo para reglas globales compartidas.
- IDs y hooks: `js/main.js` selecciona elementos por ID — no cambies esos IDs sin actualizar el script (ej.: `mobile-menu-button`, `mobile-menu`, `days`).

Integraciones y puntos de atención
- Google Calendar: `addToCalendar(title, start, end, location, details)` construye y abre una URL de calendario. Ejemplo de uso:

```js
addToCalendar('Streaming Party','2026-05-15T16:00:00','2026-05-15T18:00:00','Lima, Perú','Evento de prueba');
```

- Discord: enlaces al servidor están en header/footer y usan `target="_blank"`.
- CDNs: Tailwind, Google Fonts y FontAwesome se cargan por CDN; cualquier cambio debe mantener equivalencia para evitar roturas visuales.

Flujo de trabajo recomendado
- No hay pipeline de build: para probar localmente abre `index.html` en el navegador o ejecuta un servidor estático:

```bash
# desde la raíz del repo
npx http-server -c-1 .
# o usar la extensión Live Server de VSCode
```

- Depuración: usa la consola del navegador para errores JS; si el contador no se actualiza, revisa `targetDate` en [js/main.js](js/main.js) y que los elementos con IDs existan en el HTML.

Guías para cambios hechos por agentes AI
- Estilos: añadir reglas globales reutilizables en `css/style.css`; para cambios puntuales prefiere utilidades Tailwind en el HTML.
- JS: agrupa nueva lógica en `js/main.js`. Si expones funciones para atributos `onclick`, añádelas a `window.` para compatibilidad global.
- Contenido: mantener todos los textos en español y respetar el tono informal actual.
- Accesibilidad: preserva `aria-` y atributos `alt`/`data-alt` en imágenes y botones.

Qué evitar
- No migrar Tailwind a una pipeline local sin coordinación (la configuración actual depende del CDN y de `tailwind.config` inline).
- No renombrar IDs usados por `js/main.js` sin actualizar el script.

Archivos clave para revisar antes de PR
- [index.html](index.html) — estructura global y enlaces a CDNs
- [js/main.js](js/main.js) — interacciones: menú, contador, `addToCalendar`
- [css/style.css](css/style.css) — estilos compartidos (ej. `.glass`)

Notas finales
- No se encontró un archivo previo de instrucciones; se creó este archivo con las observaciones más relevantes detectables en el repositorio.
- Puedo ampliar con ejemplos de PR, plantillas de commit o racionales de diseño si quieres.
