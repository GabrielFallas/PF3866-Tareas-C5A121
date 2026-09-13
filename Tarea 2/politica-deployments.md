# Política de validación para nuevos deployments

## Resultado de la ejecución documentada

La ejecución de producción del 12/09/2026 registró 15 casos aprobados y un fallo (`CT-BUS-004`). No equivale a la aprobación de un deployment porque fue una comprobación del sitio público existente, no de un build identificado. Antes de una liberación, se debe repetir la batería en el ambiente y la versión específicos del release, y resolver el problema de ordenamiento por Año o clasificarlo formalmente.

## Momento y responsable

1. Ejecutar los 16 smoke tests de esta carpeta después del despliegue y antes de anunciar el release como disponible.
2. La persona responsable de QA registra para cada caso: fecha/hora, ambiente, navegador/dispositivo, resultado, evidencia y defecto asociado.
3. Usar datos de vehículo, código y clave de anuncio de prueba autorizados para los casos de publicación y edición. Nunca contactar a un vendedor real ni publicar información real durante el smoke test.

## Prioridad de los casos

Los casos de prioridad alta cubren el recorrido principal y las validaciones esenciales:

| Prioridad | Casos |
|---|---|
| Alta | `CT-BUS-001`, `CT-BUS-002`, `CT-DET-001`, `CT-DET-002`, `CT-CON-001`, `CT-CON-003`, `CT-PUB-001`, `CT-PUB-003` |
| Media | `CT-BUS-003`, `CT-BUS-004`, `CT-DET-003`, `CT-DET-004`, `CT-CON-002`, `CT-CON-004`, `CT-PUB-002`, `CT-PUB-004` |

## Criterio de aprobación

Un deployment es **válido** únicamente si pasa el **100 % de los casos de prioridad alta** y al menos el **95 % de la totalidad de smoke tests**. Como esta batería contiene 16 casos, el mínimo entero que cumple el 95 % es 16 casos: 15/16 equivale a 93,75 %. Por lo tanto, para esta batería deben pasar los 16 casos (100 %).

| Resultado | Decisión |
|---|---|
| Falla un caso de prioridad alta | **Rechazar/pausar el deployment.** Abrir defecto crítico, comunicar al equipo y aplicar rollback o corrección inmediata según el plan operativo. Repetir toda la batería luego de corregir. |
| Falla una o más pruebas de prioridad media | **Rechazar/pausar el deployment bajo el criterio estándar de esta batería.** Investigar, corregir y repetir las pruebas afectadas y las relacionadas. |
| Todas pasan | **Aprobar el deployment.** Conservar evidencia y monitorear errores y contactos durante la primera hora. |

## Gestión de fallas

Al fallar una prueba, se debe capturar evidencia (captura, URL, datos de prueba y pasos), clasificar la severidad, crear el defecto y notificar al equipo de desarrollo o release. No se debe aprobar un deployment corregido sin verificarlo nuevamente: el caso fallido y los casos relacionados deben volver a ejecutarse. Si no existe rollback, la función afectada se deshabilita temporalmente solo si esa medida protege al usuario y cuenta con la aprobación de la persona responsable del release.
