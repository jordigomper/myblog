---
layout: post
title: Descomponiendo mi aplicación yogis
img: blog/i_comp.jpg
categories: app
---

Hola chic@s! En este articulo voy a descomponer mi app Yogis, intentando hacer todos los componentes re-utilizables.

[Aprende Javascript con MentoringJS - Step 11](http://mentoringjs.com/)

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

## React-router
Para la navegación por las diferentes páginas al seleccionar el menu he utilizado react-router. Es sencillo de utilizar, en una hora puedes aprender su funcionamiento y instalarlo en la aplicación. Voy a ir comentando las funciones a medida que salen.

## Descomponiendo la App
Descomponiendo la aplicación, he creado los siguientes componentes:

**Index.js**
Contiene el componente que contiene toda la aplicación y se encarga de insertarlo en la DOM. Se importan diferentes bibliotecas, react y react-dom  permiten utilizar componentes personalizados y insertarlos en la DOM, react-router-dom es el enrutador que nos ofrece react-router.  

**BrowserRouter** es un componente de react-router. Es el enrutador y debe usarse cuando la app maneja peticiones dinámicas, es decir, desde un navegador.  

```
import React from 'react';
import ReactDOM from 'react-dom';
import { BrowserRouter } from 'react-router-dom'
import App from './App';

ReactDOM.render(
    (
        <BrowserRouter>
            <App />
        </BrowserRouter>
    ), 
    document.getElementById('root')
);
```

**App.js**
Componente simple, llama a Header y Main. Es la página principal de la app. Mostrara el menú y el contenido.  

El componente Main hace de contenedor para cargar las diferentes secciones. Header es estático para toda la app.  

![Index yogis](https://jordigomper.github.io/myblog/img/a_mockup_yogis/index.PNG "Aplicación yogis")  

```
import React from 'react'
import Header from './Header.js'
import Main from './Main.js'

const App = () => (
    <div>
        <Header />
        <Main />
    </div>
)

export default App
```

**Header.js**
Componente simple que contiene el titulo y el menú de navegación.  

![Menú yogis](https://jordigomper.github.io/myblog/img/a_mockup_yogis/menu.PNG "Aplicación yogis")  

```
import React from 'react'
import Title from './Title.js'
import Nav from './Nav.js'

const Header = () => (
    <div>
        <Title />
        <Nav />
    </div>
)

export default Header
```

**Title.js**
Muestra el titulo de la aplicación. Hacer componentes pequeños como este da la opción de re-utilizarlo en cualquier parte del código, por ejemplo un banner.  

![Title yogis](https://jordigomper.github.io/myblog/img/a_desc_yogis/title.PNG "Aplicación yogis")  

```
import React from 'react'

const Title = () => (
    <h1>
        yogis!
    </h1>
)

export default Title
```

**Nav.js**
Contiene el menú de la aplicación. react-router-dom permite utilizar el componente Link para poder navegar por la aplicación. Dentro, se ha de indicar el la propiedad to="" el nombre del componente a insertar.  

![Menu yogis](https://jordigomper.github.io/myblog/img/a_desc_yogis/menu.PNG "Aplicación yogis")  

```
import React from 'react'
import { Link } from 'react-router-dom'

const Nav = () => (
    <header>
            <nav>
                <ul>
                    <li><Link to='/'>Principal</Link></li>
                    <li><Link to='/Articles'>Articulos</Link></li>      
                    <li><Link to='/Smoothies'>Batidos</Link></li>       
                    <li><Link to='/Challenges'>Retos</Link></li>        
                    <li><Link to='/MyAcount'>Mi cuenta</Link></li>          
                </ul>
            </nav>  
    </header>
)

export default Nav
```

**Main.js**
Muestra el contenido de toda la app. Router indica que los componentes Link deben de ser mostrados aquí. Es un componente de react-router.  

```
import React from 'react'
import { Switch, Route } from 'react-router-dom'
import Home from './Home'
import Articles from './Articles'
import Smoothies from './Smoothies'
import Challenges from './Challenges'
import MyAcount from './MyAcount'

const Main = () => (
    <main>
        <Switch>
            <Route exact path='/' component={Home} />
            <Route path='/Articles' component={Articles} />
            <Route path='/Smoothies' component={Smoothies} />
            <Route path='/Challenges' component={Challenges} />
            <Route path='/MyAcount' component={MyAcount} />
        </Switch>
    </main>
)

export default Main
```

**ArticleTemp.js**
Un componente plantilla para mostrar los diferentes artículos de la app. Desde props se envia toda la información. Tiene la característica que se puede modificar el ancho dependiendo del formato que quiero mostrar de la imagen.  

![ArticleTemps yogis](https://jordigomper.github.io/myblog/img/a_desc_yogis/articletemp.png "Aplicación yogis")  

```
import React, { Component } from 'react'

export default class ArticleTemp extends Component {
    render(){
        return(
            <div>
                <article >
                    <h3>{this.props.item.title}</h3>
                    <img src={require('./img/article/img1.PNG')} alt="" width={this.props.item.width}/>
                    <p>{this.props.item.desc}</p>
                </article>  
            </div>
        )
    }

}
```

**ListTemp.js**
Componente que utilizo de plantilla para mostrar las diferentes listas de la página. Sirve en modo de presentación, debe de mostrar un resumen de la descripción.  

En un futuro incluirá una función que mostrara el elemento seleccionado.  

![ListTemp yogis](https://jordigomper.github.io/myblog/img/a_desc_yogis/listtemp.png "Aplicación yogis")  

```
import React, { Component } from 'react'

export default class ListTemp extends Component {
    render(){
        const array = this.props.articles.map((item, index) => {
            return(
                    <li key={index}>
                        <img src={require('./img/article/img1.PNG')} alt="" width={item.width}/>
                        <h3>{item.title}</h3>
                        <p>{item.desc}</p>
                    </li>
            )})

        return(
            <ul>
                {array}
            </ul>
        )
    }   
}
```

**Home.js**
Es la página principal. Utiliza el componente ListTemp en modo de presentación de todos los artículos enviando la información por props.  

![Index yogis](https://jordigomper.github.io/myblog/img/a_mockup_yogis/index.PNG "Aplicación yogis")

```
import React, { Component } from 'react'
import ListTemp from './ListTemp.js'

export default class Home extends Component {
    render(){
        return(
            <div>
                <h3> PRINCIPAL </h3>
                <ListTemp articles={this.state.articles} />
            </div>
      )
    }
}
```

**Smoothies.js**
Utiliza el componente ListTemp para mostrar un resumen de todos los batidos.  

![Menú yogis](https://jordigomper.github.io/myblog/img/a_mockup_yogis/retos-calendario.PNG "Aplicación yogis")  

```
import React, { Component } from 'react'
import ListTemp from './ListTemp'

export default class Smoothies extends Component {
    render(){
        return(
            <div>
            <h3> BATIDOS </h3>
              <ListTemp articles={this.state.smoothies} />
          </div>
      )
    }
}
```

**Challenges.js**
Esta seccion contiene tres secciones. Utiliza el mismo sistema que App. Contiene un sub-menú y un contenedor donde mostrara el contenido.  

![Menú yogis](https://jordigomper.github.io/myblog/img/a_mockup_yogis/retos-principal2.PNG "Aplicación yogis")  

```
import React from 'react'
import SubNav from './SubNav.js'
import MainChallenge from './MainChallenge.js'

const Challenges = () => (
    <div>
        <SubNav />
        <MainChallenge />
    </div>
)

export default Challenges
```

**SubNav.js**
Contiene las tres partes de retos mosrtandolos en el menú. Utiliza react-router.  

![Menú yogis](https://jordigomper.github.io/myblog/img/a_mockup_yogis/retos-principal.PNG "Aplicación yogis")  

```
import React from 'react'
import { Link } from 'react-router-dom'

const SubNav = () => (
    <header>
            <nav>
                <ul>
                    <li><Link to='/Challenges/'>Reto</Link></li>
                    <li><Link to='/Challenges/ChallengeDay'>Reto del dia</Link></li>        
                    <li><Link to='/Challenges/CalendarChallenger'>Calendario</Link></li>            
                </ul>
            </nav>  
    </header>
)

export default SubNav
```

**MainChallenge.js**
Componente que utiliza react-router como contenedor para mostrar las diferentes secciones de Challenges.js.  

![ButtonTemp yogis](https://jordigomper.github.io/myblog/img/a_desc_yogis/buttontemp.png "Aplicación yogis")  

```
import React from 'react'
import { Switch, Route } from 'react-router-dom'
import Challenge from './Challenge'
import ChallengeDay from './ChallengeDay'
import CalendarChallenger from './CalendarChallenger'

const MainChallenge = () => (
    <main>
        <Switch>
            <Route exact path='/Challenges/' component={Challenge} />
            <Route path='/Challenges/ChallengeDay' component={ChallengeDay} />
            <Route path='/Challenges/CalendarChallenger' component={CalendarChallenger} />
        </Switch>
    </main>
)

export default MainChallenge
```

**ForumTemp.js**
Componente que contiene un muro tipo Facebook. Mostrara el contenido dependiendo de la sección donde se encuentre.  

![Menú yogis](https://jordigomper.github.io/myblog/img/a_mockup_yogis/retos-principal3.PNG "Aplicación yogis")  

```
import React, { Component } from 'react'

export default class ForumTemp extends Component {
    render(){
        return(
            <div>
                <div>
                    <img src={require('./img/article/muro.PNG')} alt="" />
                </div>
                <form>
                    <input type="placeholder" value="Introduce tu comentario..." />
                    <input type="submit" value="Enviar"/>
                </form>
            </div>
        )
    }
}
```

**Challenge.js**
Este componente se muestra por defecto cuando se selecciona Retos. Contiene la información del reto utilizando ArticleTemp para mostrarlo, un botón para unirse al reto y un muro desde el componente FroumTemp donde los usuarios pueden exponer sus dudas.  

![Menú yogis](https://jordigomper.github.io/myblog/img/a_mockup_yogis/retos-principal2.PNG "Aplicación yogis")

![Menú yogis](https://jordigomper.github.io/myblog/img/a_mockup_yogis/retos-principal3.PNG "Aplicación yogis")  

```
import React, { Component } from 'react'
import ArticleTemp from './ArticleTemp.js'
import ForumTemp from './ForumTemp.js'

export default class Challenge extends Component {
    render(){
        return(
            <div>
                <h3> RETO </h3>
                <ArticleTemp item={this.state.challenge} />
                <button>Unirse al reto</button>  
                <ForumTemp />
          </div>
      )
    }
}
```

**ChallengeDay.js**
Igual que Challenge.js con la diferencia que mostrara el reto del dia.  

![Menú yogis](https://jordigomper.github.io/myblog/img/a_mockup_yogis/retos-dia.PNG "Aplicación yogis")

![Menú yogis](https://jordigomper.github.io/myblog/img/a_mockup_yogis/retos-dia2.PNG "Aplicación yogis")  

```
import React, { Component } from 'react'
import ArticleTemp from './ArticleTemp.js'
import ForumTemp from './ForumTemp.js'

export default class ChallengeDay extends Component {
    render(){
        return(
            <div>
                <h3> RETO DEL DIA </h3>
                <ArticleTemp item={this.state.challenge} />
                <button>Reto conseguido!</button>  
                <ForumTemp />
            </div>
      )
    }
}
```

**CalendarChallenger.js**
Utilizando ListTemp, muestra los batidos de los días de reto.  

![Menú yogis](https://jordigomper.github.io/myblog/img/a_mockup_yogis/retos-calendario.PNG "Aplicación yogis")  

```
import React, { Component } from 'react'
import ListTemp from './ListTemp'

export default class CalendarChallenger extends Component {
    render(){
        return(
            <div>
                <h3> CALENDARIO DEL RETO </h3>
                <ListTemp articles={this.state.smoothies} />
          </div>
      )
    }
}
```

Step by step mi aplicación va cogiendo forma, espero que te pueda ayudar a crear la tuya! Hasta luegorrr!  

**A tope con @mentoringJS!  
Jordi Gomper.**