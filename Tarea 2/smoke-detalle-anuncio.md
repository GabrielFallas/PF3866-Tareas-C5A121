# FC-02 — Detalle y galería del anuncio

**Ejecución real:** 12/09/2026, 18:14 UTC-06:00.  
**Entorno:** CRAutos producción, navegador sin sesión y Playwright MCP.  
**Anuncio usado:** Toyota FORTUNER 2024, ¢24 900 000, código público `6656966`.

---

# Caso de Prueba: Abrir ficha desde un resultado

## ID

CT-DET-001

## Objetivo

Verificar la transición desde una tarjeta hacia la ficha del vehículo.

## Precondiciones

- Resultados Toyota 2024 visibles.

## Datos de Entrada

- Tarjeta Toyota FORTUNER 2024, ¢24 900 000.

## Pasos

1. Abrir la tarjeta del FORTUNER desde los resultados.
2. Comparar la URL, el título y el precio con la tarjeta de origen.

## Resultado Esperado

- Abre `autosusados/cardetail.cfm?c=...` con el mismo vehículo y precio.

## Resultado Obtenido

- Se abrió `https://crautos.com/autosusados/cardetail.cfm?c=6656966`.
- El encabezado mostró Toyota FORTUNER 2024 y ¢24 900 000, iguales a la tarjeta elegida.

## Estado de la prueba

✅ Pasó

## Observaciones

- El anuncio estaba activo durante la ejecución y puede cambiar posteriormente.

---

# Caso de Prueba: Ver información comercial y técnica

## ID

CT-DET-002

## Objetivo

Verificar que la ficha entregue información suficiente para evaluar el vehículo.

## Precondiciones

- Ficha `c=6656966` abierta.

## Datos de Entrada

- Anuncio público Toyota FORTUNER 2024.

## Pasos

1. Revisar modelo, precio y tabla de especificaciones.
2. Localizar cilindrada, combustible, transmisión, kilometraje y provincia.

## Resultado Esperado

- Los atributos técnicos y comerciales se muestran con valores legibles.

## Resultado Obtenido

- La ficha mostró 2 800 cc, diésel, Automática/Dual, SUV 4WD/AWD, 56 000 km y Heredia.
- También indicó siete pasajeros, estado Excelente y placa ND.

## Estado de la prueba

✅ Pasó

## Observaciones

- Los atributos corresponden a la ficha observada en la fecha de ejecución.

---

# Caso de Prueba: Navegar fotografías de la galería

## ID

CT-DET-003

## Objetivo

Verificar el avance y retroceso de la **GALERIA DE FOTOS**.

## Precondiciones

- Ficha `c=6656966` abierta y galería disponible.

## Datos de Entrada

- Controles `ws_next` y `ws_prev`.

## Pasos

1. Ubicar la galería y pausar el avance automático.
2. Presionar `ws_next`.
3. Presionar `ws_prev`.

## Resultado Esperado

- La foto cambia al avanzar y vuelve a la anterior al retroceder, sin afectar la ficha.

## Resultado Obtenido

- El indicador cambió de la posición 4 a la 5 con `ws_next` y volvió a la posición 4 con `ws_prev`.
- Título, precio y especificaciones se mantuvieron visibles.

## Estado de la prueba

✅ Pasó

## Observaciones

- La interacción no modificó datos del anuncio.

---

# Caso de Prueba: Consultar vehículos del mismo vendedor

## ID

CT-DET-004

## Objetivo

Verificar el acceso al inventario publicado por el mismo vendedor.

## Precondiciones

- Ficha `c=6656966` abierta.

## Datos de Entrada

- Enlace **Ver todos los vehículos de este vendedor**.

## Pasos

1. Presionar el enlace del mismo vendedor.
2. Revisar URL, encabezado y tarjetas del listado.

## Resultado Esperado

- Se abre un listado del vendedor con tarjetas que permitan abrir fichas.

## Resultado Obtenido

- Se abrió `ssearchresults.cfm?p=1&c=BMEO5649`, encabezada por José Pablo Vega.
- Se mostraron, entre otras, Kia PICANTO 2016 y Kia SORENTO 2012; la página expuso 45 enlaces a fichas `cardetail.cfm`.

## Estado de la prueba

✅ Pasó

## Observaciones

- Este caso cubre vehículos del mismo vendedor, no el enlace distinto `similar.cfm`.

## Resumen de ejecución

| Caso | Resultado obtenido | Estado |
|---|---|---|
| CT-DET-001 | Ficha y precio coincidentes con la tarjeta. | ✅ Pasó |
| CT-DET-002 | Especificaciones técnicas visibles. | ✅ Pasó |
| CT-DET-003 | Indicador de foto 4 → 5 → 4. | ✅ Pasó |
| CT-DET-004 | Listado del mismo vendedor disponible. | ✅ Pasó |
