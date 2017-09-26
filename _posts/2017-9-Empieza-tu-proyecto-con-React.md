---
layout: post
title: Empieza tu proyecto con React
img: blog/i_comp.jpg
categories: articulo
---

React es el framework de moda, tiene una gran comunidad y el respaldo de grandes empresas como facebook o instagram. Su capacidad para crear interficies de usuario en diversas plataformas es impresionante.  

Aprender React si vienes de JS no es difícil y esto puede llevar a una mala practica, vale la pena dedicarle unas cuantas horas más y aprender a utilizarlo bien desde un principio.  

Hoy voy a explicar la base para empezar un proyecto de una forma adecuada. Empezando por las novedades que trae ES6, que ayuda a simplificar el código luego saltaremos a React, haciendo hincapié en como estructurarlo desde un inicio, como crear un interficie de usuario y como diferenciar los diversos componentes. 

Ahora... al turrón!

# Index

## ES6 son los reyes magos...
ES6 nos trae una optimización de su sintaxis y nuevos módulos integrados. Voy a repasar las novedades que nos va a facilitar nuestro día a día.  

### Desestructuración
Con este método se consigue abrir un objeto o array y extraer información o asignarle nuevos valores de una sola pieza, así de sencillo:

```
// ES6
 // asignar variables a objetos o arrays
var user = {name:'Linux', age'26', pic:'penguin.jpg', posts: []};

 // extraer a variables locales
var {name, pic, posts} = user;

 // también podemos asignar valores para iniciar una función
function viewUser ({name = {}, pic = {}, posts = []}) {
    //...
};

```

Este ejemplo se basa en un usuario permitiendo extraer los datos que nos interesa para modificarlos o llevarlos a una función.  

Puedes comprobar la ventaja comprobando el siguiente código escrito en ES5:

```
// ES5
 // asignar variables a objetos o arrays
var user.name = 'Linux';
var user.age = 26;
var user.pic = pinguin.jpg;
var user.posts = [];

 // extraer a variables locales
var name = user.name;
var age = user.age;
var pic = user.pic;
var posts = user.posts;

 // asignar valores para iniciar una función
function viewUser (user){
    name = user.name; 
    pic = user.pic; 
    age = user.age; 
    posts = user.posts; 
};
```

Como puedes ver la desestructuración de ES6 ahorra mucho código y utiliza una forma muy sencilla para manipular las variables en el interior de objetos y arrays.  

### Loops
Todos los códigos deben de tener mínimo... un bucle? ES6 trae una ventaja a la hora de poder acceder a las keys de un objeto dentro del mismo bucle:

```
// ES6
 // desde el bucle podemos ir directamente a las keys
for (let [name, pic] of Object.entries(post)) {
    // ....
};
```

Una ventaja a la hora que queramos por ejemplo, reproducir una lista con los nombres y imágenes de los usuarios.  

La ventaja que nos aporta es importante respecto a ES5, que, primero tenemos que asignar el objeto o array que se esta ejecutando en este momento en una variable dentro del bucle para luego extraer los valores:

```
// ES5
 // user_list contiene los valores del objeto que
 // posteriormente utilizamos para conseguir los
 // datos
var users = Object.users(models);
for (var i = 0; i != users.length; i++){
    users_list = users[i] 
    name = entry[0];
    age = entry[1];
    pic = entry[2];
    posts = entry[3];
}
```

Otro ejemplo más del potencial de ES6. Cada vez estas más convencido que ES6 son lo reyes? No me guardes rencor por eso...  

### Map
Map es un objeto que contiene las parejas key/value. Se puede crear desde cero y añadir el contenido con la propiedad **.set** o obtener los valores key/value con **.get** y también se puede crear una replica de un objeto o array ya existente.  

La principal característica es que puedes asignar cualquier valor (valores primitivos, funciones) como key o value transformándolos en string. Permite la comparación de los 2 valores, pudiendo saber por ejemplo si una clave contiene una función.

Normalmente se utiliza cuando las keys son desconocidas hasta el momento de la traducción, es decir, que no sabes cuantas propiedades va a tener el objeto. Seguramente esas propiedades son asignadas durante la ejecución del código.

```
// ES6
var objectMap = new Map();

var name = {},
    age = function viewUser () {},
    posts = [];

 // asignar los valores
objectMap.set(name, "Linux");
objectMap.set(age, "26");
objectMap.set(posts, "[ "post1", "post2" ]");

 // obtener valores
objectMap.get(name) // 'Linux'
objectMap.get(age) // '26'
objectMap.get(posts) // [ "post1", "post2" ]
```

Con ES5 esto no era posible, OOOOOOOOOOOOOOO

### Variables let/const
Antes del ES6 todas las variables declaradas eran de tipo **var**. Estas variales se ven afectadas por el hoisting, esto quiere decir, que antes de interpretar el código dentro del programa o cuando entra en una función, JavaScript recopila todas las variables y las define sin valor al principio del código.  

Otro problema es que no tiene ámbito de bloque, es decir, una variable dentro de una función podía acceder a las variables de nivel superior y modificarla:

```
// ES5
 // efecto hoisting
var a = 5;
(function(){
    console.log(a); // undefined
    var a = 7;
    console.log(a); // 7
})();

 // sin ámbito de bloque
var a=5;

if(true) {
    var a = 7;
}

console.log(a); // 7
```

Como puedes comprobar dentro de la función nos imprime por primera vez undefined, esto es debido que al entrar a la función a elevado a con un estado indefinido. Segundo error, se puede modificar una variable de un nivel superior sin desearlo.  

La nueva variable **let** trae nuevas ventajas, es de ámbito de bloque y no se ve afectada por el hoisting:

```
// ES6
 // ámbito de bloque
let a=5;
if(true) {
    let a = 7;
    console.log(a); // 7
}
 // en este caso no se ve afectada
console.log(a); // 5

 // efecto hoisting
let a = 5;

(function(){
    console.log(a); // error

    let a = 7;

    console.log(a); // 7
})();
```

s