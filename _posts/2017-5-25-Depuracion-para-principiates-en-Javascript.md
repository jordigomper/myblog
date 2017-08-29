---
layout: post
title: Depuración para principiantes en Javascript.
img: blog/i_debuggin.png
categories: herramientas
---
[Aprende Javascript con MentoringJS - Step 5](http://mentoringjs.com/)  
  
  
Hola! En este articulo vas a adquirir las primeras nociones de como debuggar de una forma sencilla código Javascript desde nuestro navegador, bueno bonito barato!  
Para poder avanzar durante este post sin dificultad necesitas estar un poco familiarizado con la escritura de JavaScript.<!--more-->   Si llevas poco tiempo y ya vas a empezar a implementar Javascript en tu código de HTML o simplemente quieres explorar por el código de otras paginas, este articulo te va a resultar verdaderamente útil.

  
>**La depuración** es el proceso de encontrar y resolver los defectos que impiden el correcto >funcionamiento del software de computadora o un sistema. Es un concepto de la programación.  

  
## Herramienta de desarrollo  
¡Bienvenido a esta magnifica herramienta! Esta herramienta es igual de poderosa que un mono con una ballesta.  
Si para ti es nuevo, has de saber que también sirve para poder inspeccionar con el código HTML.  
  
Todos los navegadores tienen una. Personalmente la que mas me gusta es la de Google CHROME, y es la que vamos a utilizar en este articulo.  
  
**Se puede abrir a través de atajos de teclado**  
* Windows / Linux: ctrl + shift + I  
* OSX: cmd + opt + I  
  
**Desde el menú Chrome**  

![menu chrome1](https://jordigomper.github.io/myblog/img/art1-1.png)  
  
**O haciendo clic derecho en la pagina y seleccionando inspeccionar elemento**
  
![menu chrome2](https://jordigomper.github.io/myblog/img/art1-2.png)  
  
Te aparecerá en la parte inferior de nuestro navegador una ventana como esta:  
  
![menu chrome3](https://jordigomper.github.io/myblog/img/art1-3.PNG)  
  
  
### Consola  
* Es donde vamos a depurar nuestro código de JavaScript.   
* Nos muestra donde se originan los errores.  
* Puedes accederse a las bibliotecas definidas en la pagina.  

Desde la consola podemos incorporar mensajes de alerta. La alerta es una herramientas mas simples y antiguas de JavaScript. Muestra un cuadro de dialogo con el mensaje especificado. Se detendrá el código de JavaScript hasta presionar el botón de OK en la parte inferior del cuadro.  
Esto es útil para la depuración porque se puede establecer el valor de alerta con algún significado.  
Hay que cuidado de no poner una alerta en un lugar que donde se ejecute una gran cantidad de veces, por ejemplo, un bucle. Si cometemos ese fallo podemos elegir impedir que esta pagina cree cuadros de diálogos adicionales marcando la casilla dentro del cuadro de dialogo.  
  
>// Quiero Saber si llego a esta parte del código  
>alert("Estoy aquí!");  
>// Quiero saber el valor de foo en esta parte del código.  
>alert("Foo: " + foo);  
  
Si queremos consultar alguna variable, podemos utilizar console.log(nombre de la variable). Este es básicamente el equivalente JavaScript de utilizar un método de impresión para la depuración. Al igual que una alerta, podemos utilizarlo para valores de salida o comprobar que se llega a ciertos lugares en el código.  
A diferencia de una alerta, console.log no impide que el código JavaScript de continuar. Se inicia la sesión en la consola y sigue su camino feliz.  

>// Quiero saber si llego a esta parte del código.  
>console.log("Estoy aquí!");  
>// Quiero saber el valor de foo en esta parte del código.  
>console.log("Foo: " + foo);  
  
La conexión de la consola proporciona suficiente para que pueda sobrevivir, y algunos des arrolladores se detiene allí con sus habilidades de depuración de JavaScript. Sin embargo, no es siempre la mejor herramienta para el trabajo. La depuración de JavaScript compleja usando conexión de la consola puede ser lento y doloroso. Afortunadamente, hay aún más herramientas de depuración disponibles.
  
  
### Depurador interactivo  
  
Proporciona un amplio conjunto de herramientas útiles para la depuración del código. Es especialmente útil para el código JavaScript y el código complejo que interactua con otras bibliotecas. Solo actúa cuando la herramienta de desarrollador esta activa.  
  
**Podemos encontrar las siguientes funciones:**  
  
Puede iniciar el depurador en un punto específico en el código llamando debugger.
  
>// Quiero iniciar la depuración aquí.  
>debugger;
  
Con esto se nos abre una especie de menú.  En la parte derecha podemos ver las siguientes opciones:

![menu debug](https://jordigomper.github.io/myblog/img/art1-4.PNG)  
  
Si hace clic en el botón **“continuar”(1)**, continuará ejecutando el código hasta que choca con otro punto de interrupción. Una vez más, no parece ser mucho más sucede. Vamos a probar otra cosa.  
  
Haga clic para probar la depuración  
  
Si hace clic en el **“paso más”(2)**, será pasar por encima de la siguiente línea de código. Haga esto un par de veces.  
  
Con el botón **“paso en” y “salir”(3)** podemos entrar y salir de las llamadas.
  
Puedes abrir una consola en la ficha fuentes si  presionas **ESC**. Esto puede ser útil para consultar todo lo alrededor de una de las variables y otra información en ese contexto. Puede cerrar la consola pulsando **ESC** de nuevo.  
  

Hay aún más herramientas de depuración disponibles. Esas herramientas implican un poco mas de conocimiento, y las dejaremos para otra ocasión.  

Espero que el articulo te haya servido de ayuda. Sin mas, me despido, hasta la próxima!!
