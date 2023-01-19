# Reto 1 - Creación de componentes
* Crear una página web haciendo uso de los componentes Angular.
## Objetivo

* Crea al menos 3 componentes Angular.
* Crear una relacion padre hijo entre componentes.
* Implementar los ciclos de vida dentro de los componentes.

## Desarrollo

Se requiere crear un sitio web de noticias que posea la siguiente estructura:

* Header del sitio web.
* Cuerpo del sitio web.
  * Título de la noticia.
    * Autor de la nota.
  * Contenedor de la nota.
    * Introducción A la nota.
    * Imágenes relacionadas con la nota.
    * Conclusión de la nota.
* Footer del sitio web.

Toda la información dentro web puede ser estática y haciendo uso de elementos HTML como lo son h, p, div, img etc…

Se debe hacer eso de los componentes para cada sección de la página y nota, al igual que implementar componentes dentro de otros componentes.

<details>
  <summary>Solución</summary>

  Debemos hacer uso de CLI para la creación de nuestros componentes.

  Componentes principales de la web:
  ```console
  ng g c estructura-web/header
  
  ng g c estructura-web/body
  
  ng g c estructura-web/footer
  ```
  Componentes del la nota:

  ```console
  ng g c nota/titulo

  ng g c nota/autor
  
  ng g c nota/contenedor-nota

  ng g c nota/cuerpo/introduccion

  ng g c nota/cuerpo/imagenes

  ng g c nota/cuerpo/conclusiones
  ```
  <br>

Añadiremos la estructura de la web al componente principal `app.component`

```html
<!--contenido dentro de app.component.html -->
<app-header></app-header>
<app-body></app-body>
<app-footer></app-footer>
```
Ahora añadiremos a nuestro componente de body, el título y el contenedor de la nota.

```html
<!--contenido dentro de body.component.html -->
<app-titulo></app-titulo>
<app-contenedor-nota></app-contenedor-nota>
```
Ahora tenemos que asignar un título a nuestra nota, y añadir el componente de autor.

```html
<!--contenido dentro de titulo.component.html -->
<h1>Título de la nota</h1>
<app-autor></app-autor>
```

Ya tenemos completada la sección de título, ahora solo nos falta añadir los componentes introducción, imagenes y conclusiones al contenedor de la nota.

```html
<!--contenido dentro de contenedor-nota.component.html -->
<app-introduccion></app-introduccion>
<app-imagenes></app-imagenes>
<app-conclusiones></app-conclusiones>
```

Una vez creada la estructura de la web solo tenemos que añadir las implementaciones a las etapas del ciclo de vida que deseemos usar.


</details> 