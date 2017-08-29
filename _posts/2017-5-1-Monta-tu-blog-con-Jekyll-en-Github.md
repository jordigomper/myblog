
---
layout: post
title: Crea tu blog con Jekyll en GitHub en solo unos minutos
img: blog/jekyll-logo.png
categories: articulo
---  
[Aprende Javascript con MentoringJS - Step 4](http://mentoringjs.com/)  
  
Este articulo esta escrito sobre mi experiencia a la hora de montar un blog en GitHub con Jekyll. Tengo muy poca experiencia con este editor, así que te hablare de todas las dudas y respuestas que obtuve en el proceso.  
  
## Que es Jekyll?  
Jekyll es una herramienta para la creación de blogs estáticos escrito por Tom Preston-werner, uno de los creadores de Github. Esta programado en Ruby, es de código abierto y totalmente gratuito. Su principal ventaja es que traduce todos nuestros contenidos escritos en Markdown a HTML, así simplemente nos preocuparemos de escribir y nada más. No necesita de código que se ejecute en el servidor y no utiliza PHP o MySQL, esto proporciona mayor seguridad en explotación de vulnerabilidades en estas tecnologías. Es la ***opción perfecta para integrar en nuestro Github un blog*** y como ultimo dato hay que decir que su [pagina web](https://jekyllrb.com/docs/quickstart/) esta alojada en los servidores de Github.  
  
## Instalar Jekyll en tan solo unos minutos  

Llegar a controlar Jekyll puede ser muy complicado, así que ahora que ya tenemos una idea del concepto para crear blogs que nos ofrece, voy a enseñarte la opción mas sencilla para instalar un blog en tu Github.  

1.  Crea una cuenta en [Github](https://github.com/).  
2. Entra en el repositorio [jekyll-now](https://github.com/barryclark/jekyll-now) y copia el repositorio a tu propio Github haciendo click en fork.  
![paso 1](https://jordigomper.github.io/myblog/img/jekyll-step1.PNG)  
  
3. Ves a tu nuevo repositorio, y cambia el nombre haciendo click en settings. Yo te recomiendo poner algo como mi-blog.  
![paso 2](https://jordigomper.github.io/myblog/img/jekyll-step2.PNG)  
  
4. Vamos a crear un Branch llamado gh-pages. A partir de ahora todas  las ***modificaciones las haremos desde ese branch***. En unos minutos nuestro blog se visualizara en https://nombre-de-tu-cuenta.github.io/nombre-de-tu-repositorio/.  
![paso 3](https://jordigomper.github.io/myblog/img/jekyll-step3.PNG)  
  
5. Desde el directorio principal de nuestro repositorio, editamos el archivo _config.yml:  
* Nombre del blog (name): Escribe aquí el nombre del sitio, o simplemente tu nombre.  
* Descripción (description): Una breve explicación sobre lo que vas a hablar en el blog.  
* Avatar (avatar): la url de tu avatar. Puedes simplemente copiar la url del avatar de github, de algún otro sitio donde lo tengas alojado, o alojarlo en este mismo repositorio.  
* Enlaces a tus redes (footer-links): aquí puedes configurar los iconos que aparecerán en la parte inferior de tu blog, y que enlazarán con información extra, como tu email, facebook, tu github, twitter, Google+ y un largo etcétera.  
  
![paso 4](https://jordigomper.github.io/myblog/img/jekyll-step4.PNG)  
  
![paso 5](https://jordigomper.github.io/myblog/img/jekyll-step5.PNG)  

Ya puedes comprobar nuevamente que tu blog funciona y que los cambios se ven reflejados.  
Con esto ya hemos instalado nuestro blog en Github listo para añadir contenido.    
  
  
## Añadir contenido a nuestro blog  

###  Creación de artículos  

En la carpeta _posts del directorio del repo, verás que hay un archivo .md. El nombre de los archivos son la fecha de publicación seguida de la url que queremos para el artículo.
Para empezar puedes editar el actual, y ponerle el nombre 2016-2-21-mi-primer-articulo.md.  
La portada del blog se actualizara y en el index pondrá una pequeña sección de nuestro nuevo articulo.  

Para crear nuevos artículos vamos a crear nuevos archivos en la carpeta _posts, acuérdate de que en el nombre siempre has de poner la fecha y a continuación el nombre del articulo.  
En la cabecera siempre hemos de incluir esta información:  

![paso 6](https://jordigomper.github.io/myblog/img/jekyll-step6.PNG)  
***layout*** : Indica el tipo de publicación. Podría cambiarlo por manual, articulo...  
***title:*** : Aqui va el titulo de nuestro articulo  
***excerpt_separator*** : Aquí vamos a indicar hasta donde muestra de este articulo la pagina principal. Pondremos &lt;!--more--&gt; hasta donde nos interese.  

Para darle un aspecto mas bonito utilizando Markdwon podemos consultar esta [guía de sintaxis](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)  
  
  
Aqui finaliza mi articulo. Espero que esta guía te ayude a explotar el potencial de Jekyll en Github, un saludo y hasta pronto!!  
