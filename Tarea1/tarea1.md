# Evaluación: Tarea 1

Estudiante: Gabriel Isaías Fallas López

Curso de Pruebas de Software PF3866

Universidad de Costa Rica


## Información general del sistema
- **Nombre del sistema:** crautos
- **Dirección**: [crautos.com](crautos.com)
- **Logo:** ![logo](image.png)
- **Propósito del sistema:** La página de crautos.com es un sitio de compra y venta de vehículos enfocado en el mercado costarricense, el cual se ha posicionado como una de las opciones favoritas para encontrar fácilmente un vehículo específico según sea la marca, el modelo, el año, el color, el tipo, el precio, etc. Han existido nuevas plataformas con interfaces más modernas, pero no han logrado posicionarse al mismo nivel. Se puede notar que la página actual aún conserva un estilo anticuado para la época actual, además de numerosos problemas de accesibilidad, experiencia de usuario, estabilidad y velocidad.

- **¿Qué problema resuelve?**: Permite que las personas en Costa Rica cuenten con un lugar fácil de acceder, ya sea desde una computadora o un dispositivo móvil, a un mercado amplio y diverso de compra y venta de vehículos.

- **¿Cuál es su público objetivo?:** 
  - Compradores de vehículos usados y nuevos en Costa Rica
  - Vendedores particulares y concesionarios de automóviles
  - Personas que buscan comparar precios, modelos y características de vehículos
  - Usuarios de diferentes rangos de edad con acceso a internet

- **¿Cuál es el flujo de uso esperado más común?:**
  - El usuario accede a crautos.com y realiza una búsqueda de vehículos filtrando por marca, modelo, año, precio y otras características
  - Visualiza los resultados de la búsqueda con imágenes, precio y descripción de cada vehículo
  - Selecciona un vehículo de interés para ver detalles completos, especificaciones, historial y galería de fotos
  - Contacta al vendedor a través de los medios de comunicación disponibles en la plataforma (teléfono, correo, WhatsApp)
  - Concreta la negociación y compra del vehículo fuera de la plataforma

---

## 1. Accesibilidad Inicial y Carga

- **El sitio carga correctamente (sin errores de carga o fallos visibles):** La página principal carga sin errores visibles, aunque presenta cierta lentitud. No se muestran pantallas en blanco ni mensajes de error críticos.

- **El contenido principal aparece rápidamente (menos de 5 segundos):** Sí, aunque existen áreas de mejora como el tiempo de carga lento de algunos elementos como las imágenes.

- **No hay errores evidentes (mensajes técnicos, 404, pantallas en blanco):** Se pueden observar ocasionalmente elementos no cargados correctamente en dispositivos móviles, pero en general no hay errores 404 o pantallas en blanco en la navegación básica.

- **El sitio es responsivo (se adapta a pantallas móviles/tablets):** La página se adapta a pantallas móviles, tablets y escritorio, aunque el diseño móvil podría mejorarse significativamente para una mejor experiencia del usuario.

## 2. Navegación General

- **El menú principal es visible y funcional:** El menú de navegación superior está disponible y permite acceder a las secciones principales (Inicio, Autos Nuevos, Autos Usados, Contáctenos, Anuncie su auto y Edite su anuncio).

- **Los enlaces llevan a las páginas correctas:** La mayoría de los enlaces funcionan correctamente.

- **El botón "Inicio" o logo lleva a la página principal:** El logo de crautos en la esquina superior izquierda redirige correctamente a la página de inicio.

- **Hay forma de volver atrás fácilmente o de reiniciar una acción:** Se puede utilizar el botón atrás del navegador, aunque la navegación por breadcrumbs no está claramente implementada en todas las secciones.

## 3. Flujos Críticos

- **Registro de usuario (campos obligatorios, validación, éxito):** Campos obligatorios incluyen nombre, correo electrónico y contraseña. El sistema valida campos como formato de correo, fortaleza de contraseña, nombre, apellidos, identificación, país, fecha de nacimiento, sexo, dirección física y ciudad. Tras registro exitoso, se envía confirmación por correo electrónico.

- **Inicio de sesión / recuperación de contraseña:** Inicio de sesión con correo y contraseña. Recuperación de contraseña mediante enlace enviado al correo registrado funciona correctamente.

- **Cierre de sesión correcto:** El usuario puede cerrar sesión desde el menú de su cuenta, redirigiendo correctamente a la página de inicio sin acceso a secciones privadas.

- **Creación o envío de datos (formularios, publicaciones, etc.):** Vendedores pueden crear anuncios con fotografías, descripción, precio y datos del vehículo. El sistema valida campos obligatorios antes de permitir la publicación.

- **Edición de datos existentes (perfil, configuraciones):** Los usuarios pueden editar su perfil, datos de contacto y anuncios publicados sin dificultad.

- **Proceso de pago / reserva / acción principal del sistema:** Los compradores pueden contactar al vendedor a través de múltiples canales (WhatsApp, teléfono, correo) integrados en la plataforma para negociar y concretar la compra fuera de ella.

## 4. Formularios y Validaciones

- **Los campos requeridos están claramente marcados:** Los campos obligatorios en formularios de registro y creación de anuncios no están identificados con asteriscos (*) ni cambian a un color rojo al no estar correcto el dato suministrado.

- **El sistema valida entradas incorrectas (email inválido, números, etc.):** Sí, pero solo se indica mediante una alerta que referencia un campo a la vez luego de presionar el botón de confirmación.

- **Mensajes de error son comprensibles y útiles:** Los mensajes de validación son generalmente claros, aunque algunos podrían ser más descriptivos y específicos.

