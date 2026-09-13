# Funcionalidades críticas seleccionadas

La selección se deriva del flujo principal documentado en la Tarea 1: una persona compradora busca, revisa y contacta; una persona vendedora publica y edita. Se eligieron cuatro funciones cuyo fallo interrumpe ese flujo o reduce de manera importante la oferta disponible o la generación de contactos para el negocio.

| ID | Funcionalidad | Por qué es crítica | Riesgo si falla |
|---|---|---|---|
| CT-01 | Búsqueda y listado de vehículos | Es la puerta de entrada al inventario y permite descubrir vehículos relevantes. | La persona compradora no encuentra opciones y se pierde tráfico/leads. |
| CT-02 | Detalle y galería del anuncio | Entrega la información con la que la persona compradora compara y decide sobre un vehículo. | Decisiones con datos incompletos o erróneos; pérdida de confianza. |
| CT-03 | Contacto con el vendedor | Convierte el interés en una oportunidad de negociación. | No se generan contactos ni oportunidades de venta. |
| CT-04 | Publicación y edición de anuncios | Mantiene disponible y actualizada la oferta que alimenta el mercado. | Los vendedores no pueden crear o corregir anuncios; el inventario disminuye o se degrada. |

## Criterio de priorización

Cada funcionalidad está directamente conectada con la propuesta de valor de CRAutos: reunir oferta de vehículos y facilitar que comprador y vendedor se encuentren. La exploración real mostró que **Anuncie Su Auto** abre un formulario público y que **Edite Su Anuncio** solicita el código y la clave del anuncio; por ello se prueba ese flujo, no un supuesto dashboard autenticado.

La compra no se incluye como funcionalidad interna porque, según la Tarea 1, la negociación y la transacción se concretan fuera de la plataforma. El contacto, en cambio, sí es la acción de negocio que CRAutos debe garantizar dentro de su sitio.

## Evidencia de la ejecución actual

La ejecución de producción del 12/09/2026 confirmó que las cuatro funciones están expuestas públicamente y pueden recorrerse sin sesión. Quince casos pasaron, incluidas las validaciones de publicación, y falló la ordenación por Año. El detalle verificable de cada caso está en los cuatro documentos `smoke-*.md` enlazados desde el índice.
