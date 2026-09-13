# Tarea 2 — Secciones críticas y smoke tests de CRAutos

**Estudiante:** Gabriel Isaías Fallas López  
**Curso:** PF3866 — Pruebas de Software  
**Sistema:** [crautos.com](https://crautos.com)  
**Fecha de ejecución:** 12 de setiembre de 2026, 18:25 (UTC-06:00)

## Índice

1. [Funcionalidades críticas seleccionadas](funcionalidades-criticas.md)
2. [Smoke tests: búsqueda y resultados](smoke-busqueda.md)
3. [Smoke tests: detalle del anuncio](smoke-detalle-anuncio.md)
4. [Smoke tests: contacto con vendedor](smoke-contacto-vendedor.md)
5. [Smoke tests: publicación y edición de anuncios](smoke-acceso-publicacion.md)
6. [Política de validación para deployments](politica-deployments.md)

## Alcance y método de la evidencia

Los 16 casos se ejecutaron contra la aplicación de producción de crautos.com, desde un navegador sin sesión. Se recorrieron el catálogo y sus filtros, un resultado activo, su ficha, la galería, los enlaces de contacto, las vistas previas de WhatsApp, el formulario **Anuncie su auto** y la pantalla **Editar anuncio**.

No se realizaron llamadas ni se enviaron mensajes. Tampoco se abrió un chat de WhatsApp, se publicó un vehículo, se subieron archivos ni se llegó a una página de pago. Para las pruebas de publicación se utilizaron únicamente valores ficticios y se dejó la placa vacía; por ello, el flujo se detuvo antes de crear un anuncio.

## Resumen de ejecución

| Estado | Casos |
|---|---:|
| ✅ Pasó | 15 |
| ❌ Falló | 1 |

El único fallo es `CT-BUS-004`: al seleccionar **Año**, el primer resultado visible fue 1966 y el siguiente 1960, por lo que el listado no quedó ordenado ascendentemente. `CT-PUB-002` mostró el mensaje “Por favor seleccione la marca.” y `CT-PUB-003` mostró la alerta relacionada con la placa; ambos casos permanecieron en el formulario sin crear un anuncio. Según la política definida, 15 de 16 casos (93,75 %) no alcanzan el mínimo del 95 % para aprobar un deployment.
