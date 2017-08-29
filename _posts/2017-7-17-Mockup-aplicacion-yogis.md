---
layout: post
title: Mockup de mi nueva aplicación yogis.
img: blog/i_app.jpg
categories: app
---
  
[Aprende Javascript con MentoringJS - Step 9](http://mentoringjs.com/)

Quiero presentar mi nuevo proyecto. Yogis va a ser una aplicación para móvil, donde una profesora de yoga puede promocionar un estilo de vida saludable. Es una aplicación tipo blog, donde subirá artículos, videos, fotos... pudiendo compartir las publicaciones con facebook y instragram<!--more-->  
Su interfaz va a ser muy sencilla. Con un menú que solo se muestra al pulsar el botón, el usuario tiene diversos apartados. El diseño va a ser bonito y a la vez sencillo, con colores suaves.  

[Mockup de yogis en Github](https://github.com/jordigomper/mockups-yogis)

## Ratchet
Para crear este mockup he utilizado el framework Ratchet, un conjunto de herramientas html, css y JS para realizar prototipos rápidamente. Solo tenemos que descargaro y crear un index.html, vinculando su css y JS tal y como indica en su [página oficial](http://goratchet.com/). Luego, desde la seccion de components, puedes escojer menus, submenus, botones...  

Utiliza las siguientes indicaciones para seguir una estructura básica:  
1. Si desea agregar una barra fija,  añade la clase .bar en el header. Asegúrate de que es lo primero dentro del body.  
2. Cualquier cosa que no esté en la clase .bar debe ir dentro de una div con la clase .content.  
3. Asegúrese de agregar las etiquetas adecuadas (incluidas en los ejemplos).

Siguiendo estos paso, ya podemos empezar a construir nuestra mockup

## Aplicación yogis
### Características principales
La aplicación debe permitir una gestión desde el móvil para publicaciones diarias como una figura, un batido... Y desde la web para artículos un poco más complejos que contendrá más imágenes y un diseño especial. Las publicaciones diarias podrán compartirse con facebook y/o instragram. Cada publicación deberá tener una etiqueta predefinida tipo yoga, batido, postura...

La página principal contendrá al principio una presentación de la profesora, después mostrara el ultimo articulo, batido, figura y video. 

Seleccionando el botón del menú, mostrara secciones tipo: artículos, batidos, figuras... Al seleccionar mostrara lo deseado. Desde la misma página eliminara todo el contenido actual y buscara por la etiqueta la sección indicada.

Va a tener un gestor de retos eventuales. La profesora abre un reto unos días antes, el cual saldrá promocionado en la página principal. El usuario puede inscribirse en el reto, y se le abre una nueva pestaña en el menú con el nombre de reto. Seleccionado la pestaña podrá ver la página principal del reto que contiene la información del reto (un video explicándolo, una lista con las cosas necesarias, objetivo del reto...). Esta página contiene un muro de facebook generado especialmente para ese reto donde los participantes pueden exponer sus dudas. También se muestra un submenú donde hay 3 secciones: principal, reto del día, calendario. El principal es donde estamos, si vamos al reto del día sale información del reto del día, un muro y un botón que al pulsar se abre la cámara, haces una foto y se sube directamente al muro de la profesora, si puede ser con una frase fija y hastah tipo #retodia1 conseguido!. En el muro se mostraran todos los que han publicado su foto. En el calendario sale desde el inicio al final del reto cada día información en pequeño de cada día. El día actual ha de mostrarse de un color especial.  
Durante el reto, diariamente llegara alertas a los inscritos recordándoles que hay un reto en curso.

Ahora os presento la aplicación sección por sección.

#### index.html:
Contiene una presentación de la profesora, después el ultimo articulo, batido, figura y video. Desplazamiento en vertical.

![Index yogis](https://jordigomper.github.io/myblog/img/a_mockup_yogis/index.PNG "Aplicación yogis")

Menú desplegable al pulsar el botón, para las secciones de tipo artículos, batidos, videos... borrara el contenido y buscara solo lo seleccionado.

![Menú yogis](https://jordigomper.github.io/myblog/img/a_mockup_yogis/menu.PNG "Aplicación yogis")

#### articulos.html:
Al seleccionar sobre un articulo, batido, video... la aplicación abre esta página con toda la información detallada. Deslizando la pantalla hacia los lados o pulsando las flechas laterales te desplazara por las diferentes publicaciones del tipo que hayas seleccionado.

![Menú yogis](https://jordigomper.github.io/myblog/img/a_mockup_yogis/articulos.PNG "Aplicación yogis")

![Menú yogis](https://jordigomper.github.io/myblog/img/a_mockup_yogis/articulos3.PNG "Aplicación yogis")

Deslizando la pantalla:

![Menú yogis](https://jordigomper.github.io/myblog/img/a_mockup_yogis/articulos2.PNG "Aplicación yogis")

#### retos.html:
Incorpora un submenú para poder moverte por las 3 secciones:

![Menú yogis](https://jordigomper.github.io/myblog/img/a_mockup_yogis/retos-principal.PNG "Aplicación yogis")

**Reto principal:**
Contiene toda la información del reto (objetivo, cosas necesarias....). Si no estas inscrito solo puedes acceder a esta sección.  
Primero podemos ver un botón unirse al reto. Después información del reto. En la parte inferior encontramos el muro de facebook donde la gente puede exponer sus dudas.

![Menú yogis](https://jordigomper.github.io/myblog/img/a_mockup_yogis/retos-principal2.PNG "Aplicación yogis")

![Menú yogis](https://jordigomper.github.io/myblog/img/a_mockup_yogis/retos-principal3.PNG "Aplicación yogis")

**Reto del DIA:**
Muestra información del reto del DIA. Después un botón "Conseguido!", al pulsar abre la cámara, haces una foto y se sube a la página principal de la profesora con unos hastah prefijados. En el muro de más abajo se mostrarán todas las personas que han subido la foto. En este muro no se puede escribir, solo es para incentivar a que la gente participe, para cualquier duda tienen que ir a la página principal del reto.

![Menú yogis](https://jordigomper.github.io/myblog/img/a_mockup_yogis/retos-dia.PNG "Aplicación yogis")

![Menú yogis](https://jordigomper.github.io/myblog/img/a_mockup_yogis/retos-dia2.PNG "Aplicación yogis")

**Reto calendario:**
Muestra un calendario con la información diaria del reto. 

![Menú yogis](https://jordigomper.github.io/myblog/img/a_mockup_yogis/retos-calendario.PNG "Aplicación yogis")

### Proceso de construcción con [mentoringJS](http://mentoringjs.com/)
La formación de mentoringJS incluye un proyecto personal. Cada vez me encuentro más capacitado para hacer frente a la construcción de mi proyecto gracias a este curso, que te da la capacidad de utilizar todas las tecnologías actuales en el mundo del desarrollo. Por ejemplo, podéis visitar[ mi ultimo proyecto](https://jordigomper.github.io/myblog/Proyecto-TwitchTV-con-VainillaJS/) construido solo con JavaScript nativo.  


Esta presentación es un mockup, una estructura de html, css, js sin función ninguna y con un diseño funcional, papel y piedra... Ahora desde mentoringJS empieza mi formación con React.js, un framework muy de moda de JS y que e permitirá desarrollar mi proyecto personal.  
En la primera fase de construcción empezamos con React.js y dividiré estas páginas en componentes y añadiré componentes React.js al mockup.Teneis la oportunidad de ver como desarrollo mi aplicación desde mi Github y Twitter, vais a ver que chulo va a quedar!

Hasta aquí esta breve presentación, si tienes alguna duda o sugerencia puedes ponerte en contacto conmigo.

Un saludo!!!

**A tope con @mentoringJS!  
Jordi Gomper.**