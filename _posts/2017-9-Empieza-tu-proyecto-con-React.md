---
layout: post
title: Empieza tu proyecto con React
img: blog/i_comp.jpg
categories: articulo
---

Hola chic@s! En este articulo voy a repasar las las principales funciones de React y como estructurar tu proyecto desde un principio.  

[Aprende Javascript con MentoringJS - Step 12](http://mentoringjs.com/)

Es importante no avanzar demasiado rápido cuando empezamos con React. Una base solida de buenos hábitos nos ahorra mucho tiempo en un futuro y optimiza nuestra forma de programar. Saber utilizar de forma correcta los componentes, dividiendo el trabajo de ellos en función de si es un componente de estilo o contenedor, incorporándoles un ciclo de vida, pasandoles funciones por referencia...  

También tenemos saber estructurar nuestro proyecto desde un principio, facilitar los diferentes directorios a la hora de que va a contener cada uno ahorrara tiempo a la hora de ir a buscar ese componente, imagen, o archivo.  

Ahora... al turrón!

## Componentes React
Cuando empezamos con un proyecto, antes de abrir nuestro editor de texto es importante dibujar sobre papel todas las diferentes partes que contiene.  

Por ejemplo, empezaremos desde la página principal, dibujando las diferentes partes que las componen y luego, hacemos los mismos con esas pequeñas partes, cada vez dibujaremos partes mas y mas pequeñas hasta que ya no se pueda descomponer más, por ejemplo, si estamos descomponiendo un muro que va a contener nuestra página principal, acabariamos con el botón enviar o algo por el estilo.  

Cada parte que hemos dibujado hasta el nivel más bajo, va a ser un componente React y normalmente, puede que se convierta en un componente contenedor que processara información enviada dependiendo en que lugar se encuentre. Si subimos para arriba, encontraremos componentes de estilo. Estos componentes se encargan de agrupar otros componentes dando forma a una interfaz de usuario y en ocasiones, enviando información a los componentes contenedores.  

Aqui tienes un ejemplo: 
![twitter](https://jordigomper.github.io/myblog/img/a_manual_desc/twitter2.PNG "twitter")  

Al componente que contiene toda la información como es la imagen, el titulo y el texto le vamos a llamar **SimpleCard** y es un componente de estilo. Se encarga de agrupar componentes más pequeños y darle forma. En este caso también pasa información, por ejemplo, donde se encuentra la foto al componente imagen.  

Los componentes **user**, **description** y **image** son componentes contenedores que procesan información mostrando diferente contenido dependiendo en que lugar se encuentren.  

En esta fase es importante dibujar los componentes lo mas pequeños posibles para poder reutilizarlos en las diferentes partes de nuestro proyecto.  

### props/state
Estos son dos componentes de la API de React. Se utilizan para que los diferentes componentes hijos y padres se puedan comunicar.  

**props** es la información que pasa un componente padre a la hora de instanciar otro componente y una vez instanciado, no se puede modificar. Puede contener información de estilo, contenido, controladores de eventos, funciones por referencia...

**state** se utiliza para almacenar información que en algun momento puede ser modificada y automaticamente, al cambiar, manda a renderizar el componente con la nueva información introducida. Podemos modificar state utilizando setState. 

Tomando el ejemplo anterior, SimpleCard enviara la información que contiene en su state a image desde props, renderizando el componente de nuevo si esta se ve modificada:
```
this.state = {
    imageURL: "./img1"
}
<div className='simple-card'>
  <Image url={this.state.imageUrl}/>
</div>
```

### Interficies de usuario
Una hemos indentificado todos los componentes, les hemos clasificado por contenedores y estilo ya podemos empezar a plasmarlo en código.  

El anterior componente Simplecard debera tener una estructura parecida a esta:
```
<div className='simple-card'>
  <Image url={this.props.item.imageUrl}/>
  <User text={this.props.item.user}/>
  <Description text={this.props.item.description}/>
</div>
```

Dentro de estos componentes también podemos encontrar que anidan otros componentes, por ejemplo, el componente Description puede contener un componente Date que muestra el dia que se publicó el mensaje. Siguiendo los mismos pasos no tiene más dificultad.  

### Listas/Arrays
Vamos a crear una lista con los elementos que contiene un Array, por ejemplo, para mostrar los diferentes usuarios registrados, o un resumen sobre todos los artículos de una sección.  

Para esto vamos a utilizar los métodos de JavaScript nativo. Con el método **.map** extraemos uno por uno cada elemento, y en cada operación ejecuta el código que indicamos:
```
function render() {
  return (
    <ul>
      {this.props.items.map(function(item) {
        return <li key={item.id}>{item.name}</li>
      })}
    </ul>
  );
}
```

Puedes ver que dentro del elemento ul, agregamos el método **.map** sobre la información que le pasamos desde props, creando un elemento li con el contenido de item.name.  

Cuando creamos una lista, React necesita que cada uno tenga una key única. Identificando cada uno con una key, React puede modificar ese elemento desde el DOM sin necesidad de volver a renderizar toda la lista, solo renderizara ese elemento buscandolo desde key, optimizando el rendimiento. Si no la indicamos, React envia un error desde la consola, aunque el código se ejecutara sin problemas.  

### Ciclo de vida
Es importante implementar un ciclo de vida a nuestros componentes. Vamos a ver algunos de los métodos que tenemos disponibles.  

El mas básico es el método contructor. Con el vamos a definir las diferentes variables de **state** que pueden venir desde props, funciones para el componente etc etc:
```
constructor(props) {
    // añadimos a state los valores pasados por props
    super(props);
    this.state = {showText: true};

    // funcion que ejecuta un código determinado por un tiempo
    setInterval(() => {
      this.setState => {
        return { //... };
      });
    }, 1000);
  }
```

Utilizando el método **componentWillMount()**, vamos introducir todo lo que queremos que se renderize cuando el componente es instanciado por primera vez. Por ejemplo, si añadimos un método sin asignarlo a componentWillMount, cada vez que este componente se renderize va a renderizar este método sin necesidad alguna. Realmente solo queremos que se instancie la primera vez, no necesitamos volver a instanciarlo cuando volvemos a renderizar componente cuando por ejemplo se modifica su state:
```
// define la edad desde props cuando es instanciado por primera vez
componentWillMount() {
    let mode;
    if (this.props.age > 70) {
      mode = 'old';
    } else if (this.props.age < 18) {
      mode = 'young';
    } else {
      mode = 'middle';
    }
    this.setState({ mode });
  }
```

Con todo lo mencionado y apoyandote en el manual de [React express](http://www.react.express) ya tienes el conocimiento básico sobre componentes.  

## Estructurando un proyecto
Es importante marcar una estructura a nuestro proyecto desde un principio. Piensa que poco a poco el proyecto va a ir creciendo, marcar desde el principio una estructura nos va a ayudar en un futuro y va a evitar que se desborde. En esta sección vamos a ver la estructura básica que puede tener un proyecto.  

Vamos a modificar la estructura que crea la herramienta create-react-app y aunque esto puede ir en función del gusto de cada uno, básicamente esta es la estructura básica que debemos seguir:
> * src
> +   api.js
> +   components
>     - Button.js
>     - Icon.js
>     - UserDetail.js
>     - UserList.js
> +   containers
>     - App.css
>     - App.js
>     - App.test.js
>     - HomePage.js
>     - UserDetailPage.js
>     - UserListPage.js
> +   images
>     - logo.svg
> +   index.js
> +   utils
>     + testUtils.js

* Pasito a pasito... Dentro de src vamos a introducir la API relacionadas con backend.
* Dentro de **components** van a ir todos los componentes de presentación.
* En **containers** los componentes contenedores.
* Dentro de la carpeta **img** todas las imagenes. Aquí podemos crear subdirectorios para ordenarlo mejor.
* **index.js** es el archivo donde iniciamos la aplicación llamando a ReactDom.render. Este archivo es mejor tenerlo en el directorio raiz.
* Dentro de **utils** vamos a incorporar las diversas funciones como manejadores de error, formateadores y similares. Cuando los necesitemos vamos a saber donde se encuentran.  

Cuando necesitemos importar cualquier archivo vamos a saber donde se encuentra y utilizando los diferentes métodos de los que hemos hablado en el (articulo anterior)[https://jordigomper.github.io/myblog/articulo/2017/09/22/Novedades-ES6.html], podemos crear directorios personalizados.  

Aqui acaba el articulo. Recuerda que es muy importante seguir la metodologia de la que he hablado en este articulo, esto te ayudara a optimizar el rendimiento del código y te facilitara el trabajo.  

Sin más, me despido. Un saludo!!  

**A tope con @mentoringJS!  
Jordi Gomper.**