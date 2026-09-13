# FC-04 — Publicación y edición de anuncios

**Ejecución real:** 12/09/2026, 18:25 UTC-06:00.  
**Entorno:** CRAutos producción, navegador sin sesión y Playwright MCP; para las alertas JavaScript se usó también el árbol de accesibilidad del navegador.

**Límite de seguridad:** no se publicó, editó ni eliminó ningún anuncio real; no se subieron imágenes, no se llegó a una pantalla de pago ni se introdujeron datos personales.

---

# Caso de Prueba: Abrir el formulario Anuncie su auto

## ID

CT-PUB-001

## Objetivo

Verificar que el acceso **Anuncie Su Auto** abra el formulario público de publicación.

## Precondiciones

- Navegador con conexión a Internet y sin sesión iniciada.
- Página pública de CRAutos disponible.

## Datos de Entrada

- Enlace **Anuncie Su Auto**.

## Pasos

1. Abrir `https://crautos.com/autosusados/anunciarse.cfm` desde el acceso **Anuncie Su Auto**.
2. Revisar el título y la sección **Datos Generales**.
3. Confirmar los controles y el botón **Continuar**.

## Resultado Esperado

- Carga el formulario de alta con el título **Anuncie su auto**.
- Están disponibles los datos generales del vehículo y el control para continuar.

## Resultado Obtenido

- Cargó `anunciarse.cfm` con el título y la sección esperados.
- El formulario envía a `anunciarse2.cfm` y contiene Marca, Modelo, Cilindrada, Estilo, Número de pasajeros, Año, Estado, Precio, Kilometraje, Placa, Provincia, Comentario, equipamiento, datos de contacto, opciones pagas, aceptación de términos y **Continuar**.
- El sitio indica que el precio debe ser el total en colones y que no se incluyan teléfonos en el comentario.

## Estado de la prueba

✅ Pasó

## Observaciones

- Se verificó únicamente la interfaz; no se completó ni envió la publicación.

---

# Caso de Prueba: Validar campos iniciales vacíos

## ID

CT-PUB-002

## Objetivo

Verificar que el formulario bloquee el avance cuando **Marca** permanece sin seleccionar.

## Precondiciones

- Formulario **Anuncie su auto** abierto.
- Sin modificar los campos.

## Datos de Entrada

- Marca con el valor inicial `Seleccione la Marca`.

## Pasos

1. Mantener el formulario sin datos.
2. Presionar **Continuar** una vez.
3. Registrar el mensaje de validación y confirmar que no se navega a `anunciarse2.cfm`.

## Resultado Esperado

- El formulario no avanza.
- Se muestra un mensaje claro para el primer campo obligatorio pendiente.

## Resultado Obtenido

- La acción mostró la alerta JavaScript: **“Por favor seleccione la marca.”**
- El navegador permaneció en `anunciarse.cfm`; no se creó un anuncio ni hubo navegación posterior.

## Estado de la prueba

✅ Pasó

## Observaciones

- El clic inicial mediante el localizador de Playwright quedó interrumpido por el diálogo. La activación mediante el árbol de accesibilidad permitió capturar el mensaje real.

---

# Caso de Prueba: Validar la placa obligatoria

## ID

CT-PUB-003

## Objetivo

Verificar que el formulario exija una placa antes de permitir continuar.

## Precondiciones

- Formulario **Anuncie su auto** abierto.
- Ningún dato personal, servicio pagado ni opción de publicación automática seleccionado.

## Datos de Entrada

- Marca: Toyota.
- Modelo: PRUEBA QA.
- Cilindrada: 1 800 cc.
- Estilo: Sedán.
- Número de pasajeros: 5.
- Año: 2024.
- Precio: ¢1 000 000.
- Placa: vacía.

## Pasos

1. Completar los controles con los valores ficticios indicados.
2. Dejar vacío el campo **Placa**.
3. Presionar **Continuar** una vez.
4. Registrar la alerta y confirmar que el formulario no avanzó.

## Resultado Esperado

- El sistema impide continuar y solicita el número de placa.
- No se publica el anuncio.

## Resultado Obtenido

- La alerta JavaScript observada fue: **“Por favor ingrese el número de placa y asegúrese de ingresarlo correctamente.”**
- El foco quedó en `tag` (Placa), cuyo valor continuó vacío, y la URL siguió siendo `anunciarse.cfm`.
- No hubo publicación, datos personales ni pago.

## Estado de la prueba

✅ Pasó

## Observaciones

- Los valores usados fueron ficticios y el caso se detuvo en la primera alerta aplicable.

---

# Caso de Prueba: Rechazar credenciales inválidas de edición

## ID

CT-PUB-004

## Objetivo

Verificar que la edición rechace un código y una clave inexistentes.

## Precondiciones

- Pantalla pública **Editar Anuncio** disponible.

## Datos de Entrada

- Código: `00000000`.
- Clave: `clave-ficticia`.

## Pasos

1. Abrir `https://crautos.com/anuncios/`.
2. Ingresar el código y la clave ficticios.
3. Presionar **Continuar**.

## Resultado Esperado

- No se abre una edición de anuncio.
- Se informa que las credenciales no son válidas.

## Resultado Obtenido

- Se cargó `https://crautos.com/anuncios/editcar.cfm`.
- El sitio mostró exactamente: **“No existe ningún anuncio con este código y clave.”**
- No se modificó ningún anuncio.

## Estado de la prueba

✅ Pasó

## Observaciones

- La pantalla de origen aclara que solo se puede editar un anuncio publicado.

## Resumen de ejecución

| Caso | Resultado obtenido | Estado |
|---|---|---|
| CT-PUB-001 | Formulario de publicación completo en `anunciarse.cfm`. | ✅ Pasó |
| CT-PUB-002 | Alerta de Marca observada; no avanzó el formulario. | ✅ Pasó |
| CT-PUB-003 | Alerta de Placa observada; no avanzó el formulario. | ✅ Pasó |
| CT-PUB-004 | Rechazo de código y clave ficticios en `editcar.cfm`. | ✅ Pasó |
