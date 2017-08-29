---
layout: post
title: Como modificar el DOM sin necesidad de jQuery.
img: blog/i_dom.jpg
categories: javascript
---
[Aprende Javascript con MentoringJS - Step 7](http://mentoringjs.com/)

Hola chicos! En este articulo os voy a enseñar a modificar el DOM sin la necesidad de tener que utilizar jQuery.



## Introducción
  

Para modificar nuestro **DOM** vamos a tener que hacer una de las siguientes cosas:
  
1. Seleccionar elementos HTML
2. Añadir o borrar oyentes de eventos
3. Añadir, comprobar o borrar clases
4. Añadir, cambiar o borrar atributos
5. Añadir o borrar elementos HTML
  
  

## Seleccionar elementos HTML
  
Este es el primer paso que debemos hacer antes de modificar nuestro **DOM**. Seleccionaremos un o varios elementos y podremos añadir oyentes de eventos, modificar clases, etc etc...
  
### Tipo de métodos:

Solo hay 2 métodos:
* ***querySelector*** sirve para seleccionar un elemento. Si encuentra varios elementos devuelve el primero
* ***querySelectorALL*** sirve para seleccionar mas de un elemento.
  
### Seleccionar elementos:

Puedes seleccionar un elemento por su **ID**, **CLASS** o etiqueta.
* Para **seleccionar un elemento con un ID**, se selecciona la **ID** introduciendo una **#** al comienzo del nombre del **ID**.
* Para **seleccionar un elemento con una clase**, introduciremos un **.** al comienzo del nombre de la **CLASS**
* Para **seleccionar un elemento con una etiqueta**, simplemente escribe la etiqueta en el selector.

### Tipo de selecciones:

1. Se pueden hacer selecciones encadenadas:
```javascript
document.querySelector('div #id1');
// solo selecciona las div que tengan un ID="id1"
```

2. Elementos dentro de elementos
Indicaremos que busque un elemento dentro de otro elemento añadiendo un espacio entre los electores:
HTML:
```HTML
<div class="contenedor">
  <div class="elemento-Interior">Elemento interior!</div>
</div>
```

```javascript
let elementoInterior = document.querySelector('.contenedor elementoInterior');
// Esto selecciona un elemento interior que este dentro de una CLASS .contenedor
```

Si ya tienes eleccionado un elemento con ***querySelector*** puedes usar ese elemento para realizar otra llamada a ***querySelector***:

```javascript
let contenedor = document.querySelector('.contenedor');
let elementoInterior = contenedor.querySelector('.elementoInterior');
// En la primera linea seleccionamos un elemento con CLASS=".contenedor"
// En la siguiente linea utilizamos ese selector para buscar dentro un  
// elemento CLASS="elemntoInterior"
```
  

  
## Selectores
  
### querySelector
Indicamos el nombre del elemento dentro de paréntesis y entre comillas.

Ejemplo:
  
```javascript
document.querySelector('nombre_elemento');
// introduciremos el #nombre_ID, .nombre_CLASS, o nombre_etiqueta del elemento
```
  
Ejemplo con código HTML:
  
```html
<div id="un_ID">soy un ID</div>
<div class=".una_CLASS">Soy una clase!</div>
<p>Soy una etiqueta</p>
```
  
```javascript
document.querySelector('#un_ID');
// => <div id="un_ID">soy un ID</div>

document.querySelector('.una_CLASS');
// => <div class="una_CLASS">Soy una clase!</div>

document.querySelector('p');
// => <p>Soy etiqueta</p>
```
  
  
### querySelectorALL
Igual que ***querySelector***. Para realizar múltiples selecciones estas devén de estar separadas por una coma.

Ejemplo:

```javascript
let todosLosElementos = document.querySelectorAll('elemento1, elemento2');
```

Ejemplo con código HTML:
  
```html
<div class="ave">Soy una golondrina</div>
<div class="ave">Soy un aguila</div>
<div class="reptil">Soy una tortuga</div>
```

```javascript
let animales = document.querySelectorAll('.ave, .reptil')
//   <div class="ave">Soy una golondrina</div>
//   <div class="ave">Soy un aguila</div>
//   <div class="reptil">Soy una tortuga</div>
```
  
> ***querySelectorAll*** devuelve una [NodeList](https://developer.mozilla.org/en-US/docs/Web/API/NodeList)(algo parecido a un Array).
> 
> Si estas trabajando con **navegadores modernos**, tienes que enviar elementos individuales dentro de la Nodelist con una llamada [NodeList.forEach](https://developer.mozilla.org/en-US/docs/Web/API/NodeList/forEach).
> 
> Si tienes que trabajar con **navegadores viejos**, necesitas **convertir la NodeList en un Array **antes de realizar un bucle con una llamada a ***forEach***. Puedes utilizar el método ***Array.from()***.

```javascript
// Navegadores modernos
let animales = document.querySelectorAll('.ave, .reptil')
animales.forEach(el => {/* hacer algo con el elemento */})

// Navegadores viejos
let animales = document.querySelectorAll('.ave, .reptil');

// Es posible que necesite un polyfill para Array.from
// Una alternativa, usar Array.prototype.slice.call(animales);
let Array_animales = Array.from(animales);
Array_animales.forEach(el => {/* hacer algo con el elemento */})
```
  
## Añadiendo y borrando oyentes de eventos
Permiten a JavaScript realizar una acción cada vez que se desencadene un evento. ejemplo:

```javascript
// seleccionamos el elemento button
let boton = document.querySelector('button');

// esto es un oyente de eventos, se activa cuando detecta
// un 'TipoDeEvento' en el elemento que hemos seleccionado
// button, dentro del selector botón:
boton.addEventListener('tipo de evento', nombreDeLaFuncion);

//funcion que activa el oyente de eventos
function nombreDeLaFuncion() {
    // Aqui la funcion a realizar cada vez que el elemento botón
    // recibe un tipo de evento, por ejemplo al pulsarse
};
```
**[EJEMPLO DE BOTON.](https://codepen.io/zellwk/pen/eWBLdZ)**
  
Podemos hacer muchas cosas con el objeto de evento, aquí una [lista](https://developer.mozilla.org/en/docs/Web/API/Event).
  

  
## Añadir y eliminar oyente de eventos
  
### addEventListener y removeEventListener
Para añadir un oyente de evento, seleccionar el elemento HTML, y llamar al método ***addEventListener***. ejemplo:

```javascript
Elemento1.addEventListener('click', funcion1)

function funcion1 () {
  console.log('has hecho click en algo!')
}
```

Con el método ***addEventListener*** añadimos a Elemento1 un oyente de método el cual al presionar sobre Elemento1 llama a la funcion1 y imprime un mensaje por pantalla.
  
Para eliminar un oyente de método llamaremos al método ***removeEventListener*** incluyendo los parámetros 'tipoEvento' y llamada_funcion:

```javascript
Elemento1.removeEventListener('tipoEvento', llamada_funcion);
```

Asegurate de eliminar un oyente de eventos tras completar su tarea. Normalmente suele introducirse un ***removeEventListener*** dentro de su llamada ***addEventListener***. ejemplo:

```javascript
Elemento1.addEventListener('click', llamada);

function llamada () {
  // muestra un mensaje por pantalla
  console.log('has pulsado algo!');
  // eliminar el oyente de evento
  Elemento1.removeEventListener('click', llamada);
}
```

Al borrar el oyente de eventos, en el código solo se activara cuando Elemento1 sea pulsado la primera vez, en adelante ya no se activara. Así que, solo debes borrar un oyente de eventos cuando no vas a volver a utilizarlo.

>NOTA: Debes borrar un oyente de evento cuando no tienes mas necesidad de utilizarlo para liberar recursos para otras tareas.
  
  
  
## Añadir, comprobar y eliminar clases.
  
Puede crear todo tipo de interacciones simplemente añadiendo (o eliminando) una clase.

1. Para **añadir una clase** utiliza  
    ***elemento.classList.add('nombreDeClase');***
2. Para **borrar una clase** utiliza
    ***elemento.classList.remove('nombreDeClase');***
3. Para **verificar si una clase existe** utiliza
    ***elemento.classList.contains('nombreDeClase');***
ejemplo:

```javascript
let boton = document.querySelector('button');
let nav = document.querySelector('nav');

boton.addEventListener('click', mostrarNAV);

function mostrarNAV() {
  // Comprueba si esa clase existe
  if (nav.classList.contains('visible')) {
    // Si tiene .abierto elimina esa clase
    nav.classList.remove('visible');
  } else {
    // añade .abierto
    nav.classList.add('visible');
  }
}
```
**[EJEMPLO DE BOTON.](https://codepen.io/zellwk/pen/eWBLdZ)**

Con este ejemplo podemos hacer visible un menú pulsando un botón, y ocultarlo con solo volver a presionar el botón.
  
  
  
## Añadir, cambiar y eliminar atributos
  
Los atributos son una parte importante de los elementos de HTML. Alguna veces, vas a necesitar extraer información de estos atributos para dar contexto a tu JavaScript. Otras veces, necesitaras usar estos atributos para ayudar a escribir interfaces accesibles. ejemplo:

```javascript
let boton = document.querySelector('button');
let nav = document.querySelector('nav');

boton.addEventListener('click', toggleNav);

function toggleNav() {
    // selector de la nav con CLASS="abierto"
  let abierto = nav.classList.contains('abierto');
  // Si el selector da verdadero (contiene una nav con CLASS="abierto")
  if (abierto) {
    // borra  esa clase
    nav.classList.remove('abierto');
    // indica al explorador que el menú esta oculto
    nav.setAttribute('aria-hidden', true);
    // indica que no se puede mostrar el contenido de botón
    boton.setAttribute('aria-expanded', false);
  } 
  // y si el selector abierto da false
  else {
    // agrega la CLASS="abierto"
    nav.classList.add('abierto');
    // Elimina el atributo que indica que el menú esta oculto
    nav.removeAttribute('aria-hidden');
    // Da true para que el explorador pueda mostrar el menú
    boton.setAttribute('aria-expanded', true);
  }
}

```
**[EJEMPLO COMPLETO](https://codepen.io/zellwk/pen/aWBaME)**

Se añade ***aria-expanded: true/false*** a ***botón*** para indicar al explorador si el menú esta expandido y  ***aria-hidden: true/false*** a ***nav*** para prevenir que el explorador lea el menú cuando esté oculto.

1. Para ir a un atributo utiliza
    ***getAttribute('nombre-atributo')***
2. Para cambiar/establecer un atributo utiliza
    ***setAttribute('nombre-atributo', 'valor-atributo')***
3. Para eliminar un atributo utiliza
    ***removeAttribute('nombre-atributo')***

```javascript
// Ir al atributo
button.getAttribute('aria-expanded');

// Establecer un atributo
button.setAttribute('aria-expanded', true);

// Eliminar un atributo
button.removeAttribute('aria-expanded');
```
  


## Añadir o borrar elementos en el DOM
  
### Añadir elementos en el DOM
Hay tres pasos para añadir este texto al **DOM**. Estos son:

1. Crear un elemento HTML con
    ***document.createElement***
2. Añadir contenido en el elemento HTML estableciendo
    ***innerHTML***
3. Añadir en el **DOM** con ***parentNode.prepend*** o ***parentNode.append***

ejemplo:
```javascript
let ul = document.querySelector('ul');

// crear elemento <li>
let li = document.createElement('li');

// Añadir contenido a <li> 
li.innerHTML = 'Hola de nuevo, Mundo!';

// Añadir en el DOM
ul.append(li);
```

### Eliminar elementos con DOM
Para eliminar un elemento de **DOM**, necesitas llamar a ***parentNode.removeChild***. Este método toma un parámetro - el elemento a eliminar.

ejemplo:
```javascript
ul.removeChild(li);
```

Hay que indicar específicamente el elemento a eliminar:

```javascript
let padre = document.querySelector('.padre')
let paraEliminar = document.querySelector('.elemento-para-eliminar')
padre.removeChild(paraEliminar)

// Si no quieres escribir un querySelector separado
paraEliminar.parentNode.removeChild(paraEliminar)
```

Si deseamos borrar el primer o ultimo hijo, con este ejemplo no nos vale, ja que no hay forma de saber cuál es el primer o úlitmo elemento de la lista con clases o identificadores. 

En lugar, podemos utilizar ***parentNode.children*** para ir a una NodeList con elementos dentro de ***ul***, después, usar un método de Array para ir a un elemento especifico y borrarlo.

ejemplo:
```javascript
// selector de un elemento ul
let lista = document.querySelector('ul');
// indicamos borrar el primero, al hacer click
removeFirst.addEventListener('click', function {
    // si el numero de elementos con padre es mayor a 0
  if (lista.children.length) {
    // hacemos un selector con el primer hijo que encontramos
    let firstNode = list.children[0];
    // borramos este elemento
    list.removeChild(firstNode);
  }
})
```

Aquí dejo un ejemplo que te ayudara a comprender-lo:
```javascript
let prepend = document.querySelector('.prepend')
let append = document.querySelector('.append')
let eliminarPrimero = document.querySelector('.eliminarPrimero')
let eliminarUltimo = document.querySelector('.eliminarUltimo')
let lista = document.querySelector('ul')

function crearLi () {
  let li = document.createElement('li')
  li.innerHTML = 'Hola de nuevo, mundo!'
  return li
}

// añade al principio de la lista
prepend.addEventListener('click', e => list.prepend(createLi()))

// añade al final de la lista
append.addEventListener('click', e => list.append(createLi()))

// eliminar primero
eliminarPrimero.addEventListener('click', e => {
  if (list.children.length) {
    let firstNode = list.children[0]
    list.removeChild(firstNode)
  }
})    

// eliminar ultimo
eliminarUltimo.addEventListener('click', e => {
  if (list.children.length) {
    let lastNode = list.children[list.children.length - 1]
    console.log(lastNode)
    list.removeChild(lastNode)
  }
}) 

```
**[EJEMPLO CODIGO](https://codepen.io/zellwk/pen/EmNdWp)**

Si presionas en el botón  ***prepend*** o ***append*** antes, has comprobado que el texto ***Hola de nuevo, mundo!*** se añade en el **DOM** como otro elemento de lista.

## Últimos pasos
  
A continuación os dejo 2 ejemplos donde se pone en funcionamiento todo lo mencionado en este articulo:

1. En el primer ejemplo ponemos en practicas los selectores ***querySelector*** y ***querySelectorAll***. Utilizaremos ***addEventListener*** para añadir los oyentes de eventos y ***classList*** con sus variantes para visualizar o ocultar la lista. También un pequeño ejemplo de ***forEach*** para que te hagas una ida de su funcionamiento.

En este ejemplo tendremos un primer botón, que al pulsarlo nos mostrara una lista con todos los animales y otro botón donde pone descripción. La div que contiene la lista esta en el css como opacity. Al pulsar el botón añadiremos la clase abierta la cual dará opacity:1 y hace visible la lista.

Al pulsar el botón descripción que se muestra después de hacer la lista de los animales visible, un selector con todos los li de la lista y los enviara por forEach, añadiendo una clase que los hace opacity:1 y color:red. Aquí os dejo el ejemplo:

HTML:
```html
<button>Mostrar animales</button>
<div>
  <ul>
    <li>Golondrina <span>Ave</span></li>
    <li>Aguila <span>Ave</span></li>
    <li>Tortuga <span>Reptil</span></li>
  </ul>
  <button id="descripcion">Descripción</button>
</div>
```

CSS:
```css 
button {
  font-size: 1.5em;
  margin: 1em;
  padding: 0.5em 0.75em;
}

div {
  opacity: 0;
}

.abierta {
  opacity:1;
}

span {
  color: white;
}

.des {
  color:red;
}
```

JS:
```javascript
// selector para el oyente de eventos
let boton_animales = document.querySelector('button')

// selector para añadir una clase y poder visualizar la lista
let animales = document.querySelector('div')
// selector donde cojera todos los animales y le añadirá una descripción
let boton_descripcion = animales.querySelector('#descripcion')

// cuando hacemos click en el botón Mostrar animales llama a la función
boton_animales.addEventListener('click', mostrar_animales)

// esta función se encarga de comprobar si el elemento DIV que esta dentro del // selector animales contiene la clase abierta, si la tiene la eliminia y si 
// no la añade y hace visible la lista
function mostrar_animales() {
  if (animales.classList.contains('abierta')) {
    animales.classList.remove('abierta');
    boton_descripcion.classList.remove('abierta')
  } else {
    animales.classList.add('abierta');
    boton_descripcion.classList.add('abierta')
  }
}

// oyente de método que dispara la funcion mostrar_descripcion al pulsar el 
// botón
boton_descripcion.addEventListener('click', mostrar_descripcion)

// creamos un selector añadir_des que va a contener todas las descripciones de // todos los animales de la lista. enviaremos con forEach
// añadiendo una clase a cada una para hacerla visible
function mostrar_descripcion() {
  let añadir_des = animales.querySelectorAll('ul li span')
 añadir_des.forEach( function () {
   if (añadir_des.classList.contains('des')) {
    añadir_des.classList.remove('des');
  } else {
    añadir_des.classList.add('des');
  }
 })
}
```


2. En el segundo ejemplo utilizo ***createElement***, ***innerHTML*** y ***removeChild*** para poder gestionar una agenda de nombres. Es algo sencilla y no tiene ninguna utilidad pero así puedes ver como poder manipular la creación,modificación, y borrado de los elementos dentro de la DOM.

aquí el ejemplo:

HTML:
```html
<button class="añadir">Añadir nombre</button>
<button class="eliminar">Borrar ultimo nombre</button>
<br><br><br>
<div>

</div>
```

CSS:
```css
button {
  font-size: 1em;
  margin-top: 1em;
  margin-left: 1em;
  padding: 0.5em 0.75em;
  + button {
    margin-left: 0.5em;
  }
}
```

JS:
```javascript
// selectores para los oyentes de evento
let añadir = document.querySelector('.añadir')
let eliminar = document.querySelector('.eliminar')
// selector donde añadiremos los nuevos elementos
let list = document.querySelector('div')

// esta función crea un elemento label
function createLabel () {
  let label = document.createElement('label')
  label.innerHTML = '<br><br>Nombre  '
  return label
}
// esta función crea un elemento input
function createInput () {
  let input = document.createElement('input')
  return input
}

// este oyente de eventos se dispara al
// hacer click en el botón añadir.
// a continuación llama a la función
// createLabel y createInput 
añadir.addEventListener('click', e => list.prepend(createLabel(),createInput()))

// este oyente de eventos se dispara
// cuando hacemos click en el botón 
// eliminar. 
// Crea 2 selectores de cada tipo
// con los primeros 2 elementos de
// la Array y los elimina
eliminar.addEventListener('click', e => {
  if (list.children.length) {
    let label = list.children[0]
    list.removeChild(label)
    let input = list.children[0]
    list.removeChild(input)
  }
}) 
```

Con esto acabo este articulo. Con el conocimiento adquirido y este documento ya eres capaz de modificar la estructura DOM a tu antojo.

Si tienes alguna duda no dudes en ponerte en contacto conmigo.

Espero haberte ayudado, HASTA LUEGORR!!!
  
  
  
**A tope con @mentoringJS!  
Jordi Gomper.**