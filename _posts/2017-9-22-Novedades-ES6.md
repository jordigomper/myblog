---
layout: post
title: Novedades ES6
img: blog/i_es6.jpg
categories: articulo
---

Hola chicos! En este articulo quiero repasar las mejoras más importantes que trae **ES6**.  

Cada versión que nos ofrece ESCM encontramos facilidad ya sea en el código, en nuevas funciones, nuevas variables... Esta vez, **ES6** viene cargado de novedades que nos va a ayudar nuestro día a día.  

>ES6 son los reyes magos...  

Como la comunidad de JS se ha portado muy bien los reyes magos vienen cargados de regalos, vamos a ver lo que nos traen. Las novedades más importantes para nuestro día a día que incluyen recursos donde antes no teníamos otras opciones, por ejemplo las variables de ámbito de bloque.  

Las nuevas variables **let/const** son las nuevas variables de ámbito de bloque. Antes de **ES6** solo contábamos con la variable var, estas variables sufren el efecto hositing esto quiere decir que antes de interpretar el código dentro del programa o cuando entra en una función, JS recopila las variables y las define sin valor en la parte superior del código que se esta interpretando.  
Otro problema es que no tiene ámbito de bloque, es decir, una variable de una función puede acceder a las variables de nivel superior sin necesidad de declararla:

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

Ahora vamos con la variable **const**. Es de tipo bloque y es de sólo lectura. No puede reasignarse el valor de una constante ya asignada, solo en el caso que ese valor sea un objeto o array:

```
//ES6
const MY_FAV = 7;

 // reasignación
MY_FAV = 20; // error

 // redeclarar
var MY_FAV = 20; // error
```

Con esta novedad enterramos muchas de las desventajas que nos encontrábamos al comenzar a programar con JS. Sin duda estas nuevas variables dan un nuevo potencial a JS y ara que podamos diseñar un código más completo y seguro.  

En muchas ocasiones tenemos la necesidad de extraer o asignar diversas variables que se encuentran en el interior de un objeto. La nueva asignación por **desestructuración** consigue abrir un objeto y extraer información o asignarle nuevos valores de una sola pieza, así de sencillo:

```
// ES6
 // asignar variables a objetos
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

Como puedes ver la desestructuración de **ES6** ahorra mucho código y utiliza una forma muy sencilla para manipular las variables en el interior de objetos y arrays. Otro ejemplo más del potencial de **ES6**.  

>Cada vez estas más convencido que ES6 son lo reyes? No me guardes rencor por eso...  

Todos los códigos deben de tener mínimo... un bucle? **ES6** trae una ventaja a la hora de poder acceder a las keys de un objeto dentro del mismo bucle:

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

Ahora vamos a ver los objetos creados a partir de **new Map** que perfectamente puede complementarse con el control de objetos en bucles que ya hemos visto.  

Map es un objeto que contiene las parejas key/value. Se puede crear desde cero y añadir el contenido con la propiedad **.set** o obtener los valores key/value con **.get** y también se puede crear una replica de un objeto o array ya existente.  

La principal característica es que puedes asignar cualquier valor (valores primitivos, funciones) como key o value transformándolos en string. Permite la comparación de los 2 valores, pudiendo saber por ejemplo si una clave contiene una función.

Normalmente se utiliza cuando las keys son desconocidas hasta el momento de la traducción, es decir, que no sabes cuantas propiedades va a tener el objeto. Seguramente esas propiedades son asignadas durante la ejecución del código.

```
// ES6
var this.objectMap = this.objectMap ||  new Map

