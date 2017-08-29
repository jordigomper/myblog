---
layout: post
title: Ya no vas a necesitar jQuery nunca más!
img: blog/i_nojquery.png
categories: javascript
---
  
[Aprende Javascript con MentoringJS - Step 7](http://mentoringjs.com/)  
  
Liberate de las cadenas de jQuery comprendiendo la moderna API Web y descubriendo varias bibliotecas dirigidas para ayudarte a llenar los vacíos.
  
  
## Peticiones Ajax  
  
Muchos desarrolladores que aprenden a desarrollar páginas web mediante jQuery probablemente piensan que jQuery que esta haciendo algo mágico cuando invocas al método ***$.ajax***. Esto no podría estar más lejos de la verdad. Todo el trabajo pesado es realizado por el navegador vía objeto ***XMLHttpRequest***. El ajax de jQuery es simplemente el contenedor alrededor de ***XMLHttpRequest***. El uso del soporte interno del navegador para las solicitudes de ajax no es muy difícil, como verás a continuación. Incluso las solicitudes de origen cruzado son simples.  
  
  
1. GETing
2. POSTing
3. URL Encoding
4. JSON
  
  
## GETing  
  
Empezamos con una solicitud simple pero común. Necesitamos preguntar al servidor por el nombre de una persona, dado el identificador único de esa persona. El String del ID único debe incluirse como un parámetro de consulta en el [URI][URI], con una carga útil vacía, como es común para las solicitudes GET.  Invocar una alerta con el nombre de usuario, o un error si la petición falla.  
  
### jQuery  
  
Hay un par de maneras de iniciar una solicitud GET ajax utilizando la [API][API] de jQuery. Uno implica el método 'get', que es una abreviatura de ajax con un tipo de 'get'. Sólo usaremos el método ajax para la coherencia.  
  
```javascript
$.ajax('myservice/username', {
    data: {
        id: 'identificacion-unica'
    }
})
.then(
    function success(nombre) {
        alert('El nombre de usuario es ' + nombre);
    },

    function fail(data, status) {
        alert('Peticion fallida. Estado devuelto de ' + status);
    }
);
```
  
### Native XMLHttpRequest Object
  
```javascript
var xhr = new XMLHttpRequest();
xhr.open('GET', 'myservice/username?id=identificacion-unica');
xhr.onload = function() {
    if (xhr.status === 200) {
        alert('User\'s name is ' + xhr.responseText);
    }
    else {
        alert('Request failed.  Returned status of ' + xhr.status);
    }
};
xhr.send();
```
  
El ejemplo de JS nativo funcionará en IE7 y versiones posteriores. Incluso IE6 podría aceptarlo, simplemente intercambiando ***new XMLHttpRequest()*** con el nuevo ***ActiveXObject("MSXML2.XMLHTTP.3.0")***. Nuestro ejemplo nativo parece fácil de seguir y bastante intuitivo para escribir. Entonces, ¿por qué usar jQuery aquí? ¿Qué se gana?  
  
## POSTing  
  
Vamos a ampliar un poco nuestro ultimo ejemplo. Ahora que tenemos el nombre de usuario al completo, vamos a seguir adelante y cambiarlo. Volveremos a dirigir este usuario por ID. Necesitamos enviar un mensaje a nuestro servidor para ese usuario en particular y incluir el nuevo nombre del usuario dentro del cuerpo de esta petición como una URL codificada en String. El servidor devuelve el nombre actualizado en la respuesta, por lo que debemos de comprobar para asegurarnos que todo está bien.  
  
El método correcto para usar en este caso es en realidad PATCH, pero hay algunos problemas con PATCH y otros métodos no tradicionales en los navegadores más antiguos (como IE8), por lo tanto, sólo vamos a utilizar POST aquí, pero el código es idéntico en cualquier caso, con la excepción del nombre del método diferente.  
  
También tenga en cuenta que el siguiente enfoque es prácticamente el mismo, independientemente del método de solicitud.  
  
### jQuery  
  
```javascript
var nuevoNombre = 'John Smith';

$.ajax('myservice/username?' + $.param({id: 'identificacion-unica'}), {
    method: 'POST',
    data: {
        name: nuevoNombre
    }
})
.then(
    function success(nombre) {
        if (nombre !== nuevoNombre) {
            alert('Algo salió mal. El nombre es ahora ' + name);
        }
    },

    function fail(data, status) {
        alert('Solicitud fallida. Estado devuelto: ' + status);
    }
);
```
  
### Native XMLHttpRequest Object  
  
```javascript
var nuevoNombre = 'John Smith',
    xhr = new XMLHttpRequest();

xhr.open('POST', 'myservice/username?id=identificacion-unica');
xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded');
xhr.onload = function() {
    if (xhr.status === 200 && xhr.responseText !== newName) {
        alert('Algo salió mal. El nombre es ahora ' + xhr.responseText);
    }
    else if (xhr.status !== 200) {
        alert('Solicitud fallida. Estado devuelto: ' + xhr.status);
    }
};
xhr.send(encodeURI('nombre=' + nuevoNombre));
```
  
Aquí parece claro que la forma de jQuery para enviar esta solicitud es mucho más elegante. Té ahorrara un poco de trabajo. Pero, merece la pena depender por esta elegancia? Si te parece cómodo utilizar el objeto ***XMLHttpResquest***, la respuesta sera que probablemente no.  
  
## URL Encoding  
  
jQuery proviene una función que toma un objeto y lo convierte en una URL codificada a String.  
  
```javascript
$.param({
    key1: 'algun valor',
    'key 2': 'otro valor'
});
```
  
Esto es bonito, pero podemos hacer algo similar con un poco de esfuerzo, sin jQuery. La Web [API][API] proviene dos funciones que codifica URL en strings: ***encodeURI*** y ***encodeURIComponent***. Una función que se basa en este soporte nativo para reflejar la funcionalidad de ***$.param***  no es terriblemente difícil:  
  
```javascript
function param(objeto) {
    var codificadoString = '';
    for (var prop in objeto) {
        if (objeto.hasOwnProperty(prop)) {
            if (codificadoString.length > 0) {
                codificadoString += '&';
            }
            codificadoString += encodeURI(prop + '=' + objeto[prop]);
        }
    }
    return codificadoString;
}
```
  
Si, por supuesto, el método jQuery aquí es mucho más elegante. Pero, en mi humilde opinión, uno de los pocos casos en los que jQuery notablemente mejora su código. Ciertamente no vas a tirar de jQuery sólo por el método ***$.param***, ¿verdad?  
  
## Enviando y recibiendo JSON  
  
Ahora necesitamos comunicarnos con una [API][API] que espera [JSON][JSON], y la devuelve en la respuesta. Decir que necesitamos actualizar alguna información (después de actualizar) sobre este usuario en la respuesta. El método adecuado para esta solicitud es PUT, así que es el que utilizaremos.  
  
### jQuery
  
```javascript
$.ajax('myservice/user/1234', {
    method: 'PUT',
    contentType: 'application/json',
    processData: false,
    data: JSON.stringify({
        nombre: 'John Smith',
        edad: 34
    })
})
.then(
    function success(userInfo) {
        // UserInfo será un objeto JavaScript que contiene propiedades tales 
        // como nombre, edad, direccion, etc...
    }
);
```
  
El código anterior es realmente horrible. jQuery esta repartido dentro del departamento de ajax en varios niveles. En realidad, es bastante confuso enviar cualquier cosa que no sea una petición trivial de ajax usando jQuery, en mi experiencia. El módulo de ajax de jQuery está dirigido a las solicitudes ***application/x-www-form-urlencoded***. Cualquier otro tipo de codificación requerirá que realice un poco más de trabajo.  
  
Primero tenemos que decirle a jQuery que deje los datos solos (es decir, que no lo codifique en URL). Entonces, debemos convertir el objeto JavaScript en [JSON][JSON] nosotros mismos. ¿Por qué jQuery no puede hacer esto por nosotros en base a ***contentType***? No estoy seguro.  
  
Si el servidor devuelve un tipo de contenido adecuado a la respuesta, se debe pasar el controlador de éxito un objeto JavaScript que representa el JSON devuelto por el servidor.  
  
### Web API  
  
```javascript
var xhr = new XMLHttpRequest();
xhr.open('PUT', 'myservice/user/1234');
xhr.setRequestHeader('Content-Type', 'application/json');
xhr.onload = function() {
    if (xhr.status === 200) {
        var userInfo = JSON.parse(xhr.responseText);
    }
};
xhr.send(JSON.stringify({
    nombre: 'John Smith',
    edad: 34
}));
```
  
El código anterior funcionará en IE8 y más. Pero tal vez trabajas en una empresa horrible que utiliza navegadores antiguos. En ese caso, solo tienes que añadir json.js para completar la falta de soporte de [JSON][JSON] en IE7 y versiones anteriores.  
  
## Recuperación del objeto XHR  
  
A diferencia de la mayoría de las [API][API], obtener el componente principal es un poco costoso ya que IE requiere utilizar un componente de ActiveX para que AJAX funcione.  
  
```javascript
var request;
if (window.XMLHttpRequest) { // Mozilla, Safari, ...
  request = new XMLHttpRequest();
} else if (window.ActiveXObject) { // IE
  try {
    request = new ActiveXObject('Msxml2.XMLHTTP');
  } 
  catch (e) {
    try {
      request = new ActiveXObject('Microsoft.XMLHTTP');
    } 
    catch (e) {}
  }
}
```
  
### hacer una solicitud  
  
Hacer una solicitud requiere de dos llamadas:

```javascript
request.open('GET', 'https://davidwalsh.name/ajax-endpoint', true);
request.send(null);
```
  
La llamada open define el tipo de solicitud (get, post, etc.) y el método de envío ejecuta la solicitud. ¡Muy simple! Agregar encabezados personalizados es muy sencillo:  
  
```javascript
request.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded');
```
  
### Solicitar devoluciones de llamada  
  
Por supuesto, hacer peticiones es algo inútil si no manejas el resultado, y hay dos maneras de establecer una devollución de llamada:  
  
```javascript
// cambios de estado
request.onreadystatechange = function() {
    if(request.readyState === 4) { // done
        if(request.status === 200) { // complete    
            console.log(request.responseText)
        }
    }
};

// añadir oyente de eventos
function callbackFn(e) {
    // controlador de eventos
}
request.addEventListener("progress", callbackFn, false);
request.addEventListener("load", callbackFn, false);
request.addEventListener("error", callbackFn, false);
request.addEventListener("abort", callbackFn, false);
```
  
Elija el método que desee pero el método addEventListener es probablemente el más elegante.  
  
Esta es mi sencilla introducción en la creación de solicitudes simples AJAX con la [API][API] nativa ***XMLHttpRequest***. Para obtener más información sobre las pruebas comunes de AJAX, como el envío de datos de formularios, echa un vistazo a [Mozilla Developer Network](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/Using_XMLHttpRequest)!   
   
   
   
**A tope con @mentoringJS!  
Jordi Gomper.**

[URI]: https://medialize.github.io/URI.js/
[API]: https://es.wikipedia.org/wiki/Interfaz_de_programaci%C3%B3n_de_aplicaciones
[JSON]: https://es.wikipedia.org/wiki/JSON