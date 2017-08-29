---
layout: post
title: React analizando el código y estructura.
categories: react
img: blog/i_react.jpeg
categories: react.js
---

[Aprende Javascript con MentoringJS - Step 10](http://mentoringjs.com/)  

Creando una pequeña aplicación desde cero, vamos a analizar los conceptos básicos de React utilizando los ejemplos que incluye la guía [oficial de React](http://www.react.express/).

![Demostacion apli con React](https://jordigomper.github.io/myblog/img/a_apli_react/aplicacion_react.gif)  

Tienes todos los ejemplos de la guía en [mi repositorio personal de GitHUb](https://github.com/jordigomper/react-express)

## Index.
1. [React](#react)  
 1.[Que es React?](#que-es-react)  
 2.[React llega a tu ordenador](#react-llega-a-tu-ordenador)  
     3.[Requisitos](#requisitos)  
 4.[Instalación](#instalación)  
2. [Introducción a nuestra aplicación](#introducción-a-nuestra-aplicación)  
3. [Capitulo 1. Creando la interfaz](#capitulo-1-creando-la-interfaz)  
 1.[Importar y exportar módulos](#importar-y-exportar-módulos)  
 2.[JSX](#jsx)  
 3.[Componentes simples](#componentes-simples)  
 4.[Método render](#método-render)  
4. [Capitulo 2. Imprimiendo las filas por pantalla](#capitulo-2-imprimiendo-las-filas-por-pantalla)  
 1.[Componentes personalizados](#componentes-personalizados)  
 2.[Componentes de API props y state](#componentes-de-api-props-y-state)  
 3.[Identificador Key en las listas](#identificador-key-en-las-listas)  
5. [Capitulo 3. Dando color a las filas](#capitulo-3-dando-color-a-las-filas)  
 1.[In-line style](#in-line-style)  
6. [Capitulo 4. Borrar las filas](#capitulo-4-borrar-las-filas)  
 1.[Eventos](#eventos)  
7. [Capitulo 5. Modular nuestra aplicación](#capitulo-5-modular-nuestra-aplicación)  
8. [Conclusión](#conclusión)  


## React
### Que es React?

Se trata de una biblioteca de JavaScript de código abierto que proviene de Facebook y creada por Jordan Walke. Facilita la construcción de aplicaciones de una sola página y que contienen multitud de elementos dinámicos en la pantalla y con los que el usuario puede interactuar.

### React llega a tu ordenador

Vamos a traer React a nuestro ordenador. Tenemos que instalar una serie de paquetes, que ejecutan React en modo local. Create-react-app es la herramienta que nos proporciona Facebook gracias a Dan Abramov, creador de Redux. Esta herramienta hace posible ejecutar React en local.

### Requisitos

* **[Node.js](https://nodejs.org/en/)** como mínimo en su versión 4.0, recomiendo siempre la ultima versión LTS.  
* **NPM** en versión 3.0 en adelante. Es un gestor de paquetes React. Con npm podemos instalar infinidad de complementos desde la consola CMD. 
* **Google Chrome**.  
* **[React Developer tools](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi)**, está herramienta de google Chrome sirve para debuggear nuestro código react, nos da información del árbol de nodo entre más cosas...  
* Editor de texto tipo Visual Studio Code, Sublime Text 3...

Es importante a la hora de empezar con el manual, crear un directorio local donde guardar los archivos de los ejemplos. Cada uno individualmente y ordenados.

### Instalación

Desde la cmd de windows:  
**npm install -g create-react-app**. Este comando instala create-react-app.  
**create-react-app nombreDeLaAplicacion**. Instala un directorio en la raíz con el nombre que has introducido. Esta operación puede tardar unos minutos.  
**cd nombreDeLaAplicacion**. Entramos en el directorio de la aplicación.
**rm src /App.* src/index.css src/logo.svg**. Borramos estos archivos del interior de la carpeta src que es de donde se ejecuta la aplicación. Estos archivos contienen una presentación de React que no necesitamos.  
**npm start**. Arrancamos la app. Automáticamente se abre el explorador, vamos a trabajar con esa página (http://localhost:3000/) que es el interior de src.  

Con esto ya tenemos instalado y en marcha nuestro workspace para trabar con React.

[React Expres - Quick start](http://www.react.express/quick_start)

## Introducción a nuestra aplicación

Como he dicho al principio, vamos a crear una aplicación basándonos en los ejemplos de la [oficial de React](http://www.react.express/).  

Nuestra aplicación va a consistir en una pequeña interfaz de usuario, donde tenemos varios botones que al pulsarlos van a aparecer filas de diferente color y si pulsamos sobre la fila se borrara.

Esta aplicación utilizara la DOM virtual que nos proporciona React para añadir/borrar de la DOM las diferentes filas de colores. 

Vamos a ver los los componentes de la API props y state, para que sirven y como utilizarlos.

Sin más, empezamos...

## Capitulo 1. Creando la interfaz.
Vamos a crear el estilo de interfaz que queremos, sin ninguna función. Va a ser algo simple y va a servir para ver como crear un elemento simple y como incorporarlo en la DOM.

En cada capítulo y antes de comentar el código, explicare las diferentes funciones que vamos a necesitar en ese momento, después las utilizaremos en nuestra aplicación para ver como funcionan.

### Importar y exportar módulos
Desde la llagada de ES6, JavaScript dispone de un mecanismo para importar o exportar módulos. Los módulos son fragmento de código que se carga una vez se ejecuta, con la función **import** y puede tratarse de funciones de React, objetos, variables... todas desde otro archivo. También podemos permitir la exportación de determinados archivos con la función export.

Nosotros de momento vamos a utilizarlo para importar a nuestra aplicación diferentes herramientas que nos proporciona React.

El primero módulo que cargamos no hace falta indicar el nombre cuando hacemos referencia en el en la aplicación, los demás, si.

e.j.
```
import React, { Component } from 'react'
import ReactDOM from 'react-dom'
```

Este código nos permite utilizar la herramienta **Component**, esto nos permite crear componentes en React. El otro módulo rednder, es la herramienta que utiliza React para introducir un elemento en la DOM.

[React Expres - Import and Exports](http://www.react.express/imports_and_exports)

### JSX
JSX es una extensión de JavaScript que hace más simple la forma de utilizar la API React.createElement, esta ultima nos permite crear elementos con propiedades para después incorporarlos en la DOM. JSX simplifica este método y la estructura que utiliza es mas intuitiva pudiendo anidar los elementos de una forma muy similar que en nuestro HTML nativo.

No es nativo de JSX ni tampoco es obligatorio, pero es aconsejable utilizarlo por todas las ventajas que aporta.

e.j.
```
const App = (
    <div>
        <button>blue</button>
        <button>yellow</button>
        <button>orange</button>
        <button>purple</button>
        <div>
            // aqui se mostraran las filas de colores
        </div>
    </div>
)
```
Todo lo que se encuentra dentro de los paréntesis es esta escrito en JSX.

Dentro del código JSX podemos introducir código JavaScript por diferentes razones, por ejemplo, llevar el valor de una variable. Esto lo podemos conseguir introduciendo el nombre de las variables entre corchetes{}. Al ejecutar ese código, lo interpreta como JavaScript.  

[React Expres - JSX](http://www.react.express/jsx)

### Componentes simples
React trae incorporado una serie de nodos DOM con el mismo nombre que los que hacemos servir en HTML e.j. div, span, tablas, listas… a estos les llamamos componentes simples. Podemos añadirle atributos y funciones.

Vamos a utilizar estos componentes para dar forma a nuestra interfaz. Podremos crear los &lt;button&gt;, &lt;div&gt;... que después React incorporara en la DOM y se mostraran en la aplicación.

e.j.
```
const App = (
    <div>
        <button>blue</button>
        <button>yellow</button>
        <button>orange</button>
        <button>purple</button>
        <div>
            // aqui se mostraran las filas de colores
        </div>
    </div>
)
```
Dentro de nuestro del Step 1 de la aplicación encontramos un componente llamado App, es un componente simple escrito con JSX. Los componentes simples están formados por elementos que se nombran igual que en JavaScript.  

[React Expres - DOM Comopnents ](http://www.react.express/components)

### Método render()
Este método nativo de React. Este método nos permite introducir un elemento dentro de la DOM.

La forma de utilizarlo es **render(elemento, nodo)**. render() nos permite varias formas, no es súper estricto. La forma más simple es introducir un elemento ya creado anteriormente dentro de un nodo que ya hemos asignado a una variable, pero también nos deja crear el elemento dentro, y buscar el nodo por ejemplo con un getElementById("...") o cosas parecidas.

```
render(
    App,
    document.getElementById('root')
)
```
Seleccionamos el elemento simple App y indicamos que queremos buscar un nodo llamado root y incorporarlo dentro de el.

Primero necesitamos importar desde react-dom la función render. Asignamos el elemento y el nodo a variables y utilizamos render. También podemos crear el elemento simple dentro o buscar el nodo.

[React Expres - React API ](http://www.react.express/react_api)


### [APLICACIÓN] Step 1
Nuestra interfaz consiste en 4 botones los cuales imprimen una fila al ser pulsados, cada uno de un color y división donde se imprimen las filas.
```
import React, { Component } from 'react'
import ReactDOM from 'react-dom'

const App = (
    <div>
        <button>blue</button>
        <button>yellow</button>
        <button>orange</button>
        <button>purple</button>
        <div>
            // aqui se mostraran las filas de colores
        </div>
    </div>
)


render(
    App,
    document.getElementById('root')
)
```

Primero importamos Component y render desde react y react-dom.

App es un componente simple, como he escrito antes, los componentes simples utilizan etiquetas similares que en HTML. Creamos una &lt;div&gt; donde introducimos los &lt;button&gt; de diferentes colores y el contenedor de las filas.

Con render introducimos nuestro elemento App en la DOM, buscando un elemento con 'root'.

De momento esto no hace ninguna función, es solo para que te hagas a la idea de como empezar a montar nuestra interfaz parte por parte.

## Capitulo 2. Imprimiendo las filas por pantalla
Primero vamos a convertir nuestro componente simple App en uno personalizado. Un componente personalizado ofrece muchas ventajas:reutilizar ese componente, incluir métodos, utilizar los componentes de API state y props.... 

Utilizando el componente de la API de React state, almacenaremos las filas que tenemos impresas por pantalla y veremos como incorporar métodos dentro de nuestro elemento DOM.

### Componentes personalizados
React nos deja crear componentes diferentes a las típicas etiquetas HTML. Estos nos sirve para poder re-utilizar componentes en diferentes partes del código.

Primero tenemos que importar React.Component. Cuando vamos a crear un componente personalizado, creamos la “class” y extendemos “extends Component”. Dentro vamos a utilizar render para ensamblar un componente. Después hacemos un return con el componente.

Es aconsejable nombrar a los componentes con la primera letra en mayúscula para no confundirnos con los componentes de la DOM.

Dentro del componente llamamos a render() para renderizar todo el contenido del componente, después se devuelve con return().

e.j.
```
class App extends Component {

    state = {
        store: [ 'red', 'blue', 'green']
    }

    addRow = (color) => {
        const {store} = this.state

        this.setState({
            store: this.state.store.concat(color)
        })
    }

    render(){
        return(
            <div>
                <button onClick={ (e) => {this.addRow("blue")}} >blue</button>
                <button onClick={ (e) => {this.addRow("yellow")}} >yellow</button>
                <button onClick={ (e) => {this.addRow("orange")}} >orange</button>
                <button onClick={ (e) => {this.addRow("purple")}} >purple</button>
                <div>
                    {this.state.store.map((fila, i) => <div key={i}> {fila} </div>)}
                </div>
            </div>
        )
    }
}
```
Ahora App se ha convertido en un componente personalizado, es necesario para poder añadir estilo en nuestras lineas y poder mostrar el color seleccionado. Mas adelante podremos comprobar como utilizar componentes personalizados que utilizan etiquetas diferentes a las de HTML.

[React Expres - Components ](http://www.react.express/components)

### Componentes de API props y state
Los componentes de la API de React facilitan el almacenamiento y transporte de de información de un componente. Podemos almacenar diferentes tipos de información.

Hay dos tipos de componentes, **props** y **state**.

**props** almacena las propiedades de un componente y pasan de padres a hijos cuando es instanciado y no puede ser modificado. Solo ese componente puede consultar su propio props.

**state** puede cambiar durante el transcurso de la aplicación. A diferencia de porps, state si puede modificarse. El propio componente puede auto-gestionar ese estado pero no debe modificarse directamente, hay que utilizar el método this.setState.  

Segun el manual de React, debe de evitarse tener demasiados componentes con estado, ya que aumenta la complejidad.

e.j.
```

...

 class App extends Component {

    state = {
        store: [ 'red', 'blue', 'green']
    }

    ...

    <button onClick={ (e) => {this.addRow("purple")}} >purple</button>
      <div>
          {this.state.store.map((fila, i) => <div key={i}> {fila} </div>)}
      </div>

    ...

```
Al crear el elemento App, introdiccimos por defecto 3 filas en state, esto nos permite mostrar siempre esas filas al cargar la aplicación por primera vez. Utilizaremos state.store para almacenar las filas seleccionadas en la aplicación.

Mas abajo, al crear el componente simple button, introduccimos en su props la función que nos permite añadir las filas cuando pulsamos un botón.

Continuando hacia abajo, vemos otro elemento simple div, como puedes ver, insertamos una función de JavaScript entre corchetes que busca una por una con la función .map todas las filas almacenadas en state.store y por cada fila crea un otro elemento div dentro del primero con el color de la fila seleccionada.

[React Expres - Component API ](http://www.react.express/component_api)

### Identificador Key en las listas
Cuando utilizamos una lista en nuestra aplicación React, tenemos que asignarle una propiedad única a cada lista. Si no lo hacemos, nuestro programa se ejecutara con normalidad, pero en la consola de debuggin nos mostrara un error avisándonos que debe de tenerla.  

Esta key sirve a React para poder determinar la identidad del elemento y optimiza el funcionamiento para React. 

Por ejemplo, podemos tener una lista con mil items y solo queremos borrar uno, React desde la key puede localizarlo. Esto ahorrara a React borrar todos los elementos y volver a imprimir la lista.

En el siguiente link puedes encontrar varias formas de agregar una key a tu cuando creas una lista.

e.j.
``` 

...

<div>
    {this.state.store.map((fila, i) => <div key={i}> {fila} </div>)}
</div>

...

```
Cuando la aplicación genera todas las filas almacenadas en state.store añade el número de index que ocupa como key.

[React Expres - List and Keys ](http://www.react.express/lists_and_keys)

### [APLICACIÓN] Step 2
Con diferentes métodos que vamos a utilizar coneguiremos imprimir una fila del con el color del botón pulsado y imprimirla por pantalla. Utilizaremos el componente de API state para almacenar los colores.
```
import React, { Component } from 'react'
import { render } from 'react-dom'


class App extends Component {

    state = {
        store: [ 'red', 'blue', 'green']
    }

    addRow = (color) => {
        const {store} = this.state

        this.setState({
            store: this.state.store.concat(color)
        })
    }

    render(){
        return(
            <div>
                <button onClick={ (e) => {this.addRow("blue")}} >blue</button>
                <button onClick={ (e) => {this.addRow("yellow")}} >yellow</button>
                <button onClick={ (e) => {this.addRow("orange")}} >orange</button>
                <button onClick={ (e) => {this.addRow("purple")}} >purple</button>
                <div>
                    {this.state.store.map((fila, i) => <div key={i}> {fila} </div>)}
                </div>
            </div>
        )
    }
}

render(
    <App />,
    document.getElementById('root')
)
```
Primero pasamos nuestro componente simple **App** a un componente personalizado. Dentro del componente vamos a añadir en el complemento de la API state, un estado llamado store. Esto nos servirá como almacén para guardar los colores. Por defecto incluyo tres colores.

A continuación, debemos asignar un  método para imprimir los colores almacenados en state.store. Dentro de render, utilizamos una extensión del this.state para almacenar a la variable store el valor que tiene la variable con su mismo nombre dentro de state. Esto nos asigna en store todos los colores almacenados. Utilizamos los corchetes para indicar que es JavaScript.

Utilizando el método [.map](https://developer.mozilla.org/es/docs/Web/JavaScript/Referencia/Objetos_globales/Array/map) creamos un elemento &lt;div&gt; con cada color en su interior. Como puedes ver, damos como key el index que le corresponde dentro de store ya que no tenemos un id único.

Ahora vamos a crear el método que nos permite crear una fila al pulsar el botón.  
El método con [fat arrow](https://www.google.es/search?q=fat+arrow&oq=fat+arrow&aqs=chrome..69i57j69i60l2j0l3.1543j0j4&sourceid=chrome&ie=UTF-8) addRow recibe un parámetro, que sera el valor del color del botón presionado.  
Utilizando la [destructuración](http://www.react.express/destructuring), igualamos {store} al valor de this.state.store, en esta variable añadiremos el nuevo color y modificaremos this.state.store con los valores actuales más el nuevo color.  
Como puedes ver utilizamos this.setState para modificarlo.

Pasamos a introducir el callback del método addRow dentro de los botones. Todo lo que introducimos dentro de las etiquetas de los componentes se convierten en atributos para este. Podemos asignar un atributo llamado color, key, etc etc.. Todo esto queda reflejado en los props del complemento y lo podemos utilizar a la hora que lo instanciamos.  
onClick es un controlador de eventos igual que del que disponemos en JavaScript, al pulsar este elemento, se activa el contenido de su interior. Si no necesitamos pasar ningún parámetro a la función, podríamos introducir dentro de onClick el nombre de la función empezando por this., pero como necesitamos pasar el color del botón pulsado, tenemos quehacer un método [fat arrow](https://www.google.es/search?q=fat+arrow&oq=fat+arrow&aqs=chrome..69i57j69i60l2j0l3.1543j0j4&sourceid=chrome&ie=UTF-8) pasamos el item y llamamos a addRow pasando el valor del color.

Como puedes comprobar, ahora cuando pulsamos un botón, generamos una fila con el nombre del color seleccionado.

## Capitulo 3. Dando color a las filas.
Vamos a ver como dar color a nuestras filas con el estilo inline, y como utilizar el componente props.  

Cambiaremos a un componente personalizado nuestra &lt;div&gt; donde mostramos las filas. Podremos ver como props pasa de padre a hijo.

### In-line style
Existen muchas formas de poder crear el contenido para un estilo de css, todas ellas muy parecidas. La selección del método suele ser personal. En este articulo voy a utilizar el estilo in-line que es el más aconsejable cuando empiezas a utilizar React.  
Aquí tienes una lista de los diferentes estilos disponibles en el manual oficial de React, puedes verlos pulsando este [link](http://www.react.express/styling).

e.j.
```

...

      paintRow = (color, i) => {
        const row = {
            backgroundColor: color,
            padding: 5,
        }

...

```
Cada vez que creemos un elemento personalizado Filas, añadiremos una nueva variable llamada color. Esta variable contiene el valor del color del botón seleccionado, y indicamos que backgroundColor del componente Filas es igual al valor del botón seleccionado.  

Como ves es muy parecido a la hora de asignar estilo CSS con JSX. Hay que recalcar que con esto no modificamos la hoja de CSS, es una presentación de estilo virtual desde el interior de la DOM.  

Puedes ver una lista con las diferentes propiedades que puedes utilizar pulsando [aqui](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Properties_Reference).  

[React Expres - Styling ](http://www.react.express/styling)

### [APLICACIÓN] Step 3
```
import React, { Component } from 'react'
import { render } from 'react-dom'

class Filas extends Component {
    paintRow = (color, i) => {
        const row = {
            backgroundColor: color,
            padding: 5,
        }

        return(
            <div style={row} key={i}>
                {color}
            </div>
        )
    }

    render(){
        const {store} = this.props
        return(
            <div>
                {store.map(this.paintRow)}
            </div>
        )
    }
}

class App extends Component {

    state = {
        store: [ 'red', 'blue', 'green']
    }

    addRow = (color) => {
        const {store} = this.state

        this.setState({
            store: this.state.store.concat(color)
        })
    }

    render(){
        const {store} = this.state
        return(
            <div>
                <button onClick={ (e) => {this.addRow("blue")}} >blue</button>
                <button onClick={ (e) => {this.addRow("yellow")}} >yellow</button>
                <button onClick={ (e) => {this.addRow("orange")}} >orange</button>
                <button onClick={ (e) => {this.addRow("purple")}} >purple</button>
                <Rows 
                    store={this.state.store}
                />
            </div>
        )
    }
}

render(
    <App />,
    document.getElementById('root')
)
```
Si bajamos hasta después de los botónes, podemos ver que nos encontramos con un nuevo componente personalizado llamado Rows. Este componente substituye el antiguo &lt;div&gt; que hacia de contenedor de las filas.  
Dentro de la etiqueta Rows, enviamos el this.state.store con todas las filas. Esto lo recibirá el componente Rows como props.store.  

Dentro del componente Rows, mirando el interior del render() encontramos el mismo formato de estructura en JSX que utilizábamos en el anterior ejemplo para imprimir las filas, solo que esta vez, dentro de .map no contiene el componente de la DOM, sino que llama al método paintRow.

El método paintRow crea el componente que se convierte en la fila. Le pasamos el parámetro color y i. Color contiene un string con el valor del color y i es el index que contiene de la lista dentro de store. La ventaja que nos da este método es que nos permite añadir propiedades css incluyendo dentro de su etiqueta un estilo. La variable row contiene propiedades de css, backrgoundColor viene a ser lo mismo que background-color de css.  
Le indicamos que backgroundColor debe de ser del color que le pasamos en la variable color.  

Asignamos el estilo dentro de la instancia del componente añadiendo el nombre dentro del atributo style={}.

Como puedes comprobar ahora nuestras filas se muestras del color del botón pulsado.

Ahora mismo lo más lógico seria aplicar lo mismo que hemos hecho en Rows con los botones para poder reutilizar estos en cualquier otra parte del código, pero de momento lo vamos a dejas así.

## Capitulo 4. Borrar las filas
Vamos a crear un método que borre las filas al hacer click sobre ellas. Hasta ahora no hemos visto como podemos pasar el callback de un método padre a un hijo. Como hijo quiero decir que esta dentro del componente padre, no confundir con herencias, hay que tener claro que cuando hablamos de hijos en React es sobre los diferentes niveles de componentes.

### Eventos
Los eventos se disparan hacia arriba, de hijos a padres. El evento que active un componente puede ser recogido por el padre.

e.j.
```

...

class Rows extends Component {

  ...

  return(
            <div style={row} key={i} onClick={() => this.props.containsRemoveRowMethod
  
  ...

class App extends Component {

  ...

  removeRow = (index) => {
    const {store} = this.state
    this.setState({
        store: store.filter((store, i) => i !== index )
    })

  ...

  <Rows 
      store={this.state.store}
      containsRemoveRowMethod={this.removeRow}
  />

...

```
El componente App contiene una función llamada borrar fila. Cada vez que creamos una fila, enviamos por props esta función desde la variable llamada containsRemoveRowMethod asignandola entre corchetes y con el prefijo this.

Desde el componente Rows, devolvemos el componente que en su interior contiene un controlador de eventos que al pulsar esa fila, llamara al método que contiene el elemento padre utilizando this.props.containsRemoveRowMethod.

[Blog Carlos azaustre](https://carlosazaustre.es/blog/estructura-de-un-componente-en-react/)

### [APLICACIÓN] Step 4
```
import React, { Component } from 'react'
import { render } from 'react-dom'

class Rows extends Component {
    paintRow = (color, i) => {
        const row = {
            backgroundColor: color,
        }

        return(
            <div style={row} key={i} onClick={() => this.props.containsRemoveRowMethod(i) }>
                {color}
            </div>
        )
    }

    render(){
        return(
            <div>
                {this.props.store.map(this.paintRow)}
            </div>
        )
    }
}


class App extends Component {

    state = {
        store: [ 'red', 'blue', 'green']
    }

    addRow = (color) => {
        const {store} = this.state

        this.setState({
            store: this.state.store.concat(color)
        })
    }

    removeRow = (index) => {
        const {store} = this.state
        this.setState({
            store: store.filter((fila, i) => i !== index )
        })
    }

    render(){
        const {store} = this.state
        return(
            <div>
                <button onClick={ (e) => {this.addRow("blue")}} >blue</button>
                <button onClick={ (e) => {this.addRow("yellow")}} >yellow</button>
                <button onClick={ (e) => {this.addRow("orange")}} >orange</button>
                <button onClick={ (e) => {this.addRow("purple")}} >purple</button>
                <Rows 
                    store={this.state.store}
                    containsRemoveRowMethod={this.removeRow}
                />
            </div>
        )
    }
}

render(
    <App />,
    document.getElementById('root')
)
```
Primero he creado una método removeRow que recibe el index del componente seleccionado. Dentro, asignamos todo el contenido de this.state.store a la variable store a través del método de [destructuración]() y después actualizamos el state.store asignando el valor de store que primero hemos filtrado con el método filter y que oculta el index del componente seleccionado.  

En el callback del componente Rows enviamos la instancia del método con un .this delante, pasamos el método a través del props.

Dentro del componente Rows, en la instancia del componente hemos añadido el callback a la función, utilizando el evento onClick que al pulsar envia hacia arriba la llamada al enlace de removeRow y que contiene el index del componente seleccionado, con lo cual actualizamos el state filtrando el número de index del componente.

Como puedes comprobar si pulsas encima de un color, se elimina.

Con esto hemos acabado esta sencilla aplicación. Poco a poco voy a ir profundicando más y espero poder traeros novedades con Reac y Redux

### Capitulo 5. Modular nuestra aplicación (ultimo capítulo)
Todas las aplicaciones deben de estar moduladas, esto nos permite una aplicación ordenada y todas sus partes van a poder ser reutilizadas en cualquier parte del código o otras aplicaciones.

Por norma general, se separan los componentes de la lógica del programa, podemos separar también funciones.

Index
```
import { render } from "react-dom";
import React from "react";

import App from "./App";

render(
  <App />, 
  document.getElementById("root")
);
```
Es el punto de entrada con nuestro código JavaScript. Se renderiza toda la aplicación en la DOM.

App
```
import React, { Component } from 'react'

import Rows from './Rows.js'

export default class App extends Component {

    state = {
        store: [ 'red', 'blue', 'green']
    }

    addRow = (color) => {
        const {store} = this.state

        this.setState({
            store: this.state.store.concat(color)
        })
    }

    removeRow = (index) => {
        const {store} = this.state
        this.setState({
            store: store.filter((store, i) => i !== index )
        })
    }

    render(){
        const {store} = this.state
        return(
            <div>
                <button onClick={ (e) => {this.addRow("blue")}} >blue</button>
                <button onClick={ (e) => {this.addRow("yellow")}} >yellow</button>
                <button onClick={ (e) => {this.addRow("orange")}} >orange</button>
                <button onClick={ (e) => {this.addRow("purple")}} >purple</button>
                <Rows 
                    store={this.state.store}
                    containsRemoveRowMethod={this.removeRow}
                />
            </div>
        )
    }
}
```
Contiene la lógica general del programa y sirve como contenedor de todos los componentes del nivel superior. En nuestro caso contiene las filas, los métodos y llama a los componentes

Rows
```
import React, { Component } from "react";

export default class Filas extends Component {
    paintRow = (color, i) => {
        const row = {
            backgroundColor: color,
            padding: 5,
        }

        return(
            <div style={row} key={i} onClick={() => this.props.containsRemoveRowMethod(i) }>
                {color}
            </div>
        )
    }

    render(){
        return(
            <div>
                {this.props.store.map(this.paintRow)}
            </div>
        )
    }
}
```
Filas es un componente personalizado. Cada componente tiene que estar en un archivo separado.

## Conclusión
En este articulo te he mostrado la base de React. El código final puede ser más optimizado pero no he querido liar mucho el articulo, mi intención ha sido "ir directo al grano".

Poco a poco vamos a profundizar con React, así que sigue atento, pronto llegaran noticias nuevas...

**A tope con @mentoringJS!  
Jordi Gomper.**

