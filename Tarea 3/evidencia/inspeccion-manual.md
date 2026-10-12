# Inspección manual complementaria a los reportes de axe (salida literal de la consola del navegador)

Fecha: 2026-10-04. Navegador integrado de la app Claude (Chromium 152, Windows 11), viewport 1280×800 salvo que se indique otro. Cada bloque es el resultado que devolvió la consola; solo se omitió texto de teléfonos personales.

## Anuncie su auto — `https://crautos.com/autosusados/anunciarse.cfm`

### Estructura del formulario

```json
{"h":["H1: Anuncie su auto","H4: La Página de Autos de Costa Rica","H4: Contáctanos"],
 "secs":["Datos Generales","Equipamiento","Sus Datos:","Los siguientes servicios son opcionales,"],
 "terms":[{"href":"terms.htm","img":"images/terms.jpg","text":""},{"href":"terms2.htm","img":"images/terms2.jpg","text":""}],
 "optionCtx":"NO deseo esta opción - ¢ 0 SI deseo esta opción - ¢ 2,260",
 "optionRadios":38,"fieldsets":0,"labels":0,"required":0,"autocomplete":0,
 "alertCalls":20,"onsubmit":"return validate()","asterisks":0,"inputCount":114}
```

## Ficha del anuncio — `https://crautos.com/autosusados/cardetail.cfm?c=20483869`

```json
{"h1count":2,
 "heads":["H1: Nissan FRONTIER 2016","H1: ¢ 12,300,000","H3: ($ 26,739)*","H3: Cuota $ 391/mes","H6: GALERIA DE FOTOS","H4: La Página de Autos de Costa Rica","H4: Contáctanos"],
 "shares":[{"href":"https://www.facebook.com/sharer/sharer.php?u=https","img":"images/FB-share.png","alt":"","text":""},
           {"href":"https://api.whatsapp.com/send?text=%20https://crau","img":"images/WA-share.png","alt":"","text":""}],
 "contact":[{"kind":"mailto","hasText":true},{"kind":"tel","hasText":true},{"kind":"tel","hasText":true},{"kind":"whatsapp","hasText":true},{"kind":"mailto","hasText":true}],
 "gallery":{"imgs":11,"alts":[""],"titles":[""],"ariaLive":0,"navLinks":11,"namedNav":0},
 "tableResp":[false,false,false,false,false,false,false]}
```

Prueba adicional en un viewport de 800×600 (2026-10-04 23:30 UTC): `axe.run` con la regla `scrollable-region-focusable` devolvió 0 violaciones, y los 7 contenedores `.table-responsive` midieron `scrollWidth/clientWidth` = 696/696, 695/696, 696/696, 336/336, 336/336, 0/0 y 0/0, es decir, ninguno desbordaba (ver [hallazgos descartados](../README.md#hallazgos-descartados)).

## Catálogo, vista móvil (375×812) — `https://crautos.com/autosusados/index.cfm`

Inspección de una tarjeta de vehículo (`table.carbox`):

```json
{"links":[{"href":"sados/cardetail.cfm?c=93323081","text":"","hasImg":true},
          {"href":"sados/cardetail.cfm?c=93323081","text":"Honda CRV 2020 ¢ 14,260,000 ($31,000)* 1500cc | Automático | Gasolina ","hasImg":true}],
 "cardsWithEmptyAndNamedLink":44,"totalCards":44}
```

## Catálogo, vista de escritorio (1280×800)

```json
{"objAttrs":{"type":"text/html","data":"/autosusados/showpicfeatures.cfm?f=93323081-t.jpg&c=93323081","title":null,"aria":null,"inner":""},
 "objCount":62,
 "cardText":"Honda CRV - 2020 Automático - 5 pas. ¢ 14,260,000 ($31,000)*"}
```

## Resultados de búsqueda (1280×800)

```json
{"cbParent":"<span class=\"pull-right\" font=\"font\"><input type=\"checkbox\" name=\"c\" value=\"42124378\" onclick=\"javascript:event.stopImmediatePropagation();\"></span>",
 "demoCtx":"Para comparar 2 ó más vehículos, marque el cuadro () localizado en la esquina de",
 "cardLinks":[{"href":"cardetail.cfm?c=42124378","text":"Toyota COROLLA 1988 • 5 Pas. Combustible: Gasolina Color Exterior: GRIS ¢ 400,000 ($ 870)* Cilindrada: 1300 cc"}],
 "marquee":{"text":"Carro para proyecto esta detenido por falta de uso pero esta al dia co","behavior":null,"scrollamount":"3"}}
```

## Imágenes inspeccionadas visualmente

Al abrir cada archivo de imagen en el navegador: `option3-56.gif` es una barra naranja plana de 140×17 px (sin texto) y `financeicon.png` es un icono rojo de 64×50 px.

## Rótulos visibles junto a cada control (leídos del DOM)

Para cada control se tomó el texto de la celda vecina anterior (`td.previousElementSibling.innerText`) o, si no existía, el texto de su fila.

### Catálogo — `searchform` (1280×800)

```json
{"brand":"Marca:","modelstr":"Modelo:","style":"Estilo:","fuel":"Combustible:","trans":"Transmisión:","financed":"Financiado:","recibe":"Se recibe:","province":"Provincia:","doors":"# puertas:","yearfrom":"Año Entre:","yearto":"2027 2027 2026 2025 2024 2023 2022 2021 2020 2019 ","pricefrom":"Precio Entre:","priceto":"Sin Límite 1,000,000 2,000,000 3,000,000 4,000,000","orderby":"Ordenar por:","newused":"*Mostrar:","splitmode":"Utilizar modo SPLIT"}
```

`document.searchform.querySelectorAll('label').length` devolvió `0`.

(`yearto` y `priceto` no tienen rótulo propio: el texto vecino son sus propias opciones.)

### Anuncie su auto (1280×800)

```json
{"marca":"Marca:","modelo":"Modelo:","cilindrada":"Cilindrada:","estilo":"Estilo:","numpas":"Número de pasajeros:","ano":"Año:","estado":"Estado:","precio":"Precio (¢): (Hoy: ¢460.00 / $1)","negotiable":"Precio es Negociable:","color":"Color Exterior:","color2":"Color Interior:","mileage":"Kilometraje:","tag":"Placa: (Ingresar número completo)","registered":"Ya pagó impuestos:","recibe":"Se recibe vehículo?:","combustible":"Combustible:","transmision":"Transmisión:","numdoors":"Número de puertas:","province":"Provincia:","comment":"Comentario adicional: (no poner números de teléfono en el co","nombre":"Nombre:","email":"E-mail:","email2":"Confirmar E-mail:","tel1":"Teléfono 1:","tel2":"Teléfono 2:","tel3":"Teléfono 3:","whatsapp":"Teléfono Whatsapp:","acceptrules":"Acepto que he leído los Términos y Condiciones de Uso y el A"}
```

## Catálogo — títulos en imagen y encabezados (1280×800)

```json
{"destacados":{"src":"/autosusados/images/destacados.png","parent":"TD","inHeading":false,"inLink":false,"w":"267x30"},
 "vendedores":{"src":"/autosusados/images/destacadosdevendedores.png","parent":"TD","inHeading":false,"inLink":false,"w":"342x32"},
 "searchtitle":{"src":"/autosusados/images/searchtitle.png","parent":"DIV","inHeading":false,"inLink":false,"w":"270x22"},
 "headings":["H1: Autos Usados","H4: La Página de Autos de Costa Rica","H4: Contáctanos"]}
```
