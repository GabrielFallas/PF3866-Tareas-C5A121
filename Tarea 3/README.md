# Tarea 3 — Pruebas de accesibilidad de CRAutos

**Estudiante:** Gabriel Isaías Fallas López
**Curso:** PF3866 — Pruebas de Software
**Sistema:** [crautos.com](https://crautos.com)
**Fecha de ejecución:** 4 de octubre de 2026

## Índice

1. [Metodología y alcance](#metodología-y-alcance)
2. [Resultados del análisis con axe por página](resultados-axe.md)
3. [Evidencia](evidencia/) — resultados crudos de axe ([`evidencia/axe/`](evidencia/axe/)), [salida de la inspección manual](evidencia/inspeccion-manual.md) que complementa los reportes y [revisión de los pendientes de axe](evidencia/revision-pendientes-axe.md)
4. [Reportes de bugs](#reportes-de-bugs) (34 reportes)
6. [Hallazgos descartados](#hallazgos-descartados)
7. [Limitaciones](#limitaciones)

## Metodología y alcance

Se analizaron las páginas que implementan las funcionalidades críticas de la [Tarea 2](../Tarea%202/README.md):

| Funcionalidad crítica | Página analizada | Archivo de evidencia |
|---|---|---|
| CT-01 Búsqueda y listado | Catálogo de Autos Usados (escritorio y móvil) | [`catalogo.jsonl`](evidencia/axe/catalogo.jsonl), [`catalogo-movil.jsonl`](evidencia/axe/catalogo-movil.jsonl) |
| CT-01 Búsqueda y listado | Resultados de búsqueda (marca Toyota) | [`resultados.jsonl`](evidencia/axe/resultados.jsonl) |
| CT-02 Detalle y galería / CT-03 Contacto | Ficha del anuncio | [`ficha.jsonl`](evidencia/axe/ficha.jsonl) |
| CT-04 Publicación | Anuncie su auto | [`publicar.jsonl`](evidencia/axe/publicar.jsonl) |
| CT-04 Edición | Editar anuncio | [`editar.jsonl`](evidencia/axe/editar.jsonl) |

- **Herramienta y proceso.** Se usó **axe-core 4.10.2**, el motor en el que se basa Axe DevTools, cargado desde la consola del navegador y ejecutado con `axe.run(document)` por un agente de IA, con el fin de obtener resultados más precisos y reproducibles (el entorno fue el navegador integrado de una aplicación de escritorio, donde no se pueden instalar extensiones). Posteriormente, Gabriel contrastó los bugs reportados con la extensión **Axe DevTools**, realizó las correcciones respectivas y aprobó o rechazó cada bug. Los pasos para repetir el análisis con la extensión están al final de [resultados-axe.md](resultados-axe.md#cómo-reproducir-el-análisis).
- **Entorno.** Chromium 152 (navegador integrado de la app Claude), Windows 11 Pro, sin iniciar sesión. Viewport emulado de **1280×800** para todas las páginas; el catálogo se analizó además a **375×812** (móvil) porque el sitio es responsivo y muestra otro diseño de tarjetas. Cada archivo `.jsonl` registra la hora, el viewport y la versión de axe.
- **Inspección manual.** Solo se usó para complementar los reportes de axe (por ejemplo, leer el texto visible junto a un control sin etiqueta); el texto literal de cada consulta y su respuesta está en [`inspeccion-manual.md`](evidencia/inspeccion-manual.md). No se reportan hallazgos que no provengan de un resultado de axe.
- **Qué contiene cada reporte.** Los *pasos para reproducir* describen lo que se ejecutó; el *resultado obtenido* cita lo que devolvió axe o la consola (con el HTML real devuelto); las afirmaciones sobre lectores de pantalla no se incluyen porque no se probó con ninguno.
- **Qué es un reporte.** Cada reporte describe una sola causa. Los elementos que fallan por la misma causa, en la misma página y con la misma regla (por ejemplo, los controles de un mismo formulario sin etiqueta) van juntos en un reporte con una tabla que lista cada elemento, su selector y el HTML que devolvió axe. La prioridad de un reporte agrupado es la más alta de sus elementos, y el reporte anota la prioridad individual de cada uno.
- **Pendientes de axe.** Los resultados `incomplete` se revisaron calculando a mano el contraste de cada nodo (ver [`revision-pendientes-axe.md`](evidencia/revision-pendientes-axe.md)).
- **Prioridad.** 🔴 Crítica: control esencial del flujo crítico (marca, año, precio, datos de contacto, aceptación de términos, código y clave) sin nombre accesible. 🟠 Alta: impide o dificulta una función concreta (otros controles de formularios, enlaces sin nombre, texto en movimiento, zoom bloqueado, idioma). 🟡 Media: molesta, hay alternativa o el impacto es parcial (contraste, estructura, regiones). ⚪ Baja: detalle menor o decorativo.
- **Formato.** Sigue la [plantilla de ejemplo del curso](https://github.com/aariasucr/PF3866-II-2026/blob/main/Ejemplo-Reporte-Bug-Tarea3.md).

## Reportes de bugs

Total: **34** — 🔴 Crítica 5 · 🟠 Alta 11 · 🟡 Media 16 · ⚪ Baja 2.

El **contacto con el vendedor (CT-03)** se encuentra en la ficha del anuncio. Los cinco enlaces de contacto de la ficha (correo, teléfonos y WhatsApp) tienen texto y axe no los reportó, por lo que no generaron bugs propios; los botones de compartir sí fallan (BUG-014).


### Catálogo de Autos Usados y buscador (CT-01)

| ID | Título | Prioridad | Func. | Regla axe |
|---|---|---|---|---|
| [BUG-001](bugs/BUG-001.md) | Las fotos de los vehículos del catálogo son elementos `<object>` sin alternativa textual (escritorio) | 🟡 Media | CT-01 | `object-alt` |
| [BUG-002](bugs/BUG-002.md) | Las miniaturas de las tarjetas del catálogo son `<img>` sin atributo `alt` (vista móvil) | 🟡 Media | CT-01 | `image-alt` |
| [BUG-003](bugs/BUG-003.md) | Cada tarjeta del catálogo (vista móvil) tiene un enlace vacío a la ficha, duplicado del enlace con texto | 🟡 Media | CT-01 | `link-name` |
| [BUG-004](bugs/BUG-004.md) | El icono de financiamiento (`financeicon.png`) no tiene texto alternativo en el catálogo y en los resultados | 🟡 Media | CT-01 | `image-alt` |
| [BUG-005](bugs/BUG-005.md) | Las imágenes de relleno `nooption.gif` y `option3-56.gif` de las tarjetas del catálogo no tienen `alt` | ⚪ Baja | CT-01 | `image-alt` |
| [BUG-006](bugs/BUG-006.md) | Los títulos de sección del catálogo son imágenes (`destacados.png`, `destacadosdevendedores.png`, `searchtitle.png`) sin `alt` y no son encabezados | 🟡 Media | CT-01 | `image-alt` |
| [BUG-007](bugs/BUG-007.md) | Los tres banners del catálogo («Anuncia tu auto GRATIS», «Ofertas del día», «Síguenos en Facebook») son enlaces de imagen sin `alt` o con `alt` vacío | 🟠 Alta | CT-01 | `image-alt`, `link-name` |
| [BUG-008](bugs/BUG-008.md) | Los 16 controles del buscador del catálogo (14 desplegables, «Modelo» y «Utilizar modo SPLIT») no tienen nombre accesible ni etiqueta | 🔴 Crítica | CT-01 | `select-name`, `label` |
| [BUG-009](bugs/BUG-009.md) | El precio de las tarjetas (verde `#008800` sobre gris `#efefef`) no alcanza el contraste mínimo en el catálogo y en los resultados | 🟡 Media | CT-01 | `color-contrast` |
| [BUG-010](bugs/BUG-010.md) | Las descripciones de las tarjetas del catálogo y de los resultados de búsqueda usan `<marquee>` (texto que se desplaza automáticamente) | 🟠 Alta | CT-01 | `marquee` |

### Resultados de búsqueda (CT-01)

| ID | Título | Prioridad | Func. | Regla axe |
|---|---|---|---|---|
| [BUG-011](bugs/BUG-011.md) | El botón de imagen «Ajustar filtros» de los resultados de búsqueda no tiene atributo `alt` | 🟠 Alta | CT-01 | `input-image-alt` |
| [BUG-012](bugs/BUG-012.md) | Las 16 casillas de las tarjetas de los resultados (15 de comparación `name="c"` y la casilla de ejemplo `demo`) no tienen etiqueta | 🟠 Alta | CT-01 | `label` |

### Ficha del anuncio: detalle, galería y contacto (CT-02 / CT-03)

| ID | Título | Prioridad | Func. | Regla axe |
|---|---|---|---|---|
| [BUG-013](bugs/BUG-013.md) | Los íconos de acción de la ficha («Reportar», «Favoritos», «Autos similares», «Extraer») y `aiicon.png` son enlaces de imagen sin `alt` y sin nombre | 🟠 Alta | CT-02 | `image-alt`, `link-name` |
| [BUG-014](bugs/BUG-014.md) | Los botones «Compartir» de Facebook y WhatsApp de la ficha son enlaces sin texto (imagen con `alt` vacío) | 🟡 Media | CT-02 | `link-name` |
| [BUG-015](bugs/BUG-015.md) | El logo `bacsjlogo.png` aparece dos veces en la ficha sin `alt` (en la cuota mensual y como control con `onclick` que no es enfocable) | 🟡 Media | CT-02 | `image-alt` |
| [BUG-016](bugs/BUG-016.md) | Los controles de la galería de la ficha (anterior, siguiente, pausa y 8 indicadores) son enlaces sin nombre accesible | 🟠 Alta | CT-02 | `link-name` |

### Anuncie su auto (CT-04)

| ID | Título | Prioridad | Func. | Regla axe |
|---|---|---|---|---|
| [BUG-017](bugs/BUG-017.md) | Los 20 campos de «Datos Generales» de «Anuncie su auto» (marca, modelo, año, precio, etc.) no tienen etiqueta ni nombre accesible | 🔴 Crítica | CT-04 | `select-name`, `label` |
| [BUG-018](bugs/BUG-018.md) | Los 7 campos de contacto del anunciante de «Anuncie su auto» (nombre, correos, teléfonos y WhatsApp) no tienen etiqueta | 🔴 Crítica | CT-04 | `label` |
| [BUG-019](bugs/BUG-019.md) | Los grupos repetidos de radios y casillas de «Anuncie su auto» (km/millas, 39 de equipamiento, 38 de opciones de pago) no tienen etiqueta | 🟠 Alta | CT-04 | `label` |
| [BUG-020](bugs/BUG-020.md) | La casilla de aceptación de Términos y Condiciones y Aviso de Privacidad de «Anuncie su auto» no tiene etiqueta | 🔴 Crítica | CT-04 | `label` |
| [BUG-021](bugs/BUG-021.md) | Los dos enlaces a términos y aviso de privacidad (`terms.htm`, `terms2.htm`) de «Anuncie su auto» son imágenes sin `alt` ni texto | 🟠 Alta | CT-04 | `image-alt`, `link-name` |
| [BUG-022](bugs/BUG-022.md) | Las 30 imágenes `option3-1.gif` (140×17) de las opciones de pago de «Anuncie su auto» no tienen `alt` | 🟡 Media | CT-04 | `image-alt` |
| [BUG-023](bugs/BUG-023.md) | Las imágenes `recomendado.png` y `nuevo.gif` de «Anuncie su auto» no tienen `alt` | 🟡 Media | CT-04 | `image-alt` |

### Editar anuncio (CT-04)

| ID | Título | Prioridad | Func. | Regla axe |
|---|---|---|---|---|
| [BUG-024](bugs/BUG-024.md) | Los campos «Código de anuncio» y «Clave» de «Editar anuncio» no tienen etiqueta | 🔴 Crítica | CT-04 | `label` |
| [BUG-025](bugs/BUG-025.md) | El enlace «¿Olvidó su clave? OPRIMA AQUÍ» de «Editar anuncio» es una imagen sin `alt` ni texto | 🟠 Alta | CT-04 | `image-alt`, `link-name` |

### Plantilla y elementos comunes a todas las páginas

| ID | Título | Prioridad | Func. | Regla axe |
|---|---|---|---|---|
| [BUG-026](bugs/BUG-026.md) | La plantilla desactiva el zoom en móviles con `user-scalable=0` | 🟠 Alta | todas | `meta-viewport` |
| [BUG-027](bugs/BUG-027.md) | Ninguna página tiene un landmark `main` | 🟡 Media | todas | `landmark-one-main` |
| [BUG-028](bugs/BUG-028.md) | Gran parte del contenido de las páginas queda fuera de cualquier landmark (regla `region`) | 🟡 Media | todas | `region` |
| [BUG-029](bugs/BUG-029.md) | Cuatro encabezados saltan de nivel: `<h3>` del precio y `<h6>` «GALERIA DE FOTOS» (ficha), `<h4>` del pie y `<h5>` «Resultados de Búsqueda» | 🟡 Media | todas | `heading-order` |
| [BUG-030](bugs/BUG-030.md) | El logo del encabezado (enlace a Inicio) es una imagen con `alt` vacío y el enlace no tiene nombre | 🟠 Alta | todas | `link-name` |
| [BUG-031](bugs/BUG-031.md) | El logo y el ícono de Facebook del pie son una imagen sin `alt` y un enlace vacío | ⚪ Baja | todas | `image-alt`, `link-name` |
| [BUG-032](bugs/BUG-032.md) | La lista de redes sociales del pie (`ul.social`) tiene un `<a>` como hijo directo de `<ul>` | 🟡 Media | todas | `list` |
| [BUG-033](bugs/BUG-033.md) | Siete botones (BUSCAR, Comparar, Última Página, Continuar ×2, Anuncie Su Auto y Edite Su Anuncio) con texto blanco no alcanzan el contraste mínimo | 🟡 Media | todas | `color-contrast` |
| [BUG-034](bugs/BUG-034.md) | El botón «Volver» del encabezado móvil es un enlace de imagen sin `alt` ni nombre (`javascript:window.history.back()`) | 🟡 Media | todas | `image-alt`, `link-name` |


## Hallazgos descartados

Durante el análisis aparecieron resultados que **no se pudieron reproducir** y por eso no se reportan:

- `scrollable-region-focusable` (3 nodos `.table-responsive` en la ficha) apareció en una primera pasada exploratoria, pero no a 1280×800 ni a 800×600: en ambas, axe no lo reportó y `scrollWidth` era igual a `clientWidth` en todas las tablas ([detalle](evidencia/inspeccion-manual.md#ficha-del-anuncio--httpscrautoscomautosusadoscardetailcfmc20483869)).
- El botón «Volver» (`.callusbtn`) solo se reportó en la vista móvil (BUG-034); a 1280×800 no aparece como violación.


## Limitaciones

- Las herramientas automáticas cubren solo una parte de los criterios de WCAG. **No se probó con ningún lector de pantalla**, así que los reportes describen defectos del código y de las reglas WCAG, no cómo los anuncia un lector.
- Solo se documentan hallazgos que provienen de los resultados de axe; **no se hizo prueba de navegación por teclado**, por lo que quedan fuera, por ejemplo, el indicador de foco o el orden de tabulación.
- Los resultados dependen del viewport: el sitio es responsivo y cambia de diseño. Se usó 1280×800 (y 375×812 solo en el catálogo).
- Los resultados `incomplete` de axe se revisaron calculando el contraste (ver [`revision-pendientes-axe.md`](evidencia/revision-pendientes-axe.md)): de los 261 nodos de contraste pendientes, 248 cumplen, 12 quedan **sin concluir** porque el texto está sobre una foto de fondo (los títulos del banner) y 1 (número de página activo de los resultados, 4,43:1) incumple pero **no se reporta como bug** porque axe no lo marcó como violación. En los nodos que axe marcó por solapamiento se asumió que el solapamiento no cambia el fondo visible. Los `frame-tested` son iframes de terceros que axe no puede analizar.
- Los resultados automáticos provienen de axe-core 4.10.2 (motor de Axe DevTools) ejecutado por un agente de IA; fueron contrastados y validados posteriormente con la extensión Axe DevTools por el estudiante.
- El inventario de CRAutos cambia continuamente; los anuncios y los identificadores de búsqueda (`c=`) de las URL pueden no estar disponibles más adelante. El conteo exacto de elementos puede variar.
- No se envió ningún formulario, no se escribió ningún dato personal y no se inició sesión. Para probar la validación de «Anuncie su auto» se interceptó `window.alert` y se presionó **Continuar** sin completar los campos (la página nunca navegó). La ficha del anuncio muestra un teléfono personal de la persona vendedora; no se reproduce en estos documentos.
- No se analizaron la pantalla posterior a «Editar anuncio» (`editcar.cfm`, requiere código y clave válidos), el enlace de WhatsApp (servicio externo) ni la cuenta de usuario.
