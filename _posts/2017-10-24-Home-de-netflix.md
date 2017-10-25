---
layout: post
title: Home de Netflix
img: blog/i_net.PNG
categories: articulo
---

Hola chic@s! En este articulo voy a hacer una replica del home de la famosa Netflix.

## [Aprende Javascript con MentoringJS - Step 13](http://mentoringjs.com/)  

Basándome en el articulo de [Sophia Shoemaker y Jack Oliver](https://www.fullstackreact.com/react-daily-ui/003-landing-page/). A diferencia de la fuente, mi home de Netflix está estructurado bajo ESCM6.  

Puedes encontrar la aplicación en [Github](https://github.com/jordigomper/netflix-con-react) y ver su funcionamiento en [Surge](http://jgomper-netflix.surge.sh/).  

Las consultas la vamos hacer sobre la API que nos ofrece [themoviedb](https://www.themoviedb.org/documentation/api) que tiene una extensa base de datos de películas. Para hacer las peticiones necesitamos una key, para obtenerla puedes registrarte y pulsando sobre la imagen de perfil selecciona settings y API.  

<p data-height="800"  data-with="600"data-theme-id="0" data-slug-hash="qPzwJa" data-default-tab="result" data-user="JordiGomper" data-embed-version="2" data-pen-title="Netflix React" class="codepen">See the Pen <a href="https://codepen.io/JordiGomper/pen/qPzwJa/">Netflix React</a> by Jordi (<a href="https://codepen.io/JordiGomper">@JordiGomper</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script> 

Ahora voy a enseñar un breve resumen de los diferentes componentes:  

* **index.js:** Contiene el componente App y lo introduce en el DOM.
* **App.js:** Componente contenedor con lógica. Contiene métodos que permiten buscar películas.
* **Logo.js:** Contiene el logo del sitio web.
* **Navigation.js:** Es el menú de la web, en este caso no tiene ninguna función.
* **UserProfile.js:** Muestra el nombre y la imagen del usuario. No tiene ninguna funcionalidad solo decorativo.
* **Hero.js:** Muestra la imagen de fondo principal y una descripción, en este caso de la serie Narcos.
* **TitleList.js:** Componente contenedor con lógica. Se encarga de enviar la petición de búsqueda a la API y imprimir por pantalla el resultado. Contiene varios métodos de ciclo de vida.
* **Item.js:** Se encuentra en el interior de TitleList y es el encargado de recoger la información de una película y mostrarla.
* **ListToggle.js:** Componente con lógica que contiene los botones para agregar una película a favoritos, se encuentra en el interior de Item.

Ahora voy a ir mostrando el interior de los componentes siguiendo el recorrido que sigue el flujo de datos al cargar la aplicación:  

Primero llamo a **App** desde **index**:

```
import React from 'react';
import ReactDOM from 'react-dom';
import App from "./containers/App.js"
import "./css/Index.css"

ReactDOM.render(
    <App />,
    document.getElementById('root')
);
```

En **App** se importan los diferentes componentes, métodos y estilo:  

**App.js**
```
import React from 'react';
import { Component } from 'react'
import "../css/App.css"
import Navigation from "../components/Navigation.js"
import UserProfile from "../components/UserProfile.js"
import Hero from "../components/Hero.js"
import TitleList from "./TitleList.js"
import Logo from "../components/Logo.js"

export default class App extends Component {
    constructor(props) {
        super(props);
        this.state = {
            searchTerm:"",
      searchUrl:""
        }
        this.handleChange.bind(this)
    this.handleKeyUp.bind(this)
    }

    handleKeyUp = (event) => {
    if(event.key === 'Enter' && this.state.searchTerm !== ""){
      var searchUrl =  "search/multi?query=" + this.state.searchTerm + "&api_key=166624c030b91c943c397020f20525b4";
      this.setState({
        searchUrl: searchUrl
      })
    }
  }

  handleChange = (event) => {
    this.setState({
      searchTerm: event.target.value
    })
  }

    render() {
        return(
            <div>
        <header className="Header">
          <Logo />
          <Navigation />
          <div id="search" className="Search">
            <input onChange={this.handleChange} onKeyUp={this.handleKeyUp} value={this.state.searchTerm} placeholder="Search for a title..."/>
          </div>
          <UserProfile />
        </header>
        <Hero />
        <TitleList title="Search Results" url={this.state.searchUrl}/>
        <TitleList title="Top TV picks for Jack" url='discover/tv?sort_by=popularity.desc&page=1'/>
        <TitleList title="Trending now" url='discover/movie?sort_by=popularity.desc&page=1'/>
        <TitleList title="Most watched in Horror" url='genre/27/movies?sort_by=popularity.desc&page=1'/>
        <TitleList title="Sci-Fi greats" url='genre/878/movies?sort_by=popularity.desc&page=1'/>
        <TitleList title="Comedy magic" url='genre/35/movies?sort_by=popularity.desc&page=1'/>
      </div>
        )
    }
}
```

Lo primero que hace es agregar al state las variables **searchTerm** que guarda el valor de la búsqueda y **searchUrl** donde almacena la URL creada para hacer la petición.  

```
constructor(props) {
        super(props);
        this.state = {
            searchTerm:"",
      searchUrl:""
        }
        this.handleChange.bind(this)
    this.handleKeyUp.bind(this)
    }
```

El método **handleKeyUp** comprueba cuando se pulsa enter en el interior del input encargado de la búsqueda y que contiene algún texto. Genera la URL para la petición y la almacena en **searchUrl**.  

```
handleKeyUp = (event) => {
    if(event.key === 'Enter' && this.state.searchTerm !== ""){
      var searchUrl =  "search/multi?query=" + this.state.searchTerm + "&api_key=166624c030b91c943c397020f20525b4";
      this.setState({
        searchUrl: searchUrl
      })
    }
  }
```

El método **handleChange** va almacenando todos los valores introducidos en el input de la búsqueda.  

```
handleChange = (event) => {
    this.setState({
      searchTerm: event.target.value
    })
  }
```

Desde el interior de header carga **Logo**, **Navigation**, **input con id="search"** y **UserProfile**. El elemento input contiene dos controladores de evento para los métodos **handleChange** y **handleKeyUp**.  

```
<header className="Header">
        <Logo />
        <Navigation />
        <div id="search" className="Search">
            <input onChange={this.handleChange} onKeyUp={this.handleKeyUp} value={this.state.searchTerm} placeholder="Search for a title..."/>
        </div>
    <UserProfile />
</header>
```

Después de header, se carga **Hero** con una serie predeterminada mostrando la imagen de fondo en grande y una breve descripción.  

Abajo **TitleList** muestra diferentes secciones de películas. En el primer caso es para los resultados de una búsqueda que solo se muestra cuando se ha introducido un valor y se a pulsado enter. El resto de búsquedas son predeterminadas desde la **App** mostrando diferentes categorías.  

```
<TitleList title="Search Results" url={this.state.searchUrl}/>
<TitleList title="Top TV picks for Jack" url='discover/tv?sort_by=popularity.desc&page=1'/>
<TitleList title="Trending now" url='discover/movie?sort_by=popularity.desc&page=1'/>
<TitleList title="Most watched in Horror" url='genre/27/movies?sort_by=popularity.desc&page=1'/>
<TitleList title="Sci-Fi greats" url='genre/878/movies?sort_by=popularity.desc&page=1'/>
<TitleList title="Comedy magic" url='genre/35/movies?sort_by=popularity.desc&page=1'/>
```

Al cargar la página, envio a **TitleList** las URL predeterminadas por props. **TitleList** en su primera instancia crea en state las variables data que va a contener los resultados de una petición y mounted que se encarga de hacerla visible cuando detecta que se ha recibido una petición:  

```
constructor(props) {
    super(props);

    this.state = {
  data: [],
  mounted: false
    }
}
```

Una vez montado el componente en el DOM, se ejecuta **componentDidMount** que comprueba que existe una URL. Llama a **loadContent** que es el encargado de hacer la petición y cambia el state mounted a true para mostrarse en pantalla.  
```
componentDidMount(){
    if(this.props.url !== '') {
      this.loadContent();
      this.setState({
        mounted:true
      })
    }
}
```

El método **loadContent** genera la variable requestUrl para hacer la petición y hace ferch sobre esta URL, recoge los resultados de la petición almacenándolos en data.  

```
loadContent = () => {
    var requestUrl ='https://api.themoviedb.org/3/' + this.props.url + '&api_key=166624c030b91c943c397020f20525b4';
    fetch(requestUrl).then((response) => {
      return response.json();
    }).then((data) => {
      this.setState({
        data: data
      })
    }).catch((err) => {
        console.log("There has been error");
      })
  }
```

Una vez confirmada la petición, vuelve a renderizar el comopnente que comprueba que existe los resultados de la petición. En la variable titles asignamos el resultado de los 5 primeros resultados contenidos en data, agregandolos en diferentes propiedades de title. Por cada elemento se genera un componente **Item** con la información de la película. Ahora la variable titles contiene un componente Item con la información de la película y se introduce en la devolución.  

```
    render() {
         let titles = '';
    if(this.state.data.results){
      titles = this.state.data.results.map((title, i) => {
        if(i < 5){
          var name = '';
          var backDrop = 'http://image.tmdb.org/t/p/original' + title.backdrop_path;
          if(!title.name) {
            name = title.original_title;
          } else {
            name = title.name;
          }

          return (
            <Item key={title.id} title={name} score={title.vote_average} overview={title.overview} backdrop={backDrop}/>
          )
        } else {
          return (
            <div key={title.id}></div>
          )
        }
      })
    }

        return(
            <div ref="titlecategory" className="TitleList" data-loaded={this.state.mounted}>
        <div className="Title">
          <h1>{this.props.title}</h1>
          <div className="titles-wrapper">
            {titles}
          </div>
        </div>
      </div>
        )
    }
}
```

En el caso de una búsqueda, desde **componentWillReciveProps** esperamos ese recibir por props una URL. Cuando se ejecuta, comprueba que la busqueda introducida es diferente a la actual y que contiene texto. Asigno la nueva URL recibida, cambio el estado de mounted a true y llamo a una función que contiene el método **loadContent** para hacer la petición.  

Es muy importante que el método **loadContent se ejecute solo cuando se haya cambia el estado del componente**. Como ya sabes,  al ejecutar un cambio de estado con **setState** este cambio no se lleva a cabo al momento, sino que espera al momento optimo para cambiarlo. Si ejecuto **loadContent** sin esperar a ese cambio, el resultado de la petición seria nulo ya que enviamos una URL desde state que todavía no se a asignado. Por eso, introduzco una coma después de los corchetes del interior de setState con la función loadContent que se ejecutara una vez se haya producido ese cambió:  

```
componentWillReceiveProps(nextProps) {
    if(nextProps.url !== this.props.url && nextProps.url !== ''){
      this.setState({
        url: nextProps.url,
        mounted: true
      }, function () {
        this.loadContent();
      })   
    }
}
```

En el interior de **Item** se carga toda la información de la película que le enviamos desde props. Contiene ListToggle para los botones de favorito.  

```
import React, { Component } from 'react'
import "../css/App.css"
import ListToggle from "../containers/ListToggle.js"

export default class Item extends Component {
    render() {
        return(
            <div className="Item" style={{backgroundImage: 'url(' + this.props.backdrop + ')'}}>
        <div className="overlay">
          <div className="title">{this.props.title}</div>
          <div className="rating">{this.props.score} / 10</div>
          <div className="plot">{this.props.overview}</div>
          <ListToggle />
        </div>
      </div>
        )
    }
}
```

**ListTiggogle** agrega un estado predeterminado en su primera carga con **toggle:fale**. Dependiendo valor de toggle, mostrara el botón añadir o el botón que indica que ya esta en tu lista.  

```
constructor(props) {
    super(props);
    this.state = {
        toggled:false
    }
}
```

El método **handelClick** que esta introducido con un controlador de eventos en el primer elemento div es el que se encarga de cambiar el **state.toggle**. Cuando ese elemento es pulsado, si el estado es true lo cambia a false y viceversa.  

```
handleClick = () => {
    if(this.state.toggled === true) {
      this.setState({
        toggled: false
      })
    } else {
      this.setState({
        toggled: true
      })
    }
}
```

Después devuelve el componente.  

```
 render() {
        return(
            <div  onClick={this.handleClick} className="ListToggle" data-toggled={this.state.toggled}>
        <div>
          <i className="fa fa-fw fa-plus"></i>
          <i className="fa fa-fw fa-check"></i>
        </div>
      </div>
        )
    }
}
```

La verdad es que los resultados son magníficos y no implica mucha dificultad.  

Al crear esta aplicación me encontré por primera vez con el problema de que setState no hace un cambio instantáneo. Tras estar debuggando durante un buen rato, vi como enviaba una requesUrl totalmente vacía y solo mostraba la categoría búsqueda al hacer una segunda petición y con el resultado de la primera.  

Me acorde de los primeros artículos que había leído durante mi iniciación en React y sabia que ese método solo debería ejecutarse después de que se actualice el estado. Buscando por internet probé diferentes formas hasta encontrar la que he introducido.  

Espero que te guste este articulo y que te ayude a la hora de hacer tu home de Netflix con tus series favoritas.  

Un saludo!!  

**A tope con @mentoringJS!  
Jordi Gomper.**