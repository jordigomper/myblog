---
layout: post
title: Deployar con Surge la app yogis!
img: blog/i_surge.png
categories: app, herramientas
---

Hola chic@s! En este articulo voy a utilizar [Surge](http://surge.sh/) para desplegar mi aplicación yogis y os voy a contar como hago.  

[Aprende Javascript con MentoringJS - Step 11](http://mentoringjs.com/)

[**Surge**](http://surge.sh/) es una herramienta que nos permite crear sitios estáticos. Se instala desde el gestor de paquetes **npm** de Node.js y funciona con lineas de comandos de una forma muy sencilla. Nos ofrece un hosting, desde la misma consola puedes registrarte y poner el nombre de dominio que quieras. Para registrarte solo necesitas un email. Es totalmente gratuito.  

## Como he desplegado mi aplicación con Surge
Primero de todo, he necesitado tener instalado la version de [Node.js](https://nodejs.org/en/) en su ultima versión.  

Desde la consola cmd de windows, he instalado Surge introduciendo el comando **npm install --global surge**.  
![Instalando Surge](https://jordigomper.github.io/myblog/img/a_surge/instalar.PNG "Instalando Surge")  

Una vez instalado, me posiciono desde el directorio donde se encuentra mi aplicación.  
![Directorio aplicacion](https://jordigomper.github.io/myblog/img/a_surge/directorio.PNG "Directorio aplicacion")  

Desde aquí he introducido el comando **npm run build**. Este comando crea una copia de nuestra aplicación para producción.  
Si todo ha salido bien, tiene que salir la siguiente imagen:
![npm run build](https://jordigomper.github.io/myblog/img/a_surge/directorio.PNG "npm run build")
En esta pantalla, dice que dentro de la carpeta de la aplicación a creado el directorio **build\static\js** y que dentro se encuentra el archivo **main.b5e1f395.js**, este archivo es la copia en producción de mi aplicación. También indica cuanto ocupa.  

Si te ha dado algún error, revisa el archivo que te indica. Todos los componentes y líneas de código tienen que estar bien estructurados. Piensa que surge envía un flujo de datos por nuestra aplicación y detecta todos los fallos, es comparable a un error de compilación cuando detecta algún fallo.  
Por ejemplo, los componentes tienen que importarse cuando se utilizan en un archivo externo y también permitir su exportación.
En mi caso, mi aplicación todavía no tiene ninguna función, solo la estoy descomponiendo. Hay componentes que no están llamados en ningún lugar, entonces desde el componente **App.js** los he importado aunque no los utilice, si no lo hago, esos componentes no se incluyen en mi copia de producción.  

Ahora voy a registrarme para poder subir mi aplicación al hosting que me ofrece **Surge**.  
Introduzco el comando **surge build** y me va a pedir mi email, contraseña y  nombre del dominio.
![surge build](https://jordigomper.github.io/myblog/img/a_surge/subir.PNG "surge build")  

Automáticamente, **Surge** a subido la copia de producción a mi nuevo dominio http://jordigomper.surge.sh.  
**Surge no publicara la web hasta que no valides tu dirección de email.** Una vez la he validado, ya tengo mi aplicación desplegada y publicada.
En mi caso no mostrara nada, ya que todavía no tiene contenido.  

Ahora que ya sabes como desplegar tu aplicación, a que esperas?  

**A tope con @mentoringJS!  
Jordi Gomper.**