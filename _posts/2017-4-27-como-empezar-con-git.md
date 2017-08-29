---
layout: post
title: Controlador de versiones Git.
categories: herramientas
---
[Aprende Javascript con MentoringJS - Step 2](http://mentoringjs.com/)  
  
  
Git es un controlador de versiones. Fue diseñado por Linus Torvalds. Ofrece eficiencia y confiabilidad del mantenimiento de versiones a proyectos con un gran número de aplicaciones
  
Os enseñare como empezar a desarrollar vuestros proyectos desde servidores remotos. En este caso quiero compartir mi proyecto en una comunidad developer de forma pública, como es GitHub.  

  
### Como funciona git?
> La mayoría de las operaciones Git sólo necesitan archivos y recursos locales

**El flujo local de trabajo de se divide en tres secciones:<br>**
-**Git directory(Directorio de Git):** Almacena los metadatos y base de datos del proyecto. Es la parte mas importantes y es donde se copia el proyecto que clonas desde otro ordenador o servidor.<br>
-**Working directory(Directorio de trabajo):** Es la copia de una versión del proyecto. Residen en tu máquina local.<br>
-**Staging area(Área de preparación):**  Es un sencillo archivo, su función viene a ser la de un indice que almacena información de lo que va a guardar en la próxima confirmación.<br>

**El flujo de trabajo es el siguiente:**<br>
1.Modificas archivos en tu directorio local(Working directory).<br>
2.Preparas esos archivos, añadiéndolos al "indice"(Área de preparación).<br>
3.Confirmas los cambios. De forma que se almacena permanentemente en tu directorio de Git.<br>

### Primer paso<br>
Primero debemos de configurar Git con nuestra identidad (nombre de usuario y email). Esto indicara a los diferentes desarrolladores y a nosotros mismos de quien ha efectuado cambios en diferentes partes del proyecto.<br>

### Comandos básicos para funcionar git

- **Crear o clonar repositorios:**<br>
**git help <comando>**: Este comando es el que mas nos va a ayudar.Nos muestra el manpage de todos los comandos. Si este comando no es suficiente puedes buscar ayuda de una persona en los canales **#git** o **#github**.<br>
**git init**: Inicia un repositorio local.<br>
**git clone**: Hace una copia de un repositorio Git existente. También podemos clonar repositorios desde un servidor remoto.<br>

- **Guardar repositorios:**<br>
**git status**: Nos indicara en que estado están nuestros archivos.<br>
**git add nomde_del_archivo**:Hace una confirmación inicial del archivo indicado.<br>
**git commit**: Confirmara los cambios de los archivos y los guardara en el repositorio.<br>
**git rm**: Elimina archivos<br>

- **Comandos relacionados con Branch:**<br>
**git checkout -b nombre_brranch**: Crea una rama y saltas a ella.<br>
**git checkout nombre_repo**: Saltas a branch o trunk.<br>

### GitHub IMPORTANTE
Si al conectarte a tu repositorio Git de GitHub te da error de la key, debes de seguir los pasos indicados en su sección de ayuda para introducirla a mano.

Esta guía se basa en mi experiencia inicial, toda la ayuda y información la he encontrado en google y en el curso de la pagina oficial de Git.

Gracias y espero que sirva de ayuda.
