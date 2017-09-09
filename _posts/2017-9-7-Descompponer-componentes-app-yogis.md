---
layout: post
title: Descomponiendo mi aplicación yogis
img: blog/i_app.jpg
categories: app
---

Hola chicos! En este articulo voy a descomponer mi app Yogis, intentando hacer todos los componentes re-utilizables.

## Introducción
Voy a repasar las secciones principales de mi aplicación y voy a indicar con que componente se va a mostrar, más abajo describo los diferentes componentes:

**Index:** Muestra todos los artículos y videos sobre posturas, batidos. Mostrara la imagen en grande con el titulo y un breve resumen del inicio de cada articulo. Index no deja de ser una lista de artículos con una breve descripción, voy a utilizar el componente ListTemp donde pasare un array que contiene los diferentes artículos y un formato especial para esta sección.

**Artículos:** Al pulsar un artículo desde Index, nos lo muestra. Un artículo puede contener varias imágenes. Esta sección utiliza ArticleTemp, es perfecta para mostrar artículos.

**Batidos:** Muestra una lista con las imágenes en miniatura de los batidos y una breve descripción. Al pulsar sobre el batido nos envía a la página de ese batido. Utilizo ListTemp donde paso por props los diferentes batidos.

**Retos:** Esta sección muestra la descripción de un reto que está activo. Primero contiene un sub-menú con las opciones Reto principal, reto del día y calendario. Al pulsar retos en el menú principal nos envía a la página retos principal por defecto. Utilizo ChallengeIndex.

**Retos principal:** Cuando el usuario no se ha unido en el reto, muestra un botón en rojo "Unirse al reto". Después de este botón, se muestra una explicación de que consiste el reto y la lista de las cosas que necesitamos, contendrá un video explicativo. Por ultimo, contiene un muro donde los usuarios pueden preguntar las diferentes dudas que tengan. Utilizo ButtonTemp, aquí el elemento button mostrara el texto "unirse al reto".

**Reto del dia:** Muestra la información del reto del día, por ejemplo tiene que mostrar que batido y como hacerlo o un video explicándolo. Debajo de esta explicación un botón "reto conseguido" que abre la cámara del teléfono donde el usuario debe hacer una foto. Esta foto se enviara automáticamente al muro que hay debajo del botón. Este muro solo muestra las fotos de los diferentes usuarios. Utilizo ButtonTemp y el elemento button muestra el texto "conseguido!". El muro solo muestra las fotos subidas de batidos, no tiene la opción de escribir.

**Reto Calendario:** Muestra una lista con las imágenes en miniatura y descripciones de los diferentes batidos que forman el reto. Cada batido mostrara el orden del día. Utilizo ListTemp.

**Usuario**: Muestra las diferentes opciones de un usuario. Cada usuario puede modificar diferente información y notificaciones.

La aplicación contiene un menú principal y un sub-menú para las secciones que se encuentran en retos.

## Descomponiendo la App
Descomponiendo la aplicación, he creado los siguientes componentes:

### Componentes de apoyo
**Index:** 
```
import React, { Component } from 'react'
import { render } from 'react-dom'
import App from './App.js'

export default class Index extends Component {

    render(){
        return(
            <div>
                <App />
            </div>
        )
    }
}

render(
    <Index />,
    document.getElementById('root')
)
```
Contiene el componente **App** y lo introduce en la DOM.  

**App:** 
```
import React, { Component } from 'react'
import { render } from 'react-dom'
import Header from './Header.js'
import ArticleTemp from './ArticleTemp.js'
import ListTemp from './ListTemp.js'
import ChallengeIndex from './ChallengeIndex.js'

export default class App extends Component {
    render(){
        return(
            <div>
                <Header />
                <div id="display" ></div>
            </div>
        )
    }
}
```
Contiene **Header** y un elemento div con la id="display" donde se mostraran las diferentes secciones de la app. La idea es actualizar solo el elemento "div id="display". Se importan los diferentes componentes de la aplicación.  

**Header:** 
```
import React, { Component } from 'react'
import { render } from 'react-dom'
import Title from './Title.js'
import Nav from './Nav.js'

export default class Header extends Component {
    render(){
        return(
            <header>
                <Title />
                <Nav />
            </header>
        )
    }
}
```
Contiene los componentes **Title** y **Nav**. Como nunca se modifica, solo lo incorporo en el componente **App**, actualizando solo las diferentes secciones elegidas en el menú.  

