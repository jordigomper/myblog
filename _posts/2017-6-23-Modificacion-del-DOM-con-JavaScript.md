---
layout: post
title: Modificación del DOM con JavaScript.
img: blog/i_jsnative.png
categories: javascript
---
  
[Aprende Javascript con MentoringJS - Step 7](http://mentoringjs.com/)
  
Si estas aprendiendo JavaScript, lo primero que debes aprender (después de entender los conceptos básicos como variables, funciones, etc.) es como alterar el DOM. Esto es una de las cosas que haces diariamente como desarrollador frontend.

Cambiar el **DOM** era difícil. Necesitamos jQuery para hacerlo mas fácil. Por suerte, ya no hay necesidad de jQuery.

En este articulo, vas a ver las cosas necesarias para tener que familiarizarte como un frontend developer.


## Que haces con DOM?

Cuando estas trabajando con **DOM**, vas a tener la necesidad de hacer una o más de las siguientes cosas:

1. Seleccionar elementos HTML
2. Añadir o borrar oyentes de eventos
3. Añadir o borrar clases
4. Añadir, cambiar o borrar atributos
5. Añadir o borrar elementos HTML

Voy a explicar lo que cada una de estas cosas son, por qué se usan y como hacerlo en las siguientes secciones. Vamos a saltar en primero - **selector de elementos de HTML.**
  
  
## Seleccionando elementos HTML.

Saber cómo seleccionar elementos HTML es el primer paso antes de hacer cualquier otra cosa con el **DOM**. Una vez que hayas seleccionado un elemento, deberás de añadir oyentes de eventos, cambiar clases, y hacer otras cosas.

Solo necesitas saber dos métodos para seleccionar cualquier cosa que desees - **querySelector and querySelectorALL**.

### QuerySelector
querySelecto **te ayuda a seleccionar un elemento HTML**. Si se encuentran varios elementos HTML en la selección, ***querySelector*** siempre devuelve el primer elemento. Se parece a esto:

```javascript
document.querySelector(selector);
```

Puedes seleccionar un elemento por su ID, clase o etiqueta con ***querySelector***.

Vamos a andar mediante un corto ejemplo. Digamos que tienes el siguiente ejemplo de HTML:

```html
<div id="la-primera">ID</div>
<div class="una-clase-impresionante">Class</div>
<p>Una etiqueta</p>
```

* Para **seleccionar un elemento con un id**, se selecciona la id con un #
* Para **seleccionar un elemento con una clase**, se selecciona el elemento con un .
* Para **seleccionar un elemento con una etiqueta**, simplemente escribe la etiqueta en el selector.

```javascript
document.querySelector('#unico');
// => <div id="id">ID</div>

document.querySelector('.una-clase-impresionante');
// => <div class="una-clase-impresionante">Class</div>

document.querySelector('p');
// => <p>Una etiqueta</p>
```


### Selecciones complicadas
***querySelector*** es increíblemente potente. Si vas a realizar selecciones complicadas para encadenar id's, clases y etiquetas juntas, mejor esto:

```javascript
document.querySelector('div #the-one');
```

Aunque es posible encadenar selectores, no te recomiendo que lo hagas porque es innecesario la mayoría de veces.


### Seleccionando elementos dentro de elementos
Aquí una gran cosa sobre ***querySelector***.Puedes indicarle que busque un elemento dentro de otro elemento, reduce el tiempo necesario para buscar un selector profundo.

Para hacerlo, tu añade un espacio entre las clases, id o etiquetas. Aqui un ejemplo:

```html
<div class="contenedor">
  <div class="elemento-Interior">Elemento interior!</div>
</div>
```

```javascript
let elementoInterior = document.querySelector('.contenedor elementoInterior');
// => <div class="elemento-interior">Elemento interior!</div>
```

Una alternativa, si ya tienes seleccionado un elemento con ***querySelector*** también puedes usar ese elemento para realizar otra llamada a ***querySelector***:

```javascript
let contenedor = document.querySelector('.contenedor');
let elementoInterior = contenedor.querySelector('.elementoInterior');
// => innerItem is <div class="elemento-interior">Elemento interior!</div>
```

Esto es todo lo que necesita saber sobre ***querySelector***.

Ahora, que vas a necesitar para seleccionar mas de un elemento? Aquí es donde entra el ***querySelectorAll***.


# QuerySelectorAll

***querySelectorAll*** es un método que te ayuda a seleccionar múltiple elementos.

```javascript
let todosLosElementos = document.querySelectorAll(selectores);
```

selectores, en este caso tienen la misma sintaxis que ***querySelector***. La única excepción es que puedes realizar múltiples selecciones y estas se separan con una coma (,).

```html
<div class="cosa">Una cosa</div>
<div class="cosa">Una cosa</div>
<div class="otra-cosa">Otra cosa</div>
```

```javascript
let todasLasCosas = document.querySelectorAll('.cosa, .otra-cosa')
// => [
//   <div class="cosa">Una cosa</div>,
//   <div class="cosa">Una cosa</div>,
//   <div class="otra-cosa">Otra cosa</div>
// ]
```

Esta parte es importante.

***querySelectorAll*** devuelve una [NodeList](https://developer.mozilla.org/en-US/docs/Web/API/NodeList)(incluso esto parece un Array).

Si estas trabajando con navegadores modernos, tienes que enviar elementos individuales dentro de la Nodelist con una llamada [NodeList.forEach](https://developer.mozilla.org/en-US/docs/Web/API/NodeList/forEach).

Si tienes que trabajar con navegadores viejos, necesitas convertir la NodeList en un Array antes de realizar un bucle con una llamada a ***forEach***. Este camino es fácil si utilizas ***Array.from()***.

```javascript
// Navegadores modernos
let todasLasCosas = document.querySelectorAll('.cosa, .otra-cosa')
todasLasCosas.forEach(el => {/* hacer algo con el elemento */})

// Navegadores viejos
let todasLasCosas = document.querySelectorAll('.cosa, .otra-cosa')
// Es posible que necesite un polyfill para Array.from
// Una alternativa, usar Array.prototype.slice.call(todasLasCosas);
let todasLasCosasArray = Array.from(todasLasCosas)
todasLasCosasArray.forEach(el => {/* hacer algo con el elemento */})
```

Después, pasemos a agregar y quitar oyentes de eventos.



## Añadiendo y borrando oyentes de eventos

Los oyentes de eventos permiten que su JavaScript realice una acción cada vez que se desencadene un evento. Asi es como sabes cuando un usuario ha interactuado con **DOM**. Un ejemplo es cuando pulsas un botón.

```javascript
let boton = document.querySelector('button');
let nav = document.querySelector('nav');

boton.addEventListener('click', toggleNav);

function toggleNav() {
  if (nav.classList.contains('abierto')) {
    nav.classList.remove('abierto');
  } else {
    nav.classList.add('abierto');
  }
}
```
**[EJEMPLO DE BOTON.](https://codepen.io/zellwk/pen/eWBLdZ)**

Aquí, solo necesitas saber dos métodos: addEventListener y removeEventListener.


### Añadiendo oyentes de eventos.
Para añadir un oyente de evento, primero selecciona el elemento HTML, luego llama a método addEventListener. Esto acepta dos parámetros, por ejemplo:

```javascript
let algo = document.querySelector('.algo');
algo.addEventListener(event, callback);
```

***even*** es un nombre de un evento que quieres escuchar. Estos eventos ya están predeterminados en la especificación.
Aquí una [lista practica de el tipo de eventos](https://developer.mozilla.org/en-US/docs/Web/Events) que puedes encontrar.

***callback*** es una función que hace lo que quieres cuando se dispara un evento. Esto contiene un parámetro -el objecto evento. Aquí podemos ver un ejemplo de una llamada de retorno:

```javascript
algo.addEventListener('click', llamada)

function llamada (e) {
  e.preventDefault() // Evita el comportamiento predeterminado. Úselo sólo cuando sea necesario
  console.log('has hecho click en algo!')
}
```

Podemos [hacer muchas cosas](https://developer.mozilla.org/en/docs/Web/API/Event) con el objeto de evento (e), pero esto es un tema para otro día. Vamos a ir a eliminar el oyente de evento.


### Eliminando oyentes de evento
Eliminar un oyente de método es similar a añadir un oyente de método. Aquí, llamaremos al método ***removeEventListener***, pasaremos dos parámetros - el tipo de ***evento*** y su llamada:

```javascript
algo.removeEventListener('click', llamada);
```

Normalmente, solo se eliminará un ***eventListener*** después de completar una tarea. Así que, es común encontrar ***removeEventListener*** dentro de una llamada ***addEventListener******removeEventListener***:

```javascript
algo.addEventListener('click', llamada);

function llamada () {
  console.log('has pulsado algo!');
  // elimina el oyente de evento
  algo.removeEventListener('click', llamada);
}
```

Cuando borras un oyente de eventos, ya no escuchas el evento. Así que, arriba del código, la llamada solo activara cuando ***.cosa*** sea pulsado por primera vez. En adelante al pulsar ***.cosa*** no activara la devolución de llamada.

Nota: Deberías de borrar un oyente de evento cuando no tienes mas necesidad de utilizarlo. Al hacer esto tu liberas recursos para otras tareas.

Vamos a seguir.



## Añadiendo y eliminando clases.

Volvemos a la demo del botón de mas arriba?

```javascript
let boton = document.querySelector('button');
let nav = document.querySelector('nav');

boton.addEventListener('click', toggleNav);

function toggleNav() {
  if (nav.classList.contains('abierto')) {
    nav.classList.remove('abierto');
  } else {
    nav.classList.add('abierto');
  }
}
```
**[EJEMPLO DE BOTON.](https://codepen.io/zellwk/pen/eWBLdZ)**

Esta es la función del código de demostración:

1. Añadir ***.abierto*** al ***&lt;nav&gt;*** cuando el usuario presiona el botón.
2. Eliminar  ***.abierto*** del ***&lt;nav&gt;*** si ***&lt;nav&gt;*** esta ya abierto cuando el usuario presiona el botón.
3. La transición de ***&lt;nav&gt;*** se hace con ***CSS***

Este ejemplo enseña el poder de ***CSS*** cuando se combina con JavaScript. Puede crear todo tipo de interacciones simplemente añadiendo (o eliminando) una clase.

Aquí esta como tienes que añadir una clase, eliminar una clase o verificar si existe alguna clase:

1. Para **añadir una clase** utiliza  
    ***elemento.classList.add('nombreDeClase');***
2. Para **borrar una clase** utiliza
    ***elemento.classList.remove('nombreDeClase');***
3. Para **verificar si una clase existe** utiliza
    ***elemento.classList.contains('nombreDeClase');***

El siguiente código añado o borra ***.abierto*** del ***&lt;nav&gt;*** cuando haces click en el botón:

```javascript
let boton = document.querySelector('button');
let nav = document.querySelector('nav');

boton.addEventListener('click', toggleNav);

function toggleNav() {
  // Comprueba si esa clase existe
  if (nav.classList.contains('abierto')) {
    // Si tiene .abierto elimina esa clase
    nav.classList.remove('abierto');
  } else {
    // añade .abierto
    nav.classList.add('abierto');
  }
}
```

Vamos a seguir añadiendo, cambiando y eliminando atributos.



## Añadir, cambiar y eliminar atributos

Los atributos son una parte importante de los elementos de HTML. Alguna veces, vas a necesitar extraer información de estos atributos para dar contexto a tu JavaScript. Otras veces, necesitaras usar estos atributos para ayudar a escribir interfaces accesibles.

Aquí un ejemplo encima de  ***&lt;nav&gt;***, escritas de una forma accesible:

```javascript
let boton = document.querySelector('button');
let nav = document.querySelector('nav');

boton.addEventListener('click', toggleNav);

function toggleNav() {
  let abierto = nav.classList.contains('abierto');
  if (abierto) {
    nav.classList.remove('abierto');
    nav.setAttribute('aria-hidden', true);
    boton.setAttribute('aria-expanded', false);
  } else {
    nav.classList.add('abierto');
    nav.removeAttribute('aria-hidden');
    boton.setAttribute('aria-expanded', true);
  }
}

```
**[EJEMPLO COMPLETO](https://codepen.io/zellwk/pen/aWBaME)**

En este ejemplo, han habido dos cambios:

1. Se ha añadido ***aria-expanded*** a ***botón*** para indicar al exploradores si el menú esta expandido.
2. Se ha añadido ***aria-hidden*** a ***nav*** para prevenir que exploradores lean el menú cuando esté oculto.

Aquí esta como debes de extraer la información de un atributo, establecer un atributo y borrar el atributo:

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

Finalmente, pasemos a agregar o quitar elementos.


## Añadir o borrar elementos

Empezamos esta sección con una demostración:

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


### Añadir elemento en el DOM
Hay tres pasos para añadir este texto al **DOM**. Estos son:

1. Crear un elemento HTML con
    ***document.createElement***
2. Añadir contenido en el elemento HTML estableciendo
    ***innerHTML***
3. Añadir en el **DOM** con ***parentNode.prepend*** o ***parentNode.append***

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

```javascript
ul.removeChild(li);
```

No podemos simplemente decir eliminar ***&lt;li&gt;*** y esperar que JavaScript sepa que elemento de la lista debe eliminar. Necesitamos decir al JavaScript cual a de eliminar exactamente.

Si puede utilizar ***querySelector*** para elegir cual elemento a de eliminar, este es el método más fácil:

```javascript
let padre = document.querySelector('.padre')
let paraEliminar = document.querySelector('.elemento-para-eliminar')
padre.removeChild(paraEliminar)

// Si no quieres escribir un querySelector separado
paraEliminar.parentNode.removeChild(paraEliminar)
```

En la demostración de anterior, no podemos hacer esto porque no hay forma de saber cuál es el primer o último elemento de la lista con clases o identificadores.

En lugar, podemos utilizar ***parentNode.children*** para ir a una NodeList con elementos dentro de ***ul***, después, usar un método de Array para ir a un elemento especifico y borrarlo.

Aquí está el código para eliminar le primer elemento hijo:

```javascript
let list = document.querySelector('ul');
removeFirst.addEventListener('click', function {
  if (list.children.length) {
    let firstNode = list.children[0];
    list.removeChild(firstNode);
  }
})
```



## Terminado

Alterar el **DOM** es una de las cosas mas importantes que necesita saber un frontend developer. Vas a ser capaz de hacer todo tipo de cosas preciosas en el momento que aprenda a trabajar con el **DOM**.

En este articulo se a mostrado cinco maneras comunes que se necesita para alterar el **DOM**, más el código relevante que necesitas saber. Ahora prueba a jugar con **DOM** y cree algo de magia.



La fuente de este articulo se encuentra en este [link](https://zellwk.com/blog/js-in-dom/)