---
layout: post
title: Creando una galeria de imagenes
img: blog/i_gallery.PNG
categories: app
---

Hola chi@S! Hoy traigo los pasos para crear una galería de imágenes con React.js, va a quedar chulissima en vuestras aplicaciones.

[Aprende Javascript con MentoringJS - Step 12](http://mentoringjs.com/)  

Puedes descargar la galería desde [aquí](https://github.com/jordigomper/image_gallery_React).  

![galeria con react.js]( https://jordigomper.github.io/myblog/img/gif/galeria_imagenes.gif)  

Para crear la galería vamos a utilizar [bootstrap 3](http://getbootstrap.com/) para su diseño responsive en diferentes navegadores, [font awesome](http://fontawesome.io/) para los iconos y [normalize](http://necolas.github.io/normalize.css/?lipi=urn%3Ali%3Apage%3Ad_flagship3_pulse_read%3BloKgz4hXQWGzOHMvH40r6w%3D%3D) para que el css cumpla con un standar del css. Al lio!  


Desde la herramienta **create-react-app** creamos nuestro nuevo proyecto.  

Descargamos font awesome y lo instalamos dentro de la carpeta src.  

En la carpeta public hay que modificar el archivo Index.html para incorporar las llamadas a las librerias de bootstrap, normalize y font awesome y a los archivos JS. Creamos una sección con la clase gallery-container que va a contener la galería.  

```
<!DOCTYPE html>
<html >
  <head>
    <meta charset="UTF-8">
    <title>Galeria multimedia con React.js</title>
    <meta name="viewport" content="width=device-width, initial-scale=1">

    <!-- Normalize stylesheet -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/normalize/5.0.0/normalize.min.css">

    <!-- Bootstrap 3 -->
    <link rel='stylesheet' href='https://cdnjs.cloudflare.com/ajax/libs/twitter-bootstrap/3.3.7/css/bootstrap.min.css'>

    <!-- Font Libre Franklin -->
     <link rel="stylesheet" href="../src/css/font-awesome.css">

    <!-- Main stylesheet-->
    <link rel="stylesheet" href="../src/css/index.css">
  </head>

  <body>
  <h1>Galeria sencilla con React.js</h1>
    <div id="root">
      <section class="gallery-container" ></section>
    </div>
    <footer>
      <a href="https://jordigomper.github.io/myblog/">Jordi Gomper</a>
    </footer>

    <!-- Scripts -->
    <script src='https://cdnjs.cloudflare.com/ajax/libs/react/15.3.1/react.min.js'></script>

    <script src='https://cdnjs.cloudflare.com/ajax/libs/react/15.3.1/react-dom.min.js'></script>

    <script src="../src/index.js"></script>
  </body>
</html>

```

Ahora el código y el funcionamiento interno de la galería. Esta creada con React.js y utiliza tres componentes:  

* **Gallery.js:** Contiene toda la aplicación y llama a los diferentes componentes. Utiliza boostrap para darle forma a la estructura.
* **GalleryImage.js:** Es llamado desde Gallery.js por cada url que incorpora la array imgUrls y devuelve las imágenes en miniatura que hay en la galería.  Utiliza la url pasada desde props para mostrar la imagen. No utiliza state, ya que no hace falta volver a renderizar una vez creada.
* **GalleryModal:** Llamado desde Gallery.js y incorporado fuera del contenedor donde se imprimen las imágenes. Devuelve una imagen ampliada cuando hacemos click sobre una miniatura. Este componente funciona de una forma especial a todo los que he utilizado hasta ahora. Es incorporado en la DOM en la primera carga de la aplicación pero no se muestra hasta que no hacemos click en una imagen. Contiene un ciclo de vida y state para permitir el cambio de imagen.  

Ahora voy a mostraros los componentes uno a uno y voy a explicar el funcionamiento de cada uno.  

Voy a centrarme en el funcionamiento, todo el estilo que utilizo de boostrap y css no voy a comentarlo para no complicar la explicación de su funcionamiento que es lo importante, el estilo puede ir a gusto de cada uno.  

## Gallery.js
```
import React, { Component } from 'react'
import GalleryImage from "./GalleryImage.js"
import GalleryModal from "./GalleryModal.js"

export default class Gallery extends Component {
    constructor(props) {
        super(props)

        this.state = {
            showModal: false,
            url: ''
        }
    }

    render() {
        return(
            <div refs="gallery-container" className="container-fluid gallery-container" >
                <div className="row" >
                    {
                        this.props.imgUrls.map((url, index) => {
                            return( 
                                <div className="col-sm-6 col-md-3 col-xl-2" >
                                    <div className="gallery-card" >
                                        <GalleryImage className="gallery-thumbnail" src={url} alt={'Img number' + (index + 1)} key={index} />
                                        <span className="card-icon-open fa fa-expand" onClick={e => this.openModal(url)} />
                                    </div>      
                                </div>
                            )           
                        })
                    }
                </div>
                <GalleryModal isOpen={this.state.showModal} src={this.state.url} closeModal={this.closeModal} imgUrls={this.props.imgUrls} />
            </div>
        )
    }

    openModal = (url) => {
        this.setState({
            showModal: true,
            url: url
        })
    }

    closeModal = () => {
        this.setState({
            showModal: false,
            url: ''
        })
    }
}
```

Importo los diferentes métodos, hojas de estilo y componentes utilizados.  

Dentro del componente encontramos un constructor. Cada vez que se **inicie por primera vez**, va a dar el estado de showModal como false y url no la define.  

```
constructor(props) {
super(props)

this.state = {
    showModal: false,
    url: ''
}
```

Aquí encontramos la primera particularidad. Mientras que showModal tenga el valor de false, **no va a mostrar en el navegador** el componente GalleryModal ya que este componente solo se tiene que visualizar cuando se hace click sobre una imagen. Más adelante, dentro del componente GalleryModal veremos como.  

Dentro de render, devolvemos diferentes elementos div que hacen de contenedor para las imágenes en miniatura. Cada imagen ira envuelta en otro div para tener un contenedor personal, esto sirve a la hora de posicionar el icono de ampliar.  

Llamo al array que contiene todas las urls de las imágenes con el componente **GalleryImage**. Paso por props la url de la imagen y justo debajo desde un span se coloca la llamada al icono de expandir y un gestor de eventos. Este gestor de eventos pasa por referencia la función **OpenModal**, que se encarga de cambiar el estado de showModal por true y url por el valor de la imagen seleccionada, mostrándola desde el componente **GalleryModal** que ya se muestra por el navegador.

```
// llamada al componente y span con el icono
<GalleryImage className="gallery-thumbnail" src={url} alt={'Img number' + (index + 1)} key={index} />
<span className="card-icon-open fa fa-expand" onClick={e => this.openModal(url)} />
```

```
openModal = (url) => {
    this.setState({
        showModal: true,
        url: url
    })
}
```

Fuera del contenedor de la galería se encuentra el componente **GalleryModal**. A este componente le envío por props el valor del estado de showModal y url, permitiendo la renderización y mostrando la imagen desde el url que le envío.  

También incluye por referencia la función **closeModal** que se incorporara al icono de cerrar de la imagen ampliada y que al pulsar cambiara el estado del componente Gallery por showModal false y url indefinida **volviendo a evitar que el componente se visualice** por el navegador.  

```
closeModal = () => {
        this.setState({
            showModal: false,
            url: ''
        })
    }
```

## GalleryImage
```
import React, { Component } from 'react'

export default class GalleryImage extends Component {
    render() {
        return(
            <img className={this.props.className} alt={this.props.alt} src={this.props.src}  />
        )
    }
}
```

Un componente contenedor. Devuelve la imagen con la url que paso por props. Como dato también heredera className para darle estilo con boostrap.  

## GalleryModal
```
import React, { Component } from 'react'

export default class GalleryModal extends Component {
    constructor(props) {
        super(props)

        this.state = {
            src: ''
        }
    }

    componentWillReceiveProps(nextProps){
        if(nextProps.src !== '') {
            this.setState({
                src: nextProps.src
            })
        }
    }

    render() {
        if(this.props.isOpen === false) {
            return null
        }

        return(
            <div className="modal-overlay" >
                <div className="modal-body" >
                    <a className="modal-close" href='#' onClick={this.props.closeModal} >
                        <span className='fa fa-times' />
                    </a>
                    <img src={this.state.src} alt="" />
                </div>
                <a className='card-arrow-left' href='#' onClick={() => this.changeImage(this.props.imgUrls[this.props.imgUrls.indexOf(this.state.src)-1])} >
                    <span className='fa fa-arrow-left' />
                </a>

                <a className='card-arrow-right' href='#' onClick={() => this.changeImage(this.props.imgUrls[this.props.imgUrls.indexOf(this.state.src)+1])} >
                    <span className='fa fa-arrow-right' />
                </a>
            </div>
        )
    }

    changeImage = (url) => {
        if(url !== undefined){
            this.setState({
                src: url
            })
        }
    }
}
```

Aquí el componente más peculiar de la aplicación. Vamos a ver el ciclo de vida, ya que al ser renderizado desde la primera ejecución de la aplicación es un poco característico.  

Este componente necesita tener estado para cambiar de imagen sin tener que renderizar toda la aplicación. Primero he creado un constructor donde inicia la variable src en indefinida.  

Pasamos a **componentWillReceiveProps()**. Este método **solo se ejecuta cuando detecta que algún props recibido desde el componente padre a cambiado**. Si no contiene este ciclo de vida, al pulsar una imagen mostraría el componente vacío ya que no se ha vuelto a renderizar y no asignaría la nueva url en el estado. Así que cuando detecta un cambio de props se ejecuta.  

El problema que tiene este método, es que **si utilizo this.setState dentro de el directamente sin ninguna condición, entra en bucle permanente**. Como siempre que se muestre por pantalla va a tener una url de la imagen seleccionada, con una condición if evito que entre entre en bucle, ya que una vez asignada la url al estado src, no puede entrar más.  

```
componentWillReceiveProps(nextProps){
    if(nextProps.src !== '') {
        this.setState({
            src: nextProps.src
        })
    }
}
```

Dentro del render, incluyo una condición, si props.isOpen es false, devuelvo null evitando que renderize el componente y se muestre en el navegador. De esta forma tan simple, podemos tener un componente renderizado y oculto a la vista. Cuando props.isOpen es true devuelve el componente.  

```
if(this.props.isOpen === false) {
    return null
}
```

Dentro, un contenedor div para todos los elementos. Esto sirve para poder posicionar los diferentes iconos sobre la imagen.  

El icono de cerrar incorpora la función pasada por referencia **closeModal** para cerrar la imagen.  

Los elementos span con className='card-arrow-...' contienen los iconos de flechas para desplazarnos por las diferentes imágenes sin la necesidad de tener que volver a la galería. Incorporan la función **changeImage**, antes de comentar la función vamos a ver como paso la url de la imagen posicionada en la dirección de la flecha seleccionada.  

Dentro de los parámetros que le envío a la función se encuentra lo siguiente:

```
this.props.imgUrls[this.props.imgUrls.indexOf(this.state.src)+1/-1])
```

Lo que consigo con esto es desde el método de JS **indexOf busco el indice que ocupa la url actual** y dependiendo la flecha seleccionada sumo o resto una posición. Esto genera un numero con la posición deseada y envía al método la url en el interior de imgUrls con la posición indicada.  

Dentro del método **changeImage**, lo primero que hago es comprobar que el valor recibido no es undefined. Cuando pasamos el primer elemento de la array en dirección contraria, es decir, a la izquierda o cuando pasamos las posiciones totales del array, **enviamos una url undefinied** y no muestra ninguna imagen. Esto evita que pase eso, parando la imagen siempre en la primera y ultima posición.  

Si la condición se cumple, se actualiza el estado con la nueva url pasada, renderizando el componente y mostrando la nueva imagen por pantalla.  

```
changeImage = (url) => {
    if(url !== undefined){
        this.setState({
            src: url
        })
    }
}
```

Después de crear la galería, he creado una versión estática y la he subido a surge con las ultimas aventuras que he vivido con mis amigos, lo siguiente, se las he enseñado, han flipado!  

Puedes ver el resultado en el siguiente [link](http://jgomper-gallery.surge.sh/). Si todavía no has leído mi articulo de como subir tu aplicación en surge, aquí te dejo el [link](2017-9-11-Deployar-con-Surge.md).

Hasta aquí este articulo. Ya tienes los conocimientos básicos para crear una galería y dejar boquiabiertos a todos tus amigos subiendo las fotos del ultimo verano, a que esperas?

**A tope con @mentoringJS!  
Jordi Gomper.**