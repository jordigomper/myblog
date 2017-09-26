---
layout: post
title: Deployar con Surge la app yogis!
img: blog/i_surge.png
categories: app, herramientas
---

Hola chic@s! En este articulo voy a utilizar [Surge](http://surge.sh/) para desplegar mi aplicación yogis y os voy a contar como lo hago.  

[Aprende Javascript con MentoringJS - Step 11](http://mentoringjs.com/)

[**Surge**](http://surge.sh/) es una herramienta que nos permite crear sitios estáticos. Se instala con el gestor de paquetes **npm** de Node.js y funciona con lineas de comandos de una forma muy sencilla. Nos ofrece un hosting gratuito, desde la misma consola puedes registrarte y poner el nombre de dominio que quieras. Para registrarte solo necesitas un email.  

## Como he desplegado mi aplicación con Surge
Primero de todo, he necesitado tener instalado la version de [Node.js](https://nodejs.org/en/) en su ultima versión.  

Desde la consola cmd de windows, he instalado Surge introduciendo el comando **npm install --global surge**.  
![Instalando Surge](https://jordigomper.github.io/myblog/img/a_surge/instalar.PNG "Instalando Surge")  

Una vez instalado, me posiciono desde el directorio donde se encuentra mi aplicación.  
![Directorio aplicacion](https://jordigomper.github.io/myblog/img/a_surge/directorio.PNG "Directorio aplicacion")  

Desde aquí introduzco el comando **npm run build**. Este comando crea una copia de la aplicación para producción.  
Si todo ha salido bien, tiene que salir la siguiente imagen:
![npm run build](https://jordigomper.github.io/myblog/img/a_surge/build.PNG "npm run build")
En esta pantalla dice que dentro de la carpeta de la aplicación a creado el directorio **build\static\js** y que dentro se encuentra el archivo **main.b5e1f395.js**, este archivo es la copia en producción. También indica cuanto ocupa.  

Si te ha dado algún error, revisa el archivo que te indica. Todos los componentes y líneas de código tienen que estar bien estructurados. Piensa que que este comando envía un flujo de datos por nuestra aplicación y detecta todos los fallos, es comparable a un error de compilación cuando detecta algún fallo.  
Por ejemplo, los componentes tienen que importarse cuando se utilizan en un archivo externo y también permitir su exportación.  

Ahora voy a registrarme para poder subir mi aplicación al hosting que me ofrece **Surge**.  
Introduzco el comando **surge build** y me va a pedir mi email, contraseña y  nombre del dominio.
![surge build](https://jordigomper.github.io/myblog/img/a_surge/subir.PNG "surge build")  

Automáticamente, **Surge** a subido la copia de producción a mi nuevo dominio [http://jordigomper.surge.sh]. De momento carece de css, ya que el ejercicio era contruir los componentes necesarios. También utilizo el servicio que proporciona [lorempixel](http://lorempixel.com) para generar imagenes aleatorias.  

**Surge no publicara la web hasta que no valides tu dirección de email.** Una vez la he validado, ya tengo mi aplicación desplegada y publicada.   

Ahora que ya sabes como desplegar tu aplicación, a que esperas?  

**A tope con @mentoringJS!  
Jordi Gomper.**