- **Se pueden corregir errores sin reiniciar todo el formulario:** Los errores se destacan en los campos correspondientes, permitiendo correcciones locales sin perder datos ingresados.

- **Los mensajes de éxito aparecen correctamente:** Al enviar formularios exitosamente, se redirige a otra página confirmando la acción completada.

## 5. Contenido y Usabilidad

- **Textos sin errores ortográficos o gramaticales:** El contenido general está bien redactado, aunque ocasionalmente se encuentran pequeños errores tipográficos en descripciones proporcionadas por usuarios.

- **Botones y enlaces tienen nombres claros y consistentes ("Guardar", "Cancelar", etc.):** Botones como "Buscar", "Anuncie su auto", "Contáctenos" son claros y descriptivos en toda la plataforma.

- **Las acciones del usuario tienen retroalimentación (mensajes, animaciones tipo loaders):** La mayoría de las acciones (búsquedas, filtros, publicación de anuncios) proporcionan retroalimentación visual clara. Sin embargo, no existen animaciones que mejoren la experiencia del usuario.

- **No se requieren pasos innecesarios o confusos:** El flujo principal de búsqueda y contacto es directo, pero altamente mejorable en cuanto a su diseño.

- **El sistema es intuitivo sin necesidad de instrucciones externas:** Los usuarios familiarizados con plataformas similares pueden navegar sin dificultad, aunque nuevos usuarios pueden requerir orientación en funcionalidades avanzadas. Es moderadamente intuitivo.

## 6. Compatibilidad Básica

- **Probar en al menos dos navegadores (Chrome, Firefox, Edge, Safari):**
  - Chrome (versión actual): funciona correctamente
  - Safari (versión actual): funciona, pero con algunos problemas de visualización de ciertos elementos, principalmente las imágenes que tardan bastante en cargar.

- **Probar en dispositivo móvil vs escritorio (modo responsivo o dispositivo real):**
  - Escritorio (1920x1080): experiencia óptima
  - Tablet: modo responsivo funciona adecuadamente
  - Móvil: funciona pero con ciertos elementos que no se adaptan correctamente

- **Probar en resolución más baja (ej. 1024x768) y más alta:**
  - Resolución baja (1024x768): contenido se adapta, pero algunos elementos pueden estar muy comprimidos
  - Resolución alta (2560x1440): diseño se mantiene, sin problemas de escalado

## 7. Manejo de Errores y Casos Límite

- **¿Qué ocurre si el usuario deja todo un formulario vacío?**
  El navegador muestra alertas de error indicando que los campos obligatorios deben completarse y no permite enviar el formulario.

- **¿Qué pasa si introduce datos absurdos (nombre de 1000 caracteres, símbolos raros)?**
  - Nombres de 1000 caracteres: el sistema puede aceptar pero trunca la visualización
  - Símbolos especiales en campos de texto: algunos símbolos pueden causar problemas en la validación y otros son eliminados directamente en el campo al tratar de escribirlos
  - Precios negativos: no se valida adecuadamente en algunos casos
  - Precios con decimales: no es permitido ya que se manejan en colones

- **¿Qué ocurre si se recarga la página durante una acción?**
  Los datos de formularios incompletos se pierden. No hay recuperación automática de sesión en algunos casos.

- **¿Cómo responde el sistema si se pierde la conexión a Internet?**
  El navegador muestra un mensaje genérico de error. No hay almacenamiento en caché para permitir navegación offline completa de contenido previamente cargado; la que existe es limitada.

## 8. Seguridad Básica Visible (sin análisis técnico)

- Las contraseñas no se ven mientras se escriben: El campo de contraseña oculta los caracteres de forma predeterminada. No hay un icono para mostrar/ocultar la contraseña cuando el usuario lo desee.

- No se puede navegar hacia páginas privadas sin haber iniciado sesión: Al intentar acceder a secciones como Editar su anuncio sin estar autenticado, el sistema redirige a una vista preguntando por el Código de anuncio y la clave.

- El usuario no puede ver información de otros usuarios: El sistema solo revela el nombre completo del vendedor en el anuncio. No existe manera de acceder a información privada de otros usuarios ni de conocer qué otros anuncios han publicado.

- Después de cerrar sesión, no puedes volver con el botón atrás: Sí es posible mediante el botón de atrás del navegador, aunque el sistema no muestra información sensible y redirige eventualmente a la página de inicio de sesión.

## 9. Feedback y Soporte

- Los mensajes de ayuda, tooltips o instrucciones están presentes (si aplica): No existen ayudas contextuales en los formularios ni tooltips que guíen al usuario en la correcta utilización de los campos. En ocasiones hay descripciones al lado de los campos.

- Hay términos y condiciones / políticas de privacidad visibles (si aplica): No están disponibles en el pie de página del sitio. La política de privacidad no es accesible claramente. La plataforma proporciona contacto a través de correo electrónico y número de teléfono. No hay chat en vivo ni soporte por teléfono.

## 10. Aspecto General y Estabilidad

- Diseño consistente entre secciones: El diseño es generalmente consistente, aunque se nota la influencia de diferentes épocas de desarrollo. Algunos estilos son anticuados y no reflejan estándares modernos.

- Imágenes y elementos visuales se cargan correctamente: Las imágenes de vehículos se cargan correctamente, aunque en ocasiones pueden tardar considerablemente.

- El sitio no se desajusta al hacer zoom: El zoom out y el zoom in funcionan correctamente sin desajustes significativos en el diseño.

- No hay pantallas muertas sin contenido o acción clara: Todas las páginas principales tienen contenido claro y elementos interactivos disponibles para el usuario.
