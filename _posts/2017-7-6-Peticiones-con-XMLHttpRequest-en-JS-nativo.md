---
layout: post
title: Peticiones con XMLHttpRequest en JS nativo.
img: blog/i_js.png
categories: javascript
---

[Aprende Javascript con MentoringJS - Step 7](http://mentoringjs.com/)

En este articulo vamos a conocer el mejor framework de JS, [VainillaJS](http://vanilla-js.com/). Vamos a ver las bases desde una forma práctica y a conocer el uso de JavaScript sin jQuery y que es el objeto XMLHttpRequest.
<!--more-->

**El objeto XMLHttpRequest es un API en forma de objeto que se encarga de transferir datos entre un navegador web y un servidor web.** Los datos obtenidos de la petición pueden tener formato XML, JSON, HTML o texto plano. 

## Introducción:

### Vamos a seguir los siguientes pasos:
1. Instanciar el objeto XMLHttpRequest.
2. Abrir una URL y enviar la solicitud
3. Consultar el estatus de HTTP y el contenido del resultado al finalizar la transacción.
4. Intercambiar datos JSON con un servidor.
5. Codificar URI, event lisent...

## 1. Instanciar el objeto XMLHttpRequest.

Para enviar una solicitud, primero vamos a crear un objeto XMLHttpRequest.
No todos los navegadores utilizan la misma instancia del objeto XMLHttpRequest. Para hacer nuestro código compatible con cualquier navegador primero nos aseguraremos de instanciar el objeto según el tipo de navegador, vamos a condicionarlo con el siguiente código.

#### Instanciar objeto XMLHttpRequest con todos los navegadores:
```javascript
var xhr;
if (window.XMLHttpRequest) { // Mozilla, Safari, ...
  xhr = new XMLHttpRequest();
} else if (window.ActiveXObject) { // IE
  try {
    xhr = new ActiveXObject('Msxml2.XMLHTTP');
  } 
  catch (e) {
    try {
      xhr = new ActiveXObject('Microsoft.XMLHTTP');
    } 
    catch (e) {}
  }
}
```

Podemos modificar el nombre de la variable xhr a nuestro gusto.

## 2. Abrir una URL y enviar la solicitud

Con el método **open** vamos a indicar tres parámetros, el método de la petición, la url, y activar la petición de datos de forma sincróna.  

1.En el primer parámetro tenemos las opciones GET, POST, PUT, etc... En este articulo utilizaremos GET.  
  
2.El segundo articulo vamos a indicar la url. También podemos hacer solicitudes que no sean de HTTP, cambiando la url con el directorio especificado empezando por file:///home/user/archivo.tipo.  

3.En el tercer y ultimo parámetro si indicamos true o no se especifica, se procesa de forma asíncrona, de lo contrario se gestiona de forma sincróna.
  
#### Método open:
```javascript
var xhr = new XMLHttpRequest();

// Aqui indicamos el metodo, url y el tipo
xhr.open("metodo", "url/file", true/false);
```

## 3. Consultar el estatus de HTTP y el contenido del resultado al finalizar la transacción.

El método **onreadystatechange** es el responsable de manejar los eventos que se producen. Se invoca cada vez que se produce un cambio en el estado de la petición **HTTP**.Es decir, cada vez que nuestro **xhr.status** cambie, va a dispararse este método. 

### Método onreadystatechange:
```javascript
var xhr = new XMLHttpRequest();
xhr.open('GET', 'https//www.url.com?id=identificacion-unica');
// vamos a manejar los cambios de estado con el metodo onreadystatechange
xhr.onreadystatechange = function() {
    // status 200 nos indica que la respuesta es correcta
    if (xhr.status === 200) {
        // indicamos el nombre de usuario que recojemos desde la variable responseText
        alert('El nombre del usuario es ' + xhr.responseText);
    }
    // si la respuesta es incorrecta vamos a imprimir el estado
    else {
        alert('Petición fallida.  Devuelve el estado de ' + xhr.status);
    }
};
xhr.send();
```

Puedes ver que hay dos metodos nuevos, los **estados de HTTP (xhr.status)** y los diferentes **metodos para recojer los contenido (xhr.responseText)**. Esto es lo siguiente que voy a explicarte, es muy sencillo:

### Codigos de los diferentes estados HTTP (xhr.status)
* 200 respuesta es correcta.
* 403 prohibido.
* 404 no encontrado.
* 500 error del servidor.

### Métodos para recoger el contenido de una respuesta (xhr.responseText)
* **responseText** devuelve los datos de respuesta en cadena.
* **responseXML** devuelve los datos en un XML.

## 4.Intercambiar datos JSON con un servidor.

**JSON** ***(JavaScript Object Notation)*** es un formato que se usa para identificar y gestionar datos. Nació como alternativa a XML. Su uso es fácil y puede ser leido por cualquier lenguaje de programación por lo tanto puede ser usado para el intercambio de información entre distintas tecnologías.
La mayor diferencia con XML es que puede ser analizado por una función JS estándar.

Vamos a utilizar el método **JSON.parse()** para convertir el texto recibido en un Array.

Para enviar un objeto JavaScript con una notación JSON, utilizamos el metodo **JSON.stringify()**.

### Envió y recepción de datos JSON:
```javascript
var xhr = new XMLHttpRequest();
xhr.open('GET', 'https//www.url.com?id=identificacion-unica');
//
xhr.onreadystatechange = function() {
    if (xhr.status === 200) {
        // Con este metodo conseguimos transformar en un Array
        // los datos JSON que recibimos del servidor
        var userInfo = JSON.parse(xhr.responseText);
    } else {
        alert('Petición fallida.  Devuelve el estado de ' + xhr.status);
    }
};
// Aqui estamos enviando un objeto javaScript al servidor
//  con formato JSON
xhr.send(JSON.stringify({
    nombre: 'John Smith',
    edad: 34
}));
```

El código anterior no funcionara si el navegador donde se ejecuta es antiguo. En ese caso, solo tienes que añadir json.js para completar la falta de soporte de JSON en IE7 y versiones anteriores.

## 5. Codificar URI, event lisent...

En este ultimo apartado vamos a ver un par de cosas que nos ayuda a hacer nuestra peticion más modular.

### URI Encodig

La web API proviene de dos funciones que codifica URL's en Strings. La función **encodeURI()** codifica una URI. Esta función codifica caracteres especiales excepto: . / ? : @ & = + $ # (Para codificar estos caracteres utilice **encodeURIComponent()**);

La siguiente función nos codifica una URI utilizando los métodos anteriores.

### Función con **encodeURI()**:
```javascript
// Objeto seria la URI a cadoficar
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

También podemos añadir event listener según los estados de nuestra petición.

### EventListener:
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

Este articulo se basa en todo el conocimiento y experiencia que estoy adquiriendo en mi formación de mentoringJS.  
Saber utilizar JavaScript nativo es muy importante. He comprobado que con un poco mas de código puedes traspasar todas las dependencias de una aplicación con jQuery al modo nativo.  
Para más información puedes consultar la página de [Mozilla Developer Network](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/Using_XMLHttpRequest).

Espero haber ayudado en mi nuevo articulo, para cualquier duda no dudes en ponerte en contacto conmigo.

HASTA LUEGORRRRRRRR!!!!

**A tope con @mentoringJS!  
Jordi Gomper.**