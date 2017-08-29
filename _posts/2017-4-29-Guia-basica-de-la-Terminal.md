---
layout: post
title: Aprende a utilizar la terminal.
img: blog/i_terminal.jpg
categories: articulo
---
[Aprende Javascript con MentoringJS - Step 4](http://mentoringjs.com/)  
  
  
En este curso vamos a navegar por nuestra Shell. Quizás te preguntes por que utilizar nuestra primitiva terminal si tenemos una GUI maravillosa, pues porque para algunas tareas no es útil. Vamos a adquirir los conocimientos básicos para poder navegar, crear, modificar... vamos a empezar, BANZAI!!!

> ¿Qué es La Shell?  
Es un programa que envía los comandos que has introducido por teclado al sistema. Durante muchos años era la única interfaz de usuario.  
>  
>¿Qué es una Terminal?  
Este es un programa que abre una ventana y le permite interactuar con el shell.

## La Terminal

> Si encontramos que el ultimo carácter del indicador de la shell es un # en vez de $, nos indica que estamos como superusuario. No es recomendable operar como superusuario ya que podríamos eliminar o sobrescribir cualquier archivo del sistema. A menos que necesite privilegios administrativos, no opere como superusuario.  
>  
>Para cambiar de usuario simplemente utilice el comando ***su "nombre-usuario*** y introduzca la contraseña.   
>  
>Podemos seguir utilizando el ratón. En estos casos el ratón puede sernos muy útil para poder copiar texto o desplazarnos por la ventana del Terminal.

### Comandos

> Si en algún momento no entendemos la estructura de un comando, no recordamos los atributos o queremos con detalle su funcionamiento, tenemos varias formas de acceder a esa información.  
>  
>* Si queremos información detallada del programa escribimos en la terminal ***man "nombre-del-comando"*** y accederemos al manual.  
>
>* Si lo que queremos es simplemente información de la estructura del comando y sus atributos, vale con poner ***"nombre-del-comando" --help***.

#### Navegación

> Los archivos en Linux se organizan en una estructura de directorios jerárquicos.

| Comando| Descirpcion | Funcion|
| ------------- |-------------| -----|
| pwd       | directorio de trabajo de impresión | indica el directorio de trabajo donde nos encontramos ahora mismo. |
| cd      | directorio de cambios      |   **cd "directorio"** iremos al directorio indicado <br> **cd ..** saltamos al directorio anterior <br>**cd /** vamos al directorio raiz|
| ls | lista de archivos y directorios      |    * nos indica todos los archivos y carpetas que hay en el directorio <br> **ls -l** nos indica archivos y carpetas del directorio y sus propiedades <br> [descripción](../images/propiedades_archivos.PNG) de las propiedades de los archivos|


#### Directorios principales  
  
Esta imagen nos indica las diferentes carpetas del directorio raiz y que contienen.
![direcorios](https://i2.wp.com/nexolinux.com/wp-content/uploads/2013/04/fhs1-e1365160570150.png)

#### Manipulación de archivos

| Comando| Descripción | Función|
| ------------- |-------------| -----|
|     cp  | cp archivo1 archivo2 <br> cp directorio1/archivo1 directorio2/archivo2 | Copia archivo1 como archivo 2. Podemos indicarle el directorio de archivo1 o donde copiar archivo2 |
|     mv   | mv archivo1 directorio <br> cp directorio1/archivo1 directorio2/archivo2 | Este comando mueve el archivo1 al directorio indicado |
| rm | rm file1 <br> rm dir/arch <br> rm dir1/dir2 | El comando rm elimina archivos y directorios |
| mkdir | mkdir dir1/dir2 | Crea directorios |

#### Permisos de archivo

Los archivos tienen ***derechos de acceso para el propietario del archivo, grupos y demás***. Se pueden asignar ***derechos para leer, escribir y ejecutar***.
Si ejecutamos el comando ***ls -l*** en la terminal nos sale todos los archivos y sus permisos dentro del directorio actual.

![ls -l](https://upload.wikimedia.org/wikipedia/commons/c/cc/Ls_command_result.png)

Hay que tener claro la siguiente imagen para entender esta sección:

![permisos archivos](http://linuxcommand.org/images/file_permissions.png)

El comando ***chmod*** se utiliza para cambiar los permisos de un archivo o directorio. Para usarlo, ejecute desde superusuario y especifique la configuración de permisos deseada y el archivo o archivos que desea modificar. Hay dos formas de especificar los permisos. En esta lección nos enfocaremos en uno de estos, llamado el método de la notación octal .

Es fácil pensar en la configuración de permisos como una serie de bits (que es cómo la computadora piensa acerca de ellos). Así es como funciona:

  Rwx rwx rwx = 111 111 111 
  Rw - rw - rw - = 110 110 110 
  Rwx --- --- = 111 000 000 

  y así... 

  Rwx = 111 en binario = 7 
  Rw = 110 en binario = 6 
  Rx = 101 en binario = 5 
  R = 100 en binario = 4 

Con estos conocimientos vas a poder usar la terminal en un nivel intermedio. Espero que te haya sido de ayuda, sin mas, hasta luegorrrrrrrr!!!!
