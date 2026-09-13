# FC-01 — Búsqueda y listado de vehículos

**Ejecución real:** 12/09/2026, 18:14 UTC-06:00.  
**Entorno:** CRAutos producción, navegador sin sesión y Playwright MCP.

---

# Caso de Prueba: Abrir catálogo y formulario de búsqueda

## ID

CT-BUS-001

## Objetivo

Verificar que **Autos Usados** muestre inventario y los filtros de búsqueda públicos.

## Precondiciones

- Navegador con conexión a Internet y sin sesión iniciada.

## Datos de Entrada

- URL: `https://crautos.com/autosusados/index.cfm`.

## Pasos

1. Abrir el catálogo de Autos Usados.
2. Revisar el contador, al menos una tarjeta y el formulario debajo del listado.
3. Confirmar los controles y el botón **BUSCAR**.

## Resultado Esperado

- Se visualizan vehículos y un formulario con filtros de búsqueda.

## Resultado Obtenido

- El catálogo mostró 12 207 vehículos, 3 660 con financiamiento y 25 ofertas del día.
- Se mostraron tarjetas y los filtros Marca, Modelo, Estilo, Combustible, Transmisión, Año Entre, Precio Entre, Ordenar por, Mostrar y **BUSCAR**.

## Estado de la prueba

✅ Pasó

## Observaciones

- El formulario se ubicó después del listado de tarjetas.

---

# Caso de Prueba: Filtrar Toyota 2024 por rango de precio

## ID

CT-BUS-002

## Objetivo

Verificar una búsqueda combinada con marca, año y precio.

## Precondiciones

- Catálogo de Autos Usados abierto.

## Datos de Entrada

- Marca: Toyota.
- Año entre: 2024 y 2024.
- Precio entre: ¢20 000 000 y ¢40 000 000.

## Pasos

1. Seleccionar Toyota, establecer 2024 como año inicial y final y definir el rango de precio indicado.
2. Presionar **BUSCAR**.
3. Revisar la URL y el primer resultado.

## Resultado Esperado

- Se cargan resultados Toyota 2024 dentro del rango, con atributos y precio.

## Resultado Obtenido

- Se abrió `searchresults.cfm?p=1&c=09120` con 69 resultados.
- El primero fue Toyota FORTUNER 2024, Diesel, automática, 2 800 cc, Heredia, por ¢24 900 000.

## Estado de la prueba

✅ Pasó

## Observaciones

- El inventario cambia; el vehículo se registra como evidencia de esta ejecución.

---

# Caso de Prueba: Buscar por texto de modelo

## ID

CT-BUS-003

## Objetivo

Verificar el filtro textual **Modelo**.

## Precondiciones

- Catálogo de Autos Usados abierto.

## Datos de Entrada

- Marca: Toyota.
- Modelo: FORTUNER.

## Pasos

1. Seleccionar Toyota.
2. Escribir `FORTUNER` en Modelo.
3. Presionar **BUSCAR**.

## Resultado Esperado

- Se muestran coincidencias Toyota FORTUNER o un mensaje de ausencia de resultados, sin error.

## Resultado Obtenido

- `searchresults.cfm` devolvió 127 resultados.
- Las primeras tarjetas fueron Toyota FORTUNER 2007, Toyota FORTUNER 2008 y Toyota FORTUNER SRV 2009.

## Estado de la prueba

✅ Pasó

## Observaciones

- No se produjo página de error.

---

# Caso de Prueba: Ordenar resultados por año

## ID

CT-BUS-004

## Objetivo

Verificar que **Ordenar por: Año** deje el listado visible en orden ascendente.

## Precondiciones

- Catálogo de Autos Usados abierto.

## Datos de Entrada

- Ordenar por: Año.
- Sin filtros adicionales.

## Pasos

1. Seleccionar **Año** en Ordenar por.
2. Presionar **BUSCAR**.
3. Comparar los años de las primeras tarjetas.

## Resultado Esperado

- El listado queda ordenado ascendentemente por año y sus tarjetas siguen accesibles.

## Resultado Obtenido

- El listado cargó y las tarjetas fueron accesibles, pero no quedó en orden ascendente.
- La primera tarjeta fue Chevrolet C20 1966 y la segunda Jeep WILLYS OVERLAND M38 1960; luego se mostraron vehículos de 1960 y 1962.

## Estado de la prueba

❌ Falló

## Observaciones

- Debe reportarse como defecto de ordenación o aclararse un criterio secundario que justifique la secuencia.

## Resumen de ejecución

| Caso | Resultado obtenido | Estado |
|---|---|---|
| CT-BUS-001 | Catálogo y filtros públicos disponibles. | ✅ Pasó |
| CT-BUS-002 | 69 Toyota 2024; primer resultado FORTUNER. | ✅ Pasó |
| CT-BUS-003 | 127 coincidencias FORTUNER. | ✅ Pasó |
| CT-BUS-004 | 1966 seguido de 1960 al ordenar por Año. | ❌ Falló |
