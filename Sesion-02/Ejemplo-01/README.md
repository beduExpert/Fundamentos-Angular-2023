# Ejemplo 1 - Creación de componentes.


## Objetivo

* Identificar la estrucura de un componente de Angular.
* Crear multiples componentes con CLI.
* Añdir nuestros componentes a la Vista.

## Desarrollo

Para la creación de componentes haremos uso de CLI con el siguiente comando:

```console
ng generate componente <ruta-componente/nombre-componente>
```

Dentro del comando identificamos la siguiente sintaxis:

__ng__: comando para el uso de Angular CLI

__generate__: hace referencia a la creación de nuevos archivos, se puede abreviar con una __g__

__component__: hace referencia a un componente, en este caso para su creacion, se puede abreviar con __c__

```console
ng g c componentes/contenedor-formulario
```

Una vez creado nuestro componente debemos hacer uso de su selector declarando nuestro componente dentro del componente principal de la aplicacion __app.component__

> 💡 Recuerda borrar todo el contenido previamente autogenerado por Angular en el archivo app.component.ts 

```html
<!--contenido dentro de app.component.html -->
<app-contenedor-formulario></app-contenedor-formulario>
```
Podemos implementar varias veces el mismo componente.

```html
<!-- contenido dentro de app.component.html -->
<p>Formulario 1</p>
<app-contenedor-formulario></app-contenedor-formulario>

<p>Formulario 2</p>
<app-contenedor-formulario></app-contenedor-formulario>

<p>Formulario 3</p>
<app-contenedor-formulario></app-contenedor-formulario>
```
Puedes ver tus cambios dentro de [http://localhost:4200](http://localhost:4200/), siempre y cuando tengas levantado tu servidor con el comando __ng serve__.


> 💡 Siempre revisa tu consola para identificar si existe algún error de compilación.


### Componentes dentro de componentes

Ahora crearemos un nuevo componente:

```console
ng g c componentes/input-string
```

Identificamos nuestro selector, en este caso: __app-input-string__

```typescript

import { Component } from '@angular/core';

@Component({
  selector: 'app-input-string',
  templateUrl: './input-string.component.html',
  styleUrls: ['./input-string.component.scss']
})
export class InputStringComponent {

}
```

Ahora implementaremos nuestro nuevo componente, pero esta vez dentro de nuestro componente contenedor-formulario previamente creado.

```html
<!--contenido dentro de contenedor-formulario.component.html-->
<app-input-string></app-input-string>
```

Ahora cada componente contenedor-formulario posee dentro su propio componente input-string. Recuerda que aunque sean el mismo componente, cada uno posee su propio estado y ciclo de vida.

### Ciclo de vida de un componente


Como vimos previamente, todos los componentes poseen su propio ciclo de vida, veamos como implementar la etapa onInit en nuestro componente contenedor-formulario.

```typescript

import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'app-contenedor-formulario',
  templateUrl: './contenedor-formulario.component.html',
  styleUrls: ['./contenedor-formulario.component.scss']
})
export class ContenedorFormularioComponent implements OnInit{

  ngOnInit(): void {
    console.log('ngOnInit');
  }

}
```
Nuestro método implementado ngOnInit será llamado automáticamente al momento de inicializar el componente, si revisamos nuestra consola una vez nuestra aplicación ha cargado los cambios, notaremos que tenemos el mensaje “ngOnInit” aparece 3 veces, esto sucede porque nosotros hemos renderizado este componente 3 veces en la misma página. De esta manera nos damos cuenta que cada componente tiene su propio ciclo de vida.


Cada etapa de vida implementa diferentes funciones dentro de nuestra clase componente, si deseamos añadir la etapa: “AfterViewInit”, debemos añadirla a nuestras implementaciones de clase junto con su método a implementar.

```typescript
import { AfterViewInit, Component, OnInit } from '@angular/core';

@Component({
  selector: 'app-contenedor-formulario',
  templateUrl: './contenedor-formulario.component.html',
  styleUrls: ['./contenedor-formulario.component.scss']
})
export class ContenedorFormularioComponent implements OnInit , AfterViewInit{
  ngAfterViewInit(): void {
    throw new Error('Method not implemented.');
  }

  ngOnInit(): void {
    console.log('ngOnInit');
  }

}

```

> 💡 Con el uso de extensiones dentro de VSCode logramos que el editor de código nos ayude autocompletando nombres de clases, importación automática o implementación de métodos entre muchas otras funciones. Una de las más recomendadas es __Angular Language Service__.
> 