**Title:** 
```
import React, { Component } from 'react'
import { render } from 'react-dom'

export default class Title extends Component {
    render(){
        return(
            <title></title>
        )
    }
}
```
Contiene el elemento title que muestra el titulo de la página.  

**Nav:** 
```
import React, { Component } from 'react'
import { render } from 'react-dom'

export default class Nav extends Component {

    render(){
        return(
            <nav>
                <ul>
                    <li>Princpal</li>
                    <li>Articulos</li>
                    <li>Batidos</li>
                    <li>Retos</li>
                    <li>Mi cuenta</li>
                </ul>
            </nav>
        )
    }
}
```
Contiene el menú principal de la aplicación.  

**ArticleTemp:** 
```
import React, { Component } from 'react'
import { render } from 'react-dom'

export default class ArticleTemp extends Component {
    // const {article} = this.props

    render(){
        return(
            <div>
                <article >
                    <header> {/* article.header */} </header>
                    <img> {/* article.image */} </img>
                    <p> {/* article.description */} </p>
                </article>  
            </div>
        )
    }

}
```
Es una plantilla para mostrar los artículos o descripciones en cualquier zona de la app. A través de props mandamos la información que compone el articulo. Se utiliza para: Articulo, Batidos y el componente ButtonTemp.

**ListTemp:**  
```
import React, { Component } from 'react'
import { render } from 'react-dom'

export default class List extends Component {

    render(){
        return(
            <div>
                {/*this.props.list.map(this.showItem(index))*/}
            </div>
        )
    }   
}
```
Recibe un array de objetos y crea una lista con la imagen en miniatura y una breve descripción. Al pulsar envía al articulo. Se utiliza para mostrar la página principal, la lista de batidos y la lista de batidos que componen un reto.

**ChallengesIndex:**  
```
import React, { Component } from 'react'
import { render } from 'react-dom'
import SubNav from './SubNav.js'
import ButtonTemp from './ButtonTemp.js'
import ForumTemp from './ForumTemp.js'

export default class ChallengesIndex extends Component {
    render(){
        return(
            <div>
                <SubNav />
                <div ></div>
            </div>
        )
    }
}
```
Añade la el sub-menú que utiliza esta sección. Contiene un elemento "div id="challenge"" donde se introducirán los componentes que forman parte de esta sección.

**SubNav:**  
```
import React, { Component } from 'react'
import { render } from 'react-dom'

export default class SubNav extends Component {
    state = {
        menu: ['Reto principal','Reto del dia','Calendario']
    }
    
    render(){
        return(
            <nav>
                <ul>
                    {this.state.menu.map((item, index) => {
                        <li key={index}> {item} </li>
                    })}
                </ul>
            </nav>
        )
    }
}
```
Muestra el sub-menú de la sección de retos.

**ButtonTemp:**
```
import React, { Component } from 'react'
import { render } from 'react-dom'
import ArticleTemp from './ArticleTemp.js'
import Forum from './ForumTemp.js'

export default class ChallengeDay extends Component {
    render(){
        return(
            <div>
                <ArticleTemp />
                <button>{this.props.buttontext}</button>
                <Forum />
            </div>
        )
    }
}
```
Esta plantilla contiene los componentes ArticleTemp para poder mostrar la descripción, un botón y un muro que dependiendo en que lugar se monte este componente puede tener diferentes funciones. Por ejemplo en la sección de reto disponible mostrara información del reto, el botón sirve para unirse y el muro para que los usuarios comenten diferentes dudas. Se utiliza en el index de retos disponibles y reto del día.

**ForumTemp:**
```
import React, { Component } from 'react'
import { render } from 'react-dom'

export default class Forum extends Component {
    render(){
        return(
            <div>
                <div>
                        {/*muestra el foro*/}
                </div>
                <form>
                    <input type="placeholder" value="Introduce tu comentario..." />
                    <button type="submit" value="Enviar comentario" />
                </form>
            </div>
        )
    }
}
```
Desde props enviamos la información del muro, luego lo muestra con unas características que dependen de en que sección se encuentre.  

La idea es reutilizar todo lo posible. Por ejemplo cuando pulsas en el menú la opción Batidos, envía al componente ListTemp por porps un array con todos lo batidos, lo mismo con retos disponibles o reto del día, al pulsar, envía por props a ButtonTemp toda la información para montar ese componente.  

Step by step mi aplicación va cogiendo forma, espero que te pueda ayudar a crear la tuya! Hasta luegorrr!  

**A tope con @mentoringJS!  
Jordi Gomper.**