# Reto 2 - Creación de componentes

- Implementar a nuestra página web los distintos tipos de conexión de datos (binding)

## Objetivo

- Identificar que tipo de binding debemos utilizar según la necesidad.
- Aplicar one-way-binding y two-way-binding de manera adecuada.

## Desarrollo

Con base al Sitio Web de noticias previamente creado.

<ol>
<li>
Definir el título, autor, introducción, imágenes y concluciones desde la lógica de los componentes.
</li>
<br>
<li>
Dentro del componente de imágenes, añadir un botón que al presionarlo cambie la imagen mostrada.
</li>
<br>
<li>
Añadir un componente nuevo dentro del contenedor de la nota, este componente debe tener un campo de texto y un botón para enviar un comentario
    <ol>
    <li>
    Una vez se presione el botón enviar, el campo de texto debe ser borrado y el mensaje enviado debe aparecer debajo (para realizar esta actividad tienes que almacenar el comentario antes de que sea borrado por el botón enviar).
    </li>
    </ol>
</li>

</ol>

<details>
  <summary>Solución</summary>

### punto #1

Para definir el título, autor, introducción y conclusiones desde el componente debemos hacer uso de la interpolación en el componente correspondiente.

```html
<!--contenido dentro de titulo.component.html -->
<h1>{{titulo}}</h1>
<app-autor></app-autor>
```

```html
<!--contenido dentro de autor.component.html -->
<h3>{{autor}}</h3>
```

```html
<!--contenido dentro de introduccion.component.html -->
<p>{{introduccion}}</p>
```

```html
<!--contenido dentro de conclusiones.component.html -->
<h1>{{conclucion}}</h1>
```

Para definir la imagen debemos hacer uso de un enlace de propiedad

```html
<!--contenido dentro de imagenes.component.html -->
<img [src]="imagen" />
```

### Punto #2

Necesitamos añadir un botón con su evento `click` el cual ejecuta una función que cambie el valor del atributo `src`:

```html
<!--contenido dentro de imagenes.component.html -->
<img [src]="imagen" />

<button (click)="clickButon()">Siguinete Imagen</button>
```

```typescript
// componente imagenes.component.ts
import { Component } from "@angular/core";

@Component({
  selector: "app-imagenes",
  templateUrl: "./imagenes.component.html",
  styleUrls: ["./imagenes.component.scss"],
})
export class ImagenesComponent {
  imagen = "assets/img/logo.png";

  clickButon(): void {
    this.imagen = "assets/img/logo_2.png";
  }
}
```

### Punto #3

Necesitamos generar un nuevo componente, e incluir un Input que use `ngModel`, y un botón conectado a su evento `click`:

```console
ng g c nota/comentarios
```

```html
<!--contenido dentro de comentarios.component.html -->
<input [(ngModel)]="comentario" />

<button (click)="enviar()">enviar</button>
```

```typescript
// componente comentarios.component.ts
import { Component } from "@angular/core";

@Component({
  selector: "app-comentarios",
  templateUrl: "./comentarios.component.html",
  styleUrls: ["./comentarios.component.scss"],
})
export class ComentariosComponent {
  comentario = "";

  enviar() {
    this.comentario = "";
  }
}
```

### Punto 3.1

Necesitamos almacenar el valor de nuestro comentario antes de ser borrado, para eso hacemos uso de una nueva variable.

```html
<!--contenido dentro de comentarios.component.html -->
<input [(ngModel)]="comentario" />

<button (click)="enviar()">enviar</button>

{{ultimoMensaje}}
```

```typescript
// componente comentarios.component.ts
import { Component } from "@angular/core";

@Component({
  selector: "app-comentarios",
  templateUrl: "./comentarios.component.html",
  styleUrls: ["./comentarios.component.scss"],
})
export class ComentariosComponent {
  comentario = "";
  ultimoMensaje = "";

  enviar() {
    this.ultimoMensaje = this.comentario;
    this.comentario = "";
  }
}
```

> 💡 No olvides implementar el componente `app-comentarios` dentro del contendor de la nota.

</details>
