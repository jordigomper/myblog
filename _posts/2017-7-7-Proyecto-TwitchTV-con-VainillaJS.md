---
layout: post
title: TwitchTV con VainillaJS.
img: blog/i_twitch.jpg
categories: javascript
---

[Aprende Javascript con MentoringJS - Step 7](http://mentoringjs.com/)

En este articulo vamos a pasar un antiguo proyecto que utiliza jQuery a VainillaJS. Vamos a utilizar la API de [Twitch Developers](https://dev.twitch.tv/) para hacer una página que nos da información de varios canales.
  
<html>
<head>
  <meta charset="utf-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <title>Twitch tv</title>
  <!--CSS-->
  <style type="text/css">
    * {
  color: #767677;
  font-family: 'Ruda', sans-serif;
}

body {
  background: #111111 !important;
}

.container {
  margin: 10px;
  max-width: 720px;
  min-width: 440px;
  
}

#title {
  font-family: 'Bungee Inline', cursive;
}

#header {
  background: #171717;
  border-bottom: 1px solid #767677;
  margin: 0px;
}

.menu {
  padding: 10px;
}
.menu>ul {
    list-style-type: none;
    margin: 0;
    padding: 0;
}

.menu>ul>li {
    display: inline;
    padding: 20px;
}

.menu>ul>li a:hover {
  color: white;
}

.menu>ul>li a:focus {
  color: white;
}

.menu>ul>li a#online:focus {
  border-bottom: 2.5px solid #E62356;
}

.menu>ul>li a#offline:focus {
  border-bottom: 2.5px solid #25B4E5;
}

.menu>ul>li a#all:focus {
  border-bottom: 2.5px solid #712CDD;
}

.menu>ul>li a {
    color: #767677 ;
    text-decoration: none;
    padding: 11px;
}

.logo {
  width: 75px;
  border-radius: 50%;
}

#icon {
  text-align: center;
  margin: 10px 0px;
  /*padding: 20px 20px;*/
}

#display {
  background: #181818;
  margin-top: 0px;
  padding: 10px 0px 10px 10px;

}

#canal {
  background: #282828;
  margin: 20px 0px 20px 20px;
  border-radius: 75px 0px 0px 75px;
  /*max-height: 130px;*/
  border-right: 1px solid #767677;

}

#streaming {
  text-align: right;
  /*padding: 60px 10px;*/
}

#name {
  font-size: 15px;
  text-align: center;
  /*padding-top: 60px;*/
}

#name>a {
  color: #767677;
}

#name>a:hover {
  color: white;
  text-decoration: none;
}

.col-md-3 {
  padding-top: 40px; 
}

.col-md-7 {
  padding-top: 40px;
}
  </style>
  <!-- bootstrap CDN -->
  <!-- Latest compiled and minified CSS -->
  <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css" integrity="sha384-BVYiiSIFeK1dGmJRAkycuHAHRg32OmUcww7on3RYdg4Va+PmSTsz/K68vbdEjh4u" crossorigin="anonymous">
  <!-- Optional theme -->
  <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap-theme.min.css" integrity="sha384-rHyoN1iRsVXV4nD0JutlnGaslCJuC7uwjduW9SVrLvRYooPp2bWYgmgJQIXwl/Sp" crossorigin="anonymous">
  <!-- font-awesome CDN -->
  <link href="https://maxcdn.bootstrapcdn.com/font-awesome/4.6.3/css/font-awesome.min.css" rel="stylesheet" integrity="sha384-T8Gy5hrqNKT+hzMclPo118YTQO6cYprQmhrYwIiQ/3axmI1hQomh7Ud2hPOy8SP1" crossorigin="anonymous">
  <!--jQuery-->
  <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.1.1/jquery.min.js"></script>
  <!--Google font-->
  <link href="https://fonts.googleapis.com/css?family=Ruda" rel="stylesheet">
  <link href="https://fonts.googleapis.com/css?family=Bungee+Inline" rel="stylesheet">
