---
layout: post
title: Diagramas de secuencia.
img: blog/i_diagrama.PNG
categories: herramientas
---

[Aprende Javascript con MentoringJS - Step 8](http://mentoringjs.com/)  

Voy a explicar que es un diagrama de secuencia y lo voy a aplicar sobre el proyecto de TwitchTV. Dibujare la secuencia de interacción entre las distintas operaciones, funciones y actores.
<!--more-->

## Diagramas de secuencia
### Definición

Los diagramas de secuencia se usan para modelar escenarios dentro de un sistema y ofrecen una vista de análisis de bajo nivel. Esto incluye información de diseño sobre las interacciones de objetos.
El tiempo fluye por el diagrama mostrando el flujo de control de un participante a otro.  
Debemos de representar las diferentes interacciones que va a tener nuestro código sobre un escenario.

### Websequencediagrams

El programa que he utilizado para crear el diagrama ha sido [websequencediagrams](https://www.websequencediagrams.com/) en su versión gratuita. Tiene una interface intuitiva y sencilla, recomendable para nuestros primeros diagramas.  
Tenemos utilizar el cuadrado izquierdo de color azul para introducir las relaciones y el programa se encargara de crear el dibujo. 

> Unos ejemplos sencillos:  
> title Aqui escribe el titulo  
> C->D: Dibujara una fecha desde C a D.  
> C-->D: Relación de dependencia de C con D  
> C->C: Flecha recursiva a C.  
> C->+D: Crea un nuevo flujo en D.  
> D->-C: Acaba con el flujo en D.  

### Aplicándolo a TwitchTV

En este caso, vas a ver el funcionamiento que puede tener el código sobre un escenario normal, donde especificare sobre las funciones que se encargan de acceder a la información del canal y mostrarlo por pantalla.  
Voy a empezar por el flujo natural del código.  

#### Primera parte:
Cuando la página esta totalmente cargada, el código JavaScript ejecuta una función que lo primero que hace es llamar a otra función llamada **getChannelInfo**. Dejo abierta la primera función, que se sigue ejecutando hasta el final del código.   
![Primera parte](https://jordigomper.github.io/myblog/img/DdS/img1.PNG "Diagrama de secuencias")

#### Segunda parte:
Lo primero que hace la función **getChannelInfo** es hacer una instancia del objeto **[XMLHttpRequest](https://jordigomper.github.io/myblog/Peticiones-con-XMLHttpRequest-en-JS-nativo/)** y enviar una petición. Esta última, llama a la función **makeURL** para conseguir la URL donde enviar la petición. **makeURL** devuelve la URL con los datos enviados, y ya puede enviar la petición a la API. Una vez recibida, la función guarda la respuesta del servidor con la información del canal, y dependiendo de está, asigna diferentes valores a diferentes variables.
Dejo abierto el flujo de la primera instancia a **XMLHttpRequest** y abro otro **request.open** que finaliza al enviar la petición a la API, que es cuando acaba el **request.open**.  
![Segunda parte](https://jordigomper.github.io/myblog/img/DdS/img2.PNG "Diagrama de secuencias")

#### Tercera parte:
Repito el paso anterior pero esta vez enviare otro valor a **makeURL** para acceder a otra parte de la información que necesito.
Puedes ver que el flujo indica que se esta llevando esta operación dentro de la primera petición al servidor.  
![Tercera parte](https://jordigomper.github.io/myblog/img/DdS/img3.PNG "Diagrama de secuencias")

#### Cuarta parte:
Creo un elemento HTML con la información que he recogido del canal, a continuación, inserto el nuevo elemento en la DOM. El navegador actualiza la página mostrando el nuevo canal añadido.
Aquí acaba el el flujo de la primera petición.  
![Cuarta parte](https://jordigomper.github.io/myblog/img/DdS/img4.PNG "Diagrama de secuencias")

#### Ultima parte:
En la ultima parte el usuario puede seleccionar que tipo de canales quiere ver(All/Online/Offline). Cuando nuestro código de JavaScript detecta que ha sido pulsado un ".selector", primero asigna la clase ".active" al selector asignado, y después, dependiendo la selección, mostrara los canales modificando la hoja de .css.  
El usuario puede hacer clic sobre un canal y será redirigido.   
![Ultima parte](https://jordigomper.github.io/myblog/img/DdS/img5.PNG "Diagrama de secuencias")

Por ultimo hacer un pequeño comentario de las diferentes funciones o partes del código:
![Ultima parte](https://jordigomper.github.io/myblog/img/DdS/img6.PNG "Diagrama de secuencias")

**CODIGO COMPLETO:**
![Codigo completo](https://jordigomper.github.io/myblog/img/DdS/UsuarioTwitchTV.png "Diagrama de secuencias")

#### Conclusión
He tenido en cuenta las funciones mas importantes, mostrándolas lo mas sencillas posible y teniendo una idea superficial del funcionamiento que tienen el código. Si paras a mirar paso a paso todo el diagrama, vas a tener un concepto básico del funcionamiento de mi programa y puede ayudarte a resolver alguna duda de funcionamiento, prácticamente muestra casi al 80% todo el código.  

Es importante hacer un Diagrama de secuencia de nuestro código claro y sencillo, para ayudar a las posibles personas que quieran trabajar o aprender de nuestro código.  

Espero haberte ayudado, si tienes alguna duda puedes ponerte en contacto conmigo en las diferentes plataformas. 
  
Un saludo!
  
**A tope con @mentoringJS!  
Jordi Gomper.**