for (let [name, age, posts] of this.objectMap) {
    // obtener valores
    this.objectMap.get(name) // 'Linux'
    this.objectMap.get(age) // '26'
    this.objectMap.get(posts) // [ "post1", "post2" ]

    // asignar los valores
    this.objectMap.set(name, "Windows");
    this.objectMap.set(age, "32");
    this.objectMap.set(posts, "[ "post1", "post2" ]");
}
```

En la versión ES5 tenemos que crear un objecto para poder hacer esta operación, ya que no incorpora el objeto Map. Tampoco podemos iterar sobre las propiedades dentro de un bucle, así que en este aspecto ES6 hace de una operación común en nuestros códigos algo más sencillo y legible de hacer.  

También encontramos nuevos metodos para nuestras arrays. Por ejemplo, **Array.prototype.findIndex** nos sirve para encontrar el primer elemento que coincida con las variables que le indicamos desde la función:

```
// ES6
const i = ripples.findIndex(function(r) { return r.started && !r.ending; });
```

Con esta función obtenemos el indice donde empieza una onda y donde acaba dentro de un array.  

También tenemos **Array.prototype.fill** que rellena todos los elementos de una matriz desde el indice inicial indicado hasta el indice final indicado con un valor estático:

```
// ES6
var numbers = [1, 2, 3]
numbers.fill(1);
```

El resultado es un array con tres elementos con valor de 1 cada uno de ellos.  

Otra de los nuevos métodos es **Array.prototype.copyWithin** que copia la parte indicada de esa misma matriz y la pega en otra ubicación en su interior sin modificar el tamaño de la misma. Puedes encontrar más info [aquí](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/copyWithin).  

Es casi imposible aprenderse todos los métodos, así que con saber que existe esa función ya vale, después google te ayudara a recordad como funciona...  

Disponemos de las **fat arrows**, que nos facilita código a la hora de crear una función. La característica principal de estas funciones es que siempre hacen referencia al objeto que la invoca.  

En su sintaxis podemos encontrar diferentes variaciones. Si no pasamos ningún parámetro por referencia o solo uno podemos excluir los paréntesis, no necesita usar llaves para el contenido si solo usa una sola expresión y no hace falta una declaración de devolución y para usar la des estructuración sobre un objeto hay que pasar el parámetro entre corchetes.  

```
// ES6
 // fat arrow simple
 // al no indicar return siempre devuelve el resultado
 // devuelve la palabra bar
const arrow1 = () => 'bar'

 // fat arrow simple
 // devuelve x + 1
const arrow2 = (x) => {
  return x + 1
}
 
 // llama una función por cada elemento 
this.items.map(x => this.doSomethingWith(x))
```

Esta función la vamos a ver en todos los códigos ya que aporta un gran potencial a la hora de crear funciones comunes para objetos. Dominarla es esencial si escribes tu código bajo **ES6**.  

Contamos con **Template Literals**, que nos permite concatenar diversas lineas y variables. Siempre van envueltas con **tildes invertidas** y las variables en el interior de **${ }**, pudiendo hacer cualquier operación con ellas:

```
var a = 5;
var b = 10;
console.log(`Quince es ${a + b} y\nno ${2 * a + b}.`);
// "Quince es 15 y
// no 20."
```

Con **Promise** podemos sincronizar código, reteniendo la ejecución de esa parte del código a la espera de recibir una respuesta. Normalmente se utilizan para las peticiones a un servido, ya que puede que la respuesta tarde en procesarse.  

Utiliza los métodos **onSucces** y **onFailure** donde indicaremos que debe hacer en cada uno de los casos.  

Puedes encontrar más información en [aqui](http://jamesknelson.com/grokking-es6-promises-the-four-functions-you-need-to-avoid-callback-hell/).

Con la **extensión array** podemos mostrar el interior de un array o re asignar sus parámetros solo introduciendo tres puntos al principio(...array). Podemos mostrarla por pantalla sin la necesidad de ningún bucle, también añadir nuevos elementos sin la necesidad de utilizar **.push**:

```
var parts = ['shoulders', 'knees']; 
var lyrics = ['head', ...parts, 'and', 'toes']; 
// ["head", "shoulders", "knees", "and", "toes"]
```

Como puedes comprobar, a la segunda variable hemos añadido diferentes elementos, incluido una propagación de la primera, por eso incluye todas las variables.  

Una de las ventajas más significantes de **ES6** es su nueva **gestión de archivos imoprt & export**. Mejora su sintaxis facilitando la importación y exportación de bibliotecas, clases, partes del código... También podemos agregar accesos a directorios en nuestra app.

Hasta aquí esta guía de **ES6**.  

**A tope con @mentoringJS!  
Jordi Gomper.**