</head>
<body>
  
  <div class="container">
    <!--T´tulos-->
    <div id="contenido">
      <div id="header">
        <div class="row text-center">
          <h1 id="title">TWITCH STREAMERS</h1>
          <div class="menu">
            <ul>
              <li><a class="selector" id="all" href="#">ALL</a></li>
              <li><a class="selector" id="online" href="#">ONLINE</a></li>
              <li><a class="selector" id="offline" href="#">OFFLINE</a></li>
            </ul>
          </div>
        </div>
      </div>
      <!--Aquí se visualizan los canales-->
      <div id="display">
      </div>

      <!--Pie de página-->
      <div class="row" id="footer">
      </div>
    </div>
  </div>



  <!--JavaScript-->
  <script>
    var channels = ["freecodecamp", "ESL_SC2", "OgamingSC2", "cretetion", "storbeck", "habathcx", "RobotCaleb", "noobs2ninjas", "brunofin", "comster404"];

function getChannelInfo() {
    //Las urls
    channels.forEach(function(channel) {
        function makeURL(type, name) {
            return 'https://api.twitch.tv/kraken/' + type + '/' + name + '?client_id=c8a3wkkb56yqjhlcui7tcfyjvs65dy6';
        };

        const req = new XMLHttpRequest();
        req.open('GET', makeURL("streams", channel));
        req.onreadystatechange = function() {
            if (req.readyState === 4) {
                if (req.status === 200) {
                    var data = JSON.parse(this.response),
                        game,
                        status;

                    if (data.stream === null) {
                        game = "Offline";
                        status = "offline";
                    } else if (data.stream === undefined) {
                        game = "Not found";
                        status = "offline";
                    } else {
                        game = data.stream.game;
                        status = "online";
                    };

                    const req = new XMLHttpRequest();
                    req.open('GET', makeURL("channels", channel));
                    req.onreadystatechange = function() {
                        if (req.readyState === 4) {
                            if (req.status === 200) {
                                var data = JSON.parse(this.response);
                                var logo = data.logo != null ? data.logo : "https://dummyimage.com/50x50/ecf0e7/5c5457.jpg&text=0x3F",
                                    name = data.display_name != null ? data.display_name : channel,
                                    description = status === "online" ? ': ' + data.status : "";

                                var html = document.createElement("div");
                                html.innerHTML = '<div class="row ' + status + '" id="canal"><div class="col-xs-2 col-md-2" id="icon"><img src="' +
                                    logo + '" class="logo"></div><div class="col-xs-5 col-md-3" id="name"><a href="' +
                                    data.url + '" target="_blank">' + name + '</a></div><div class="col-xs-5 col-md-7" id="streaming">' +
                                    game + '<span class="hidden-xs">' + description + '</span></div></div>';

                                //Pongo a los que están online los primeros de la lista y a los offline los últimosç
                                var qdisplay = document.getElementById("display")
                                status === "online" ? qdisplay.prepend(html) : qdisplay.appendChild(html);
                            } else {
                                console.log("Error, " + req.StatusText);
                            }
                        }
                    };
                    req.send();

                } else {
                    console.log("Error, " + req.StatusText);
                }
            }
        };
        req.send();

    });
};

window.addEventListener("load", function() {
    getChannelInfo();

    var selector = document.querySelectorAll('.selector');
    selector.forEach((e) => {
        e.addEventListener('click', function() {

            selector.forEach((e) => {
                e.classList.remove('active');
            });
            this.classList.add('active');

            var status = this.id;
            var selectorAll = document.querySelectorAll('#canal');
            var selectorOnline = document.querySelectorAll('.online');
            var selectorOffline = document.querySelectorAll('.offline');

            if (status === "all") {
                selectorAll.forEach((e) => {
                    e.classList.remove("hidden");
                })
            } else if (status === "online") {
                selectorOnline.forEach((e) => {
                    e.classList.remove("hidden");
                })
                selectorOffline.forEach((e) => {
                    e.classList.add("hidden");
                })
            } else {
                selectorOffline.forEach((e) => {
                    e.classList.remove("hidden");
                })
                selectorOnline.forEach((e) => {
                    e.classList.add("hidden");
                })
            };
        });
    });
});

  </script>

  <script src="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/js/bootstrap.min.js" integrity="sha384-Tc5IQib027qvyjSMfHjOMaLkfuWVxZxUPnCJA7l2mCWNIpG9mGCD8wGNIcPD7Txa" crossorigin="anonymous"></script> 
</body>
</html>  
  



## Introducción
1. Hacer fork de la repro en GitHub.
2. Analizar el funcionamiento del programa.
3. Liberar TwitchTV de jQuery.

## 1. Hacer fork de la repro en GitHub.

Para empezar necesitas descargar proyecto original de TwitchTV que se basa en peticiones jQuery.  
Haz click en este [link](https://github.com/jordigomper/twitchtv) y a continuación, en la parte derecha superior, pulsa el botón Fork. Una vez realizada esta operación ya tienes el proyecto original en tu GitHub.  
  
Este proyecto esta construido con el framework CSS **Boostrap**, si no estas familiarizado con el te aconsejo buscar información. Boostrap te permite dar forma a un sitio web mediante librerías CSS que incluyen botones, cuadros, menús...


## 2. Analizar el funcionamiento del programa.
  
Vamos a analizar el código. Podemos dividirlo en 2 partes:

### Parte 1
```javascript
$(document).ready(function() {
  getChannelInfo();
  

  //Cuando pulso los botones del menú
  $(".selector").click(function() {

    $(".selector").removeClass("active");
    $(this).addClass("active");
    var status = $(this).attr('id');

    if (status === "all") {
      $(".online, .offline").removeClass("hidden");
    } else if (status === "online") {
      $(".online").removeClass("hidden");
      $(".offline").addClass("hidden");
    } else {
      $(".offline").removeClass("hidden");
      $(".online").addClass("hidden");
    }


  });

});
```

Esta parte del código, se encarga de llamar la función **getChannelInfo()** cuando la página esta cargada. También contiene un **controlador de eventos**, que al pulsar un elemento que que este dentro de este selector, ejecuta una función. Esta function se encarga de añadir y eliminar diferentes clases que se encargan de mostrar o ocultar ciertos elementos dependiendo del botón pulsado.

### Parte 2
```javascript
var channels = ["freecodecamp", "ESL_SC2", "OgamingSC2", "cretetion", "storbeck", "habathcx", "RobotCaleb", "noobs2ninjas", "brunofin", "comster404"];

function getChannelInfo() {
  //Las urls
  channels.forEach(function(channel) {
    function makeURL(type, name) {
      return 'https://wind-bow.hyperdev.space/twitch-api/' + type + '/' + name + '?callback=?';
    };

    
    $.getJSON(makeURL("streams", channel), function(data) {
      var game,
          status;
      if (data.stream === null) {
        game = "Offline";
        status = "offline";
      } else if (data.stream === undefined) {
        game = "Not found";
        status = "offline";
      } else {
        game = data.stream.game;
        status = "online";
      };

      $.getJSON(makeURL("channels", channel), function(data) {
        var logo = data.logo != null ? data.logo : "https://dummyimage.com/50x50/ecf0e7/5c5457.jpg&text=0x3F",
          name = data.display_name != null ? data.display_name : channel,
          description = status === "online" ? ': ' + data.status : "";

          html = '<div class="row ' + status + '" id="canal"><div class="col-xs-2 col-md-2" id="icon"><img src="' + 
          logo + '" class="logo"></div><div class="col-xs-5 col-md-3" id="name"><a href="' + 
          data.url + '" target="_blank">' + name + '</a></div><div class="col-xs-5 col-md-7" id="streaming">'+ 
          game + '<span class="hidden-xs">' + description + '</span></div></div>';

        //Pongo a los que están online los primeros de la lista y a los offline los últimos
        status === "online" ? $("#display").prepend(html) : $("#display").append(html);
      });
    });
  });
};
```

Esta es la segunda parte la cual se encuentra en la parte superior del código. Podemos ver un Array que contiene el nombre de varios canales.  
A continuación vemos la función **getChannelInfo()** que es llamada automáticamente cuando la web está cargada. Ahora vamos a ir comentando el código paso a paso, de arriba a abajo.

Paso 1:
```javascript
 channels.forEach(function(channel) {
    //.....
  });
```
 Esta función va a recorrer la Array channels y va a ejecutar todo el código de su interior por cada canal que encuentre hasta llegar al final. Se extiende hasta el final de la función **getChannelInfo()**.

Paso 2:
```javascript
function makeURL(type, name) {
  return 'https://wind-bow.hyperdev.space/twitch-api/' + type + '/' + name + '?callback=?';
};
```
**makeURL** Recibe 2 parametros:  
**type:** Los valores deben ser streams o channels, necesitamos hacer esas 2 tipos de peticiones por cada canal para recibir la información total que deseamos. Streams muestra si el canal esta emitiendo ahora mismo y channels nos proporciona información del canal.  
**name:** Es el nombre del canal. Es una propiedad de forEach.  

Esta función devuelve la URL que necesitamos para hacer las peticiones.

Paso 3:
```javascript
 $.getJSON(makeURL("streams", channel), function(data) {
    var game,
        status;
    if (data.stream === null) {
      game = "Offline";
      status = "offline";
    } else if (data.stream === undefined) {
      game = "Not found";
      status = "offline";
    } else {
      game = data.stream.game;
      status = "online";
    };

      //......

      });
```
Esto es una petición con jQuery. Con la función makeURL crea una URL, donde hace una petición. El servidor nos devuelve una respuesta con la información solicitada. Vamos hacer una petición sobre **streams**, esto nos informara si el canal esta emitiendo.  

Creamos 2 variables games, status. Hemos recibido la información del servidor sobre **data.stream** que nos dice si el canal esta emitiendo ahora mismo. Dependiendo del estado de **data.stream** asignaremos un valor a game y status las cuales utilizaremos más abajo.

Paso 4:
```javascript
 $.getJSON(makeURL("channels", channel), function(data) {
    var logo = data.logo != null ? data.logo : "https://dummyimage.com/50x50/ecf0e7/5c5457.jpg&text=0x3F",
      name = data.display_name != null ? data.display_name : channel,
      description = status === "online" ? ': ' + data.status : "";

      html = '<div class="row ' + status + '" id="canal"><div class="col-xs-2 col-md-2" id="icon"><img src="' + 
      logo + '" class="logo"></div><div class="col-xs-5 col-md-3" id="name"><a href="' + 
      data.url + '" target="_blank">' + name + '</a></div><div class="col-xs-5 col-md-7" id="streaming">'+ 
      game + '<span class="hidden-xs">' + description + '</span></div></div>';

    //Pongo a los que están online los primeros de la lista y a los offline los últimos
    status === "online" ? $("#display").prepend(html) : $("#display").append(html);
  });
```

Hacemos una ultima petición al servidor con el tipo **channels**. esto nos devuelve información del canal.  
Vamos a asignar diferentes variables dependiendo de la información recibida.  

Fijate después del salto de linea, cuando empieza la variable html. Html es la variable que contiene la información individual de cada canal y que se muestra por pantalla, es decir, es nuestro elemento HTML que se mostrara por pantalla. Vamos a asignarle una clase row+status(online/offline) dependiendo de como este el canal. Asignaremos el logo y la url para el link, el juego actual y la descripción.  
Al final ordena los canales dependiendo del status online/offline utilizando los métodos **prepend()** y **append()** de jQuery.  

Con esto ya tenemos todo el código desglosado. Vamos a pasarlo a VainillaJS.
  
Voy a comentar por encima las principales diferencias que podemos encontrar a la hora de pasar todo el código a VainillaJS.  
El **controlador de eventos** es un método de jQuery. En VainillaJS vamos a utilizar el EventListener, muy parecido.  
Las **peticiones al servidor** son distintas. Esta es la principal diferencia.
Entre otras cosas también veras, selectores de elementos (querySelector) selectores de nodos de DOM (getElementByID), los métodos para modificar las clases de los elementos son distintos etc....

### 3. Liberar TwitchTV de jQuery.

Paso 1 VainillaJS:
```javascript
window.addEventListener("load", function() {
  getChannelInfo();

  var selector = document.querySelectorAll('.selector');
  selector.forEach((e) => {
    e.addEventListener('click', function() {
      selector.forEach((e) => {
        e.classList.remove('active');
      });
      this.classList.add('active');

      var status = this.id;
      var selectorAll = document.querySelectorAll('#canal');
      var selectorOnline = document.querySelectorAll('.online');
      var selectorOffline = document.querySelectorAll('.offline');

      if (status === "all") {
        selectorAll.forEach((e) => {
          e.classList.remove("hidden");
        })
      } else if (status === "online") {
        selectorOnline.forEach((e) => {
          e.classList.remove("hidden");
        })
        selectorOffline.forEach((e) => {
          e.classList.add("hidden");
        })
      } else {
        selectorOffline.forEach((e) => {
          e.classList.remove("hidden");
        })
        selectorOnline.forEach((e) => {
          e.classList.add("hidden");
        })
      };
    });
  });
});
```

El manejador de eventos de VainillaJS es el **Event Listener**. Decimos que cuando el objeto windows(página) este cargado(load) ejecute el siguiente código.

Primero llamamos a la función **getChannelInfo()**.  
Ahora vamos a utilizar los selectores(querySelector) para poder modificar los elementos que tenemos dentro del DOM. Seleccionamos elementos con clase .selector que son los tres botones principales de la pagina(All/Online/Offline). Aqui a añadir un event listener a cada elemento que se activara al pulsarlo(click).  
Cuando pulsamos un .selector vamos a borrar la clase .active de todos los elementos en .selector y a continuación vamos a añadírselo solo al .selector pulsado. Para esto vamos a utilizar el método classList. La clase .active indica que botón ha sido pulsado el ultimo.  
Vamos a asignar a la variable status la id que contiene el .selector pulsado (All/Online/Offline) y vamos a utilizar selectores para los diferentes elementos que se han creado.  
Dependiendo de status, recorreremos los diferentes selectores añadiendo o borrando la clase .hidden que es la que se encarga de ocultar dichos elementos. Como puedes ver, aquí ya estamos modificando los diferentes elementos(div) que hemos creado dependiendo de los canales. Fijate que los selectores selectorOnline y selectorOffline hacen referencia a las clases .online y .offline que se asignan a cada canal dependiendo del status, no te confundas con las id's #all, #online y #offline de los botones.

Paso 2 VainillaJS
```javascript
var channels = ["freecodecamp", "ESL_SC2", "OgamingSC2", "cretetion", "storbeck", "habathcx", "RobotCaleb", "noobs2ninjas", "brunofin", "comster404"];

function getChannelInfo() {
    //Las urls
    channels.forEach(function(channel) {
        function makeURL(type, name) {
            return 'https://api.twitch.tv/kraken/' + type + '/' + name + '?client_id=c8a3wkkb56yqjhlcui7tcfyjvs65dy6';
        };
    });
});
```

Subimos hacia la segunda parte. Todo esto es igual, solo hay que modificar el return de la función makeURL añadiendo el client_id para que el servidor nos permita hacer varias peticiones.

Paso 3 VainillaJS
```javascript
const req = new XMLHttpRequest();
req.open('GET', makeURL("streams",channel));
req.onreadystatechange = function() {
  if (req.readyState === 4) {
    if (req.status === 200) {
      var data = JSON.parse(this.response),
          game,
          status;

      if (data.stream === null) {
          game = "Offline";
          status = "offline";
      } else if (data.stream === undefined) {
          game = "Not found";
          status = "offline";
      } else {
          game = data.stream.game;
          status = "online";
      };
    }
  }
};
```

Vamos a enviar la petición haciendo uso del objeto de navegador **XMLHttpRequest**. Si no sabes nada de esto, visita [mi anterior articulo donde explico que es y como utilizar XMLHttpRequest](https://jordigomper.github.io/myblog/Peticiones-con-XMLHttpRequest-en-JS-nativo/). Esta es la gran diferencia con jQuery. Las peticiones jQuery son mas sencillas, pero si dedicas un poco de tiempo a tu formación vas a aprender a hacer peticiones con JavaScript vainilla y vas a darte cuenta que no es difícil.  
Con el método open enviamos la petición. **Onreadystatechange** se dispara cuando detecta que el status ha cambiado. El primer **if (req.readyState === 4)** son los valores predefinidos sobre la instancia del objeto **XMLHttpRequest**, cuando devuelve 4 es que esta completo. El siguiente **if (req.status === 200)** son los códigos de los diferentes **estados de la petición HTTP**, 200 si la respuesta es correcta.  
Después de pasar esta serie de filtros, vamos a guardar los datos recibidos en **formato JSON** y lo vamos a **transformar en un Array de JS con el método JSON.parse()**. Dentro pondremos la variable **this.response** que es la respuesta que nos ha dado el servidor con la información de la petición. Todo esto lo agregamos a la variable data.  
Creamos dos variables más, game y status. Dependiendo de la información que hemos recibido que se encuentra en la variable data, daremos diferentes valores a game y status. Recordad que esto se ejecuta en cada canal.

**Los valores definidos para la propiedad readyState son los siguientes:**  

*  0 - No inicializado (objeto creado, pero no se ha invocado el método open)  
*  1 - Cargando (objeto creado, pero no se ha invocado el método send)  
*  2 - Cargado (se ha invocado el método send, pero el servidor aún no ha respondido)  
*  3 - Interactivo (se han recibido algunos datos, aunque no se puede emplear la propiedad responseText)  
*  4 - Completo (se han recibido todos los datos de la respuesta del servidor)  
  
**Códigos de los diferentes estados HTTP status:**

*  200 - respuesta es correcta.
*  403 - prohibido.  
*  404 - no encontrado.
*  500 - error del servidor.

Paso 4 VainillaJS:
```javascript
const req = new XMLHttpRequest();
req.open('GET', makeURL("channels",channel));
req.onreadystatechange = function() {
  if (req.readyState === 4) {
    if (req.status === 200) {
      var data = JSON.parse(this.response);
      var logo = data.logo != null ? data.logo : "https://dummyimage.com/50x50/ecf0e7/5c5457.jpg&text=0x3F",
          name = data.display_name != null ? data.display_name : channel,
          description = status === "online" ? ': ' + data.status : "";

      html = '<div class="row ' + status + '" id="canal"><div class="col-xs-2 col-md-2" id="icon"><img src="' +
          logo + '" class="logo"></div><div class="col-xs-5 col-md-3" id="name"><a href="' +
          data.url + '" target="_blank">' + name + '</a></div><div class="col-xs-5 col-md-7" id="streaming">' +
          game + '<span class="hidden-xs">' + description + '</span></div></div>';

      //Pongo a los que están online los primeros de la lista y a los offline los últimos
      var qdisplay = document.getElementById("display")
      status === "online" ? qdisplay.prepend(html) : qdisplay.appendChild(html);

    } else {
        console.log("Error, " + req.StatusText);
    }
  }
};
req.send();

} else {
console.log("Error, " + req.StatusText);
}
}
};
req.send();

});
};
```

Vamos a por el ultimo paso. Continuando dentro de la anterior petición, vamos hacer otra petición, pero esta vez a channels para poder obtener información del canal solicitado. Todo es igual que su predecesora.  
Dependiendo de la formación obtenida, vamos a asignar las variables logo, name, channel, description.  
Después del salto de linea, encontramos la variable html. Esta es la variable que contiene todo el código HTML con la información del canal y que convertiremos en un elemento que mostraremos por pantalla. Lo más importante aquí es la clase row+status. Esta clase indica si el canal esta online o offline.  
Creamos un selector del nodo de la DOM que contiene la ID #display, es la el elemento div que hace de contenedor de los elementos con la información de los canales. Si el estatus del canal es online, insertaremos el elemento html que contiene toda la información desde arriba y desde abajo si el canal es offline. Al ordenar los canales estamos modificando la DOM.
  
Acabamos la parte del código que cierran las dos peticiones. Podemos ver el método **send()**, es el que se encarga de enviar información al servidor pero en este caso no lo hemos utilizado.  
También vemos 2 else's que contienen el error, cuando no se cumplen la condición del primer if nos indica que a pasado.  
  
Con esto acabamos este articulo.

Como puedes comprobar no es tan costoso utilizar VainillaJS si tenemos en cuenta todas sus ventajas. 

Para descargarte del código completo este [link](https://codepen.io/JordiGomper/pen/gRvYLo) te envia a codepen donde podras copiarlo. 
  
Espero haberte ayudado, si tienes alguna duda no dudes en ponerte en contacto conmigo, UN SALUDO!!! 
  
**A tope con @mentoringJS!  
Jordi Gomper.**
