---
layout: post
title: Descomponiendo mi aplicación yogis
img: blog/i_app.jpg
categories: app
---

Hola chicos! En este articulo voy a descomponer mi app Yogis, intentando hacer todos los componentes re-utilizables.

## Introducción
Voy a repasar las secciones principales de mi aplicación:

**Index:** Muestra todos los artículos y videos sobre posturas, batidos. Mostrara la imagen en grande con el titulo y un breve resumen del inicio de cada articulo.

**Artículos:** Al pulsar un artículo desde Index, nos lo muestra. Un artículo puede contener varias imágenes.

**Batidos:** Muestra una lista con las imágenes en miniatura de los batidos y una breve descripción. Al pulsar sobre el batido nos envía a la página de ese batido.

**Retos:** Esta sección muestra la descripción de un reto que está activo. Primero contiene un sub-menú con las opciones Reto principal, reto del día y calendario. Al pulsar retos en el menú principal nos envía a la página retos principal por defecto.

**Retos principal:** Cuando el usuario no se ha unido en el reto, muestra un botón en rojo "Unirse al reto". Después de este botón, se muestra una explicación de que consiste el reto y la lista de las cosas que necesitamos, contendrá un video explicativo. Por ultimo, contiene un muro donde los usuarios pueden preguntar las diferentes dudas que tengan.

**Reto del dia:** Muestra la información del reto del día, por ejemplo tiene que mostrar que batido y como hacerlo o un video explicándolo. Debajo de esta explicación un botón "reto conseguido" que abre la cámara del teléfono donde el usuario debe hacer una foto. Esta foto se enviara automáticamente al muro que hay debajo del botón. Este muro solo muestra las fotos de los diferentes usuarios.

**Calendario:** Muestra una lista con las imágenes en miniatura y descripciones de los diferentes batidos que forman el reto. Cada batido mostrara el orden del día.

**Usuario**: Muestra las diferentes opciones de un usuario. Cada usuario puede modificar diferente información y notificaciones.

La aplicación contiene un menú principal y un sub-menú para las secciones que se encuentran en retos.

## Descomponiendo la App
Descomponiendo la aplicación, he creado los siguientes componentes:

### Componentes lógicos
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
Es una plantilla para mostrar los artículos o descripciones en cualquier zona de la app. A través de props mandamos la información que compone el articulo, pudiendo mostrar los artículos, batidos, descripciones de retos...

**List:**  
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
Recibe un array de objetos y crea una lista con la imagen en miniatura y una breve descripción. Al pulsar envía al articulo.

**Forum:**
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
Desde props enviamos la información del muro, luego lo muestra dependiendo en que sección se encuentre.

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
import Challenge from './Challenge.js'
import ChallengeDay from './ChallengeDay.js'
import ChallengerSmoothies from './ChallengerSmoothies.js'
import ChallengesIndex from './ChallengesIndex.js'
import Smoothies from './Smoothies.js'

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
Contiene **Header** y un elemento div con la id="display" donde se mostraran las diferentes secciones de la app. Se importan los diferentes componentes de la aplicación.  

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

**Article:** 
```
import React, { Component } from 'react'
import { render } from 'react-dom'
import List from './ArticleTemp.js'

export default class Article extends Component {

    render(){
        return(
            <div>
                <ArticleTemp />
            </div>
        )
    }   
}
```
Este componente es la sección que muestra un resumen de todos los artículos y videos. Utiliza la plantilla


**Smoothies:**
```
import React, { Component } from 'react'
import { render } from 'react-dom'
import List from './List.js'

export default class Smoothies extends Component {

    render(){
        return(
            <div>
                <List />
            </div>
        )
    }   
}
```
Contiene el componente List que le enviamos el array de todos los batidos.

**ChallengesIndex:**  
```
import React, { Component } from 'react'
import { render } from 'react-dom'
import SubNav from './SubNav.js'

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
Por defecto muestra el componente Challenge dentro del elemento div. Contiene el sub-menú para esta sección.

**Challenge:**
```
import React, { Component } from 'react'
import { render } from 'react-dom'
import Article from './Article.js'
import Forum from './Forum.js'

export default class ChallengeDay extends Component {
    render(){
        return(
            <div>
                <ArticleTemp />
                <button>Conseguido!</button>
                <Forum />
            </div>
        )
    }
}
```
Aprobecha el componente ArticleTemp para imprimir la información de todo el reto. Un muro con el componente Forum donde los usuarios pueden escribir sus dudas.

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

**ChallengeDay:**
```
import React, { Component } from 'react'
import { render } from 'react-dom'
import Article from './Article.js'
import Forum from './Forum.js'

export default class ChallengeDay extends Component {
    render(){
        return(
            <div>
                <ArticleTemp />
                <button>Conseguido!</button>
                <Forum />
            </div>
        )
    }
}
```
Es el reto del día. Utiliza la plantilla ArticleTemp para mostrar la descripción y el componente Forum donde se suben las fotos de los usuarios.

**ChallengeSmoothies:**
```
import React, { Component } from 'react'
import { render } from 'react-dom'
import List from './List.js'

export default class ChallengerSmoothies extends Component {

    render(){
        return(
            <div>
                <List />
            </div>
        )
    }   
}
```
Envia al complemento List un array de objetos donde imprime los batidos del reto.
