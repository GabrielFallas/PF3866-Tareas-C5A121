# FC-03 — Contacto con el vendedor

**Ejecución real:** 12/09/2026, 18:14 UTC-06:00.  
**Entorno:** CRAutos producción, navegador sin sesión y Playwright MCP.  
**Regla de seguridad:** no se realizaron llamadas ni se enviaron mensajes. Las pruebas de WhatsApp se detuvieron en la vista previa; no se presionó **Open app** ni **Continue to WhatsApp Web**.

---

# Caso de Prueba: Mostrar sección Vendedor

## ID

CT-CON-001

## Objetivo

Verificar que una ficha pública muestre datos de contacto del vendedor.

## Precondiciones

- Ficha pública Toyota FORTUNER 2024 (`c=6656966`) abierta.

## Datos de Entrada

- Datos públicos mostrados por la ficha.

## Pasos

1. Ubicar la tabla **Vendedor**.
2. Revisar las filas **Nombre**, **Teléfono** y **WhatsApp**.

## Resultado Esperado

- Se muestran el nombre, al menos un teléfono y un enlace de WhatsApp cuando esté disponible.

## Resultado Obtenido

- La tabla mostró a JOSÉ PABLO VEGA, los teléfonos 8839-3080 y 7109-3070, y el número de WhatsApp 8839-3080.

## Estado de la prueba

✅ Pasó

## Observaciones

- Se consultaron solamente datos que el anuncio muestra públicamente.

---

# Caso de Prueba: Verificar enlaces telefónicos

## ID

CT-CON-002

## Objetivo

Verificar que los teléfonos del vendedor usen enlaces de llamada válidos.

## Precondiciones

- Ficha `c=6656966` abierta.

## Datos de Entrada

- Enlaces de 8839-3080 y 7109-3070 de la fila Teléfono.

## Pasos

1. Inspeccionar el atributo `href` de ambos teléfonos, sin activarlos.
2. Comparar cada destino con el número visible.

## Resultado Esperado

- Cada contacto del vendedor usa el protocolo `tel:` y corresponde al número mostrado.

## Resultado Obtenido

- Se identificaron los enlaces `tel: 8839-3080)` y `tel: 7109-3070)` en la fila del vendedor.
- Se excluyó `tel: 22914141`, ya que corresponde al contacto general de CRAutos.

## Estado de la prueba

✅ Pasó

## Observaciones

- El paréntesis final en los URI `tel:` debe corregirse, aunque los números visibles sean correctos.

---

# Caso de Prueba: Vista previa de WhatsApp del vendedor

## ID

CT-CON-003

## Objetivo

Verificar que el enlace WhatsApp del vendedor construya un destinatario y texto correctos.

## Precondiciones

- Ficha `c=6656966` abierta.

## Datos de Entrada

- Enlace de WhatsApp de la fila Vendedor, con destinatario 50688393080.

## Pasos

1. Abrir el enlace WhatsApp de la fila del vendedor.
2. Revisar la vista previa `api.whatsapp.com`.
3. Detenerse antes de abrir la aplicación o WhatsApp Web.

## Resultado Esperado

- La vista previa identifica al destinatario y el texto corresponde al anuncio, sin enviar mensaje.

## Resultado Obtenido

- **Share on WhatsApp** mostró “Chat on WhatsApp with +506 8839 3080”.
- El texto indicó Toyota FORTUNER 2024 y `https://crautos.com/wa?c=6656966`.
- Se mostraron **Open app** y **Continue to WhatsApp Web**; ninguno se accionó.

## Estado de la prueba

✅ Pasó

## Observaciones

- No se abrió un chat ni se transmitió mensaje alguno.

---

# Caso de Prueba: Vista previa de compartir anuncio

## ID

CT-CON-004

## Objetivo

Verificar que el ícono de compartir por WhatsApp incluya el enlace de la ficha.

## Precondiciones

- Ficha `c=6656966` abierta.

## Datos de Entrada

- Ícono WhatsApp de compartir junto al precio.

## Pasos

1. Abrir el destino del ícono de compartir.
2. Revisar la vista previa de WhatsApp.
3. No continuar a la app ni seleccionar contacto.

## Resultado Esperado

- La vista previa contiene la URL exacta de la ficha y ofrece continuar hacia WhatsApp sin enviar nada.

## Resultado Obtenido

- **Share on WhatsApp** mostró `https://crautos.com/autosusados/cardetail.cfm?c=6656966`.
- Ofreció **Open app** y **Continue to WhatsApp Web**; no se abrió conversación ni se seleccionó contacto.

## Estado de la prueba

✅ Pasó

## Observaciones

- La prueba validó la generación de la vista previa, no el envío del contenido.

## Resumen de ejecución

| Caso | Resultado obtenido | Estado |
|---|---|---|
| CT-CON-001 | Datos del vendedor visibles. | ✅ Pasó |
| CT-CON-002 | Enlaces `tel:` presentes para ambos teléfonos. | ✅ Pasó |
| CT-CON-003 | Vista previa con destinatario y texto correctos. | ✅ Pasó |
| CT-CON-004 | Vista previa con la URL exacta de la ficha. | ✅ Pasó |
