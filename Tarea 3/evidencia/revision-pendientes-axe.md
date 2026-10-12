# Revisión manual de los resultados `incomplete` de axe

Fecha: 2026-10-04. Navegador integrado de la app Claude (Chromium 152, Windows 11), viewport 1280×800 (y 375×812 para el catálogo móvil). Axe-core 4.10.2. Sin sesión iniciada y sin enviar formularios.

Axe deja una comprobación como `incomplete` cuando no puede decidir si pasa o falla. Para cada nodo se indica el motivo que dio axe (`messageKey`) y qué se hizo.

## Método para `color-contrast`

Para cada nodo `incomplete` se leyeron con `getComputedStyle` el color del texto y el color de fondo del primer ancestro opaco (componiendo los fondos con transparencia que hubiera en el camino), se calculó la razón de contraste con la fórmula de WCAG 2.x y se comparó con el mínimo (4,5:1; 3:1 si el texto es de 24 px o más, o de 18,66 px o más en negrita). Un nodo cuyo fondo incluye una imagen no se puede medir así y se marcó aparte.

## Resultado por página

| Página | Nodos `color-contrast` pendientes | Motivo de axe | Cumplen al medirlos | No concluyentes | Fallan |
|---|---:|---|---:|---:|---:|
| Anuncie su auto | 156 | `elmPartiallyObscured` 151, `bgImage` 4, `pseudoContent` 1 | 155 | 1 (`h1`) | 0 |
| Editar anuncio | 6 | `bgImage` 4, `elmPartiallyObscured` 1, `pseudoContent` 1 | 5 | 1 (`h1`) | 0 |
| Catálogo (1280×800) | 22 | `elmPartiallyObscured` 17, `bgImage` 4, `pseudoContent` 1 | 21 | 1 (`h1`) | 0 |
| Catálogo (375×812) | 5 | `elmPartiallyObscured` 4, `pseudoContent` 1 | 4 | 1 (`h1`) | 0 |
| Resultados | 18 | `elmPartiallyObscured` 10, `bgImage` 4, `pseudoContent` 3, `shortTextContent` 1 | 14 | 3 (`h1`, `h5` ×2) | 1 (paginación, observación) |
| Ficha | 54 | `elmPartiallyObscured` 45, `bgImage` 4, `pseudoContent` 5 | 49 | 5 (`h1` ×2, `h3` ×2, `b`) | 0 |

«Cumplen» incluye los 4 enlaces del menú por página (se resolvieron con el peor caso, abajo). En los `elmPartiallyObscured` (texto de las tablas del formulario, de las tarjetas, etc.) axe no pudo decidir porque otro elemento se solapa; el cálculo se hizo sobre el fondo del elemento que lo contiene, así que **asume que el solapamiento no cambia el fondo visible**.

### Enlaces del menú principal (`bgImage`, 4 nodos por página)

Son texto blanco sobre `rgba(0,0,0,0.5)` que a su vez está sobre la imagen del banner con un degradado `linear-gradient(to right, rgba(231,42,26,.8), rgba(233,194,0,.6))`. No se puede leer el color real de la foto, pero se calculó el **peor caso** (foto blanca debajo del degradado y del 50 % de negro):

| Posición en el degradado | Contraste (foto blanca) | Contraste (foto negra) |
|---|---:|---:|
| Izquierda (rojo) | 9,86:1 | 13,61:1 |
| Centro | 7,10:1 | 12,54:1 |
| Derecha (amarillo) | 5,18:1 | 11,24:1 |

Todos superan 4,5:1, así que estos 4 enlaces por página **cumplen** aunque la imagen cambie.

### Títulos sobre la imagen del banner (`pseudoContent` y `bgImage`)

Los `<h1>` (y en resultados y ficha los `<h5>` y `<h3>` del banner) están en blanco sobre la misma imagen con degradado, esta vez sin el 50 % de negro. El fondo depende de la foto, que varía por página y, en la ficha, es la foto del vehículo:

| Posición en el degradado | Contraste (foto blanca) | Contraste (foto negra) |
|---|---:|---:|
| Izquierda | 3,54:1 | 6,38:1 |
| Centro | 2,15:1 | 5,56:1 |
| Derecha | 1,40:1 | 4,54:1 |

El resultado va de 1,4:1 a 6,4:1 según la foto, por eso **no se puede concluir** con axe ni con cálculo. En las capturas (por ejemplo [`resultados-escritorio.jpg`](resultados-escritorio.jpg) y la cabecera del catálogo) el texto se lee, pero eso no sustituye una medición sobre el píxel real. **Queda pendiente** de medir con un cuentagotas de color sobre la página real, y no se reporta como bug.

### Número de página activo en los resultados

En la paginación de resultados (`shortTextContent`, un solo carácter) axe no pudo decidir. Al medirlo a mano dio texto `rgb(255,255,255)` sobre `rgb(231,42,26)`, 16 px normal: **4,43:1**, por debajo de 4,5:1. Como axe lo dejó como `incomplete` y no como violación, **no se reporta como bug** en esta entrega; queda como observación.

## Otras reglas `incomplete`

| Regla | Dónde | Revisión | Conclusión |
|---|---|---|---|
| `frame-tested`, `frame-title-unique` | Catálogo (3), resultados, ficha, editar (1 cada una) | Los `<iframe>` son de Google Ads (`google_ads_iframe_…`), reCAPTCHA y DoubleClick, de otro origen: axe no puede entrar | Contenido de terceros; no se reporta |
| `link-in-text-block` | Catálogo, enlace «OFERTAS DEL DIA.» (`a.yellowfont`) | Color calculado `rgb(255,255,255)`, igual al texto que lo rodea, `text-decoration: none`; solo lo distingue estar dentro de un `<b>` | No se pudo medir el contraste por solapamiento; se distingue únicamente por negrita. No se reporta, queda como observación |

## Cómo repetirlo

```js
const r = await fetch('https://cdnjs.cloudflare.com/ajax/libs/axe-core/4.10.2/axe.min.js');
(0, eval)(await r.text());
const res = await axe.run(document, { runOnly: ['color-contrast'], resultTypes: ['violations', 'incomplete'] });
res.incomplete[0].nodes.map(n => ({ motivo: n.any[0].data.messageKey, html: n.html.slice(0, 80) }));
```

Nota: al ejecutar `axe.run` con todas las reglas en una pestaña recién abierta (visibilidad `hidden`) una vez devolvió 0 pendientes de contraste; limitando la ejecución a `color-contrast` y con el viewport fijado, los conteos coinciden con los guardados en `evidencia/axe/`.
