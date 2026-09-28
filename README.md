# Proyecto Ventas POLI — Entrega 2

Primera versión web de las mejoras propuestas, hecha con HTML, CSS,
JavaScript y la librería jQuery. Se puede ver en cualquier navegador
abriendo index.html, sin instalar software adicional.

## Páginas
- index.html: resumen de ventas y ranking de vendedores
- productos.html: listado con búsqueda, orden y descarga de productos.txt
- vendedores.html: listado con búsqueda, orden y descarga de vendedores.txt
- ventas.html: detalle de ventas por vendedor y descarga de su archivo

## Sitio publicado
https://areiza-zenith.github.io/ProyectoVentasPOLI-web/

##Explicación del código
Version web de mi primera entrega en java
Aquí JavaScript genera los mismos datos, jQuery los muestra en 4 páginas, y el usuario puede descargar los .txt
index.html      → resumen y ranking
productos.html  → tabla de productos
vendedores.html → tabla de vendedores
ventas.html     → ventas de cada vendedor
css/style.css   → diseño
js/app.js       → toda la lógica (jQuery)

Las 4 páginas comparten el mismo app.js. Cada una le dice al script qué página es, y el script ejecuta solo la parte que corresponde.

##HTML
Todas las páginas tienen la misma estructura:
<body data-page="productos">
  <header> ...título, menú, botón "Regenerar datos"... </header>
  <main> ...contenido propio de cada página... </main>
  <footer>...</footer>
  <script src="...jquery.min.js"></script>
  <script src="js/app.js"></script>
</body>
data-page="productos": es un atributo personalizado. jQuery lo lee con $('body').data('page') para saber en qué página está.
<nav>: los 4 enlaces del menú.
Tablas vacías: el HTML solo trae el encabezado (<thead>) y un <tbody> vacío. jQuery llena las filas con datos.
Orden de los scripts: primero jQuery y después app.js, porque app.js usa $ y necesita que jQuery ya esté cargado.
Respaldo de jQuery:

##CSS
Variables (:root{--bg:...;--ac:...}): definen los colores una sola vez y se reutilizan con var(--ac). Cambiar un color cambia todo el sitio.
Modo oscuro automático: @media(prefers-color-scheme:dark) redefine las variables si el computador del usuario usa tema oscuro.
Flexbox en el header y en .tools (buscador y botón en una fila).
CSS Grid en .cards: repeat(auto-fit,minmax(200px,1fr)) acomoda las tarjetas solas según el ancho.
.card{display:none}: las tarjetas empiezan ocultas para que jQuery las muestre con animación.
Responsive: el @media(max-width:600px) reduce el espaciado de las tablas en celulares.
Detalles: tbody tr:hover resalta la fila bajo el mouse, y th[data-k]{cursor:pointer} muestra la manita en columnas ordenables

##JavaScript con jQuery
$(function () { ... })

Todo el código está dentro de esta función. Es la forma corta de decir "ejecuta esto cuando el HTML ya cargó" (equivale a $(document).ready). Sin esto, jQuery buscaría elementos que todavía no existen.

var NOM = [...], APE = [...], PRO = [...];
var rnd  = function (a, b) { ... };     // número entero aleatorio entre a y b
var pick = function (a) { ... };        // elemento aleatorio de una lista
var money = function (n) { return '$' + n.toLocaleString('es-CO'); };
var full  = function (v) { return v.nombres + ' ' + v.apellidos; };

Son las listas de nombres, apellidos y productos, más funciones pequeñas: números aleatorios, formato de moneda colombiana ($11.707.000) y nombre completo.

##Tabla resumen de jQuery usado  

unción jQuery	Para qué se usa
$(function(){})	Esperar a que cargue la página
$('#id'), $('.clase'), $('nav a')	Seleccionar elementos
$('<a>')	Crear elementos nuevos
.html(), .text()	Cambiar el contenido
.attr(), .data()	Leer y poner atributos
.addClass()	Agregar clases CSS
.on('click' / 'input' / 'change')	Manejar eventos
.trigger()	Disparar un evento por código
.val()	Leer lo escrito o elegido en un campo
.appendTo(), .remove()	Agregar y quitar elementos
.hide(), .fadeIn(), .delay()	Animaciones
$.each, .each	Recorrer listas
$.map	Transformar listas
$.grep	Filtrar listas
