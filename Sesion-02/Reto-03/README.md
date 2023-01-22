# Reto 3 - Creación de directivas

- Haremos uso de las ventajas de desarrollo de templates que nos ofrece Angular.

## Objetivo

- Implementar directivas estructurales.
- Implementar directivas de atributo.

## Desarrollo

Con base al Sitio Web de noticias previamente creado.

<ol>
<li>
En el componente que creaste para mostrar el último comentario, si no existe un mensaje anterior, mostrar el mensaje : “Se el primero en compartir tus comentarios”.
</li>
<br>
<li>
En tu componente de Autor, ahora una nota tiene múltiples autores, por lo que tienes que crear una lista de nombres de autor en tu componente, y mostrarlos de la siguiente forma:

“Autor 1, Autor 2, Autor 3, Autor 4.”

</li>
<br>
<li>
Aplica a tus componentes las directivas ngClass y ngStyles a tu gusto
</li>
</ol>

<details>
  <summary>Solución</summary>

### punto #1

Añadiremos la directiva ngIf para validar si la variable `ultimoMensaje` almacena algún valor.

```html
<!--contenido dentro de comentarios.component.html -->
<input [(ngModel)]="comentario" />

<button (click)="enviar()">enviar</button>

<div *ngIf="ultimoMensaje">{{ultimoMensaje}}</div>

<div *ngIf="!ultimoMensaje">Se el primero en compartir tus comentarios</div>
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

### Punto #2

Al usar la directiva ngFor, podemos obtener el índice de cada elemento recorrido asignado el valor de índice a alguna variable de la siguiente forma: let **variable** = index

```
*ngFor="let autor of autores; let i = index"
```

Aplicandolo a nuestro componente:

```html
<!--contenido dentro de autor.component.html -->
<span *ngFor="let autor of autores; let i = index">
  {{autor}}{{ i < autores.length ? ',': '.' }}
</span>
```

```typescript
// componente autor.component.ts
import { Component } from "@angular/core";

@Component({
  selector: "app-autor",
  templateUrl: "./autor.component.html",
  styleUrls: ["./autor.component.scss"],
})
export class AutorComponent {
  autores = ["Autor 1", "Autor 2", "Autor 3", "Autor 4", "Autor 5"];
}
```

</details>
