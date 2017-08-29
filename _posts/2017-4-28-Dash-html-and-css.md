---
layout: post
title: Curso Dash HTML y CSS 
categories: html&css
---
[Aprende Javascript con MentoringJS - Step 3](http://mentoringjs.com/)  
  
  
Dash es un programa interactivo para aprender HTML, CSS i JavaScript. Es muy útil para empezar en el mundo de la codificación web.
  
Con la base del curso de Codeacademy solamente hemos de preocuparnos de escribir los que nos indican, la dificultad es baja.  
Aquí vamos a ver las posibilidades que, con nuestra simple base de html y css, tenemos diferentes posibilidades de crear una pagina web.  
La única diferencia que apreciamos con Codeacademy es que en este curso no disponemos de una hoja de estilo separada de nuestra hoja de HTML, deberemos de introducir nuestro código CSS dentro de la misma hoja de HTML, no os preocupéis básicamente es lo mismo. Durante el curso se nos pondrán varios checkpoints donde tendremos que hacer lo que nos indican, estos tienen el fondo de color amarillo y nos indicaran con un visto verde cuando este todo bien y nos deje pasar al siguiente punto. Si en algún momento te sientes atascado o no recuerdas que sintaxis tenia algún elemento, puedes ir dentro de la división de pantalla de la esquina izquierda superior y presionar sobre Skills, estas skills son etiquetas que pasando el cursos por encima nos indicaran la sintaxis. Las Skills de color rojo son HTML, las amarillas CSS y las azules Javascript. Durante el curso iremos desbloqueando las a medida que avanzamos.  
El foro de Dash no es mas que su pagina principal de facebook, un rollazo si tienes que buscar algo!


## Proyecto 1. Construye una web personal

> La base de este proyecto es crear una web muy simple pero con un aspecto increíble.

Empezando, nos indican que tenemos que construir una pagina web para nuestra amiga Anna, al turrón! 

Nos indican como funciona Dash, en la esquina izquierda superior nos irán indicando los pasos. Esquina izquierda inferior es donde tenemos el editor, donde hemos de colocar nuestro código HTML y CSS. En la parte derecha podemos visualizar el aspecto que va teniendo nuestra pagina web.
 

**Parte 1:**
Empezamos con los etiquetas tipo &lt;h&gt; y &lt;p&gt;, ningún problema si hemos hecho el curso de Codeacademy. Nos enseña el apartado de las pestañas. 
Seguimos con las etiquetas input. Estas no habían salido en Codeacademy. Simplemente se usan para crear controles interactivos para formularios. La forma en que funciona varia dependiendo del valor que indiquemos dentro del atributo type. Mas información [aquí](https://developer.mozilla.org/es/docs/Web/HTML/Elemento/input). Seguimos hasta finalizar la parte 1.

**Parte 2:**
Vamos a darle un apartado CSS dentro de nuestro HTML y vamos a crear una estructura básica.
Entre las etiquetas &lt;style&gt; vamos a colocar nuestro código CSS. Siguiendo con el curso vamos a darle la estructura adecuada a nuestro código.

**Parte 3:**
Nos indican que vamos a incluir los logos y el style a nuestra web. Para colocar las imágenes nos van a decir una ruta [RELATIVA](http://librosweb.es/libro/xhtml/capitulo_4/enlaces_relativos_y_absolutos.html) que hemos de poner. 
dentro de CSS body vamos a indicar que el fondo va a ser una ur, abrimos paréntesis y comillas dobles y ponemos la url que nos dan. Con background-size:cover indicamos que cubra toda el fondo sin modificar la resoluciones la imagen. Acabamos el curso y podemos ver nuestra maravillosa pagina web que hemos creado para Anna.


## Proyecto 2. Construye una blog.

Jeff nos indica que Anna le a hablado muy bien de nosotros, y que quiere que le construyamos un blog

**Parte 1:**
Empezamos dándole una estructura básica. Vamos crear una tabla no ordenada donde vamos a colocar 3 links. 

**Parte 2:**
En esta parte vamos a añadir el estilo a la web. Vamos a simular que llamamos a una hoja de estilo externa, pero realmente vamos a utilizar el documento HTML para introducir el código CSS. Nos va a explicar el atributo [display](https://www.w3schools.com/cssref/pr_class_display.asp), atributo que debemos de repasar si todavía no tenemos claro su funcionamiento. Acabamos esta parte sin mucha dificultad.

**Parte 3:**
En esta parte vamos a alinear todo los textos y apartados de la web. Cambien vamos a ver algo nuevo. Con el atributo @media vamos a indicar que cuando se cumpla la condición que indicaremos entre paréntesis entre a buscar el CSS que hay. Esto sirve optimizar nuestra web a diferentes resoluciones de pantallas. Por ejemplo a dispositivos móviles, tablets, etc etc... En la división de pantalla derecha, arriba a la derecha tenemos un interruptor con el dibujo de un teléfono móvil, si presionamos el aspecto de nuestra web cambiara y simulara la visión a través de una pantalla de un teléfono móvil. Es importante ir alternando las vistas hasta poder hacerse una idea dela funcion @media y como afecta a diferentes resoluciones de pantalla. Vamos a tocar un poco de Javascript, el nivel es muy fácil y nos indican perfectamente la sintaxis y como funciona, nada del otro mundo...

**Parte 4:**
Vamos a profundizar en la optimización de nuestra web para diferentes dispositivos y resoluciones de pantalla. Es muy importante ir alternando las diferentes vistas. Acabando esta parte finalizamos el este curso


## Proyecto 3. Pequeña web de negocios.

Esha nos dice que necesita una pagina web para su restaurante.

**Para este proyecto no debemos de utilizar el navegador de IExplorer, ya que vamos a ver transparencias con rgba y no es compatible con ninguna versión actual.**

**Parte 1:**
En esta parte empezamos añadiendo imágenes, posicionando elementos... nada que no sabemos ya. A medida que avanzas empezamos con los atributos de class para CSS, sencillo si hemos acabado el curso de Codeacademy. Añadiremos diferentes clases a diferentes &lt;div&gt;'s. Nos enseñaran el elemento &lt;br /&gt; que utilizaremos para dar saltos de linea. Acabamos esta parte sin dificultad ninguna.

**Parte 2:**
Empezamos con el elemento &lt;span&gt;, es un elemento in-line y sirve para poder dar estilo a algún texto. Nos explica como crear colores transparentes para nuestros fondos. Para comprender todo esto un poco mas podemos experimentar con esta [web](http://www.css3maker.com/css-3-rgba.html).

**Parte 3:**
Vamos a optimizar nuestra web para diferentes dispositivos utilizando el elemento @media. La dificultad es baja y debemos de aprovechar para ir alternando las vistas y comprender lo que estamos haciendo. Con esto acabamos este proyecto que es el ultimo de este articulo.

Espero que os haya servido de ayuda. Es importante comprender todo lo que hemos hecho, dejando para mas adelante aspectos como saber de memoria las sintaxis de según que cosas. Hay que aprovechar el aspecto interactivo que nos ofrece Dash para experimentar y ver los cambios se afectan a nuestra web. Al final de todo crearemos una función de Javascript que nos mostrara los detalles de plato al presionar encima. 

Sin mas me despido, hasta luego mundo!!
