# Resultados del análisis con axe por página

Volver al [índice](README.md).

**Fecha de ejecución:** 2026-10-04 (entre 23:26 y 23:32 UTC)  
**Motor:** axe-core 4.10.2 (el motor de Axe DevTools), ejecutado en el navegador integrado de la app Claude (Chromium 152, Windows 11 Pro).  
**Viewport:** 1280×800 para las cinco páginas; el catálogo además a 375×812.  
**Reglas:** todas las predeterminadas de axe (WCAG 2.0/2.1/2.2 A y AA, más buenas prácticas). Se consultaron los resultados `violations` e `incomplete`.  
**Sin sesión iniciada y sin enviar formularios ni escribir datos.**

Los archivos [`evidencia/axe/*.jsonl`](evidencia/axe/) conservan, por página, cada regla con su impacto, el número de nodos y el HTML de cada nodo; los nodos con HTML idéntico se agruparon con su conteo (`"n"`), y para la regla `region` solo se guardaron ejemplos de selectores.

La escala de impacto es la de axe (*Crítico* > *Serio* > *Moderado*). La prioridad de cada bug (Crítica/Alta/Media/Baja) la asigné yo con los criterios descritos en el [README](README.md#metodología-y-alcance).

## Páginas analizadas

| # | Funcionalidad (Tarea 2) | Página | URL | Archivo |
|---|---|---|---|---|
| 1 | CT-01 | Catálogo de Autos Usados | `https://crautos.com/autosusados/index.cfm` | [`catalogo.jsonl`](evidencia/axe/catalogo.jsonl) · [`catalogo-movil.jsonl`](evidencia/axe/catalogo-movil.jsonl) |
| 2 | CT-01 | Resultados de búsqueda (marca Toyota) | `https://crautos.com/autosusados/searchresults.cfm?p=1&c=10040` ¹ | [`resultados.jsonl`](evidencia/axe/resultados.jsonl) |
| 3 | CT-02 / CT-03 | Ficha del anuncio (Nissan FRONTIER 2016) | `https://crautos.com/autosusados/cardetail.cfm?c=20483869` ² | [`ficha.jsonl`](evidencia/axe/ficha.jsonl) |
| 4 | CT-04 | Anuncie su auto | `https://crautos.com/autosusados/anunciarse.cfm` | [`publicar.jsonl`](evidencia/axe/publicar.jsonl) |
| 5 | CT-04 | Editar anuncio | `https://crautos.com/anuncios/` | [`editar.jsonl`](evidencia/axe/editar.jsonl) |

¹ El valor `c=` es un identificador de búsqueda de sesión y caduca; para reproducir hay que repetir la búsqueda desde el catálogo (marca *Toyota* → **BUSCAR**).  
² Los anuncios cambian; usar cualquier ficha activa.

## Resumen por página (1280×800)

Número de **nodos** (elementos HTML) afectados por regla.

| Regla axe | Impacto | Catálogo | Resultados | Ficha | Publicar | Editar | Total |
|---|---|---:|---:|---:|---:|---:|---:|
| `image-alt` | Crítico | 114 | 8 | 8 | 35 | 2 | 167 |
| `label` | Crítico | 2 | 16 | — | 95 | 2 | 115 |
| `select-name` | Crítico | 14 | — | — | 12 | — | 26 |
| `input-image-alt` | Crítico | — | 1 | — | — | — | 1 |
| `meta-viewport` | Crítico | 1 | 1 | 1 | 1 | 1 | 5 |
| `object-alt` | Serio | 62 | — | — | — | — | 62 |
| `link-name` | Serio | 5 | 2 | 20 | 4 | 3 | 34 |
| `color-contrast` | Serio | 65 | 23 | 2 | 3 | 3 | 96 |
| `marquee` | Serio | 55 | 17 | — | — | — | 72 |
| `list` | Serio | 1 | 1 | 1 | 1 | 1 | 5 |
| `region` | Moderado | 81 | 31 | 17 | 33 | 9 | 171 |
| `landmark-one-main` | Moderado | 1 | 1 | 1 | 1 | 1 | 5 |
| `heading-order` | Moderado | 1 | 1 | 2 | 1 | 1 | 6 |
| **Total de nodos** | | **402** | **102** | **52** | **186** | **23** | **765** |
| Reglas con violación | | 12 | 11 | 8 | 10 | 9 | 13 distintas |
| Reglas que pasaron | | 35 | 36 | 32 | 33 | 34 | |

Por impacto: **314** nodos críticos (41 %), **269** serios (35 %) y **182** moderados (24 %).

Catálogo a 375×812 (vista móvil): 335 nodos; `image-alt` 127, `link-name` 67, `region` 83, `marquee` 37, `select-name` 14, `label` 2, `color-contrast` 1, `heading-order` 1, `landmark-one-main` 1, `list` 1, `meta-viewport` 1. A diferencia del escritorio, no aparece `object-alt` porque las fotos de las tarjetas son `<img>`.

## Elementos `incomplete` (revisión manual)

| Página | Regla | Nodos |
|---|---|---:|
| Catálogo (1280×800) | `color-contrast` | 22 |
| Catálogo (1280×800) | `frame-tested` / `frame-title-unique` | 3 / 3 |
| Catálogo (1280×800) | `link-in-text-block` | 1 |
| Catálogo (375×812) | `color-contrast` / `link-in-text-block` | 5 / 1 |
| Resultados | `color-contrast` / `frame-tested` | 18 / 1 |
| Ficha | `color-contrast` / `frame-tested` | 54 / 1 |
| Publicar | `color-contrast` | 156 |
| Editar | `color-contrast` / `frame-tested` | 6 / 1 |

**Revisión.** Se midió a mano el contraste de los nodos pendientes (detalle y método en [`revision-pendientes-axe.md`](evidencia/revision-pendientes-axe.md)): 248 de 261 cumplen, 12 no se pueden concluir porque el texto de los títulos del banner está sobre una foto y 1 incumple (número de página activo de los resultados, 4,43:1) pero no se reporta como bug porque axe no lo marcó como violación. Los `frame-tested` y `frame-title-unique` son iframes de terceros.

## Cómo reproducir el análisis

Con la extensión **Axe DevTools** (Chrome/Firefox): abrir la página en un viewport de 1280×800, abrir DevTools → pestaña *axe DevTools* → *Scan all of my page*, y comparar con las tablas anteriores. Los números pueden variar con la versión de las reglas y con el inventario (los anuncios cambian).

Con la consola del navegador (lo que se hizo aquí):

```js
const r = await fetch('https://cdnjs.cloudflare.com/ajax/libs/axe-core/4.10.2/axe.min.js');
(0, eval)(await r.text());
const res = await axe.run(document, { resultTypes: ['violations', 'incomplete'] });
console.table(res.violations.map(v => ({ regla: v.id, impacto: v.impact, nodos: v.nodes.length })));
```
