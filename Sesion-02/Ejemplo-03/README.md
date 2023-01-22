# Ejemplo 1 - Uso de directivas.


## Objetivo

* Identificar en qué situaciones debemos aplicar directivas.
* Uso de ngIf y ngFor en templates.

## Desarrollo

### Directivas estructurales

Usamos la directiva ngIf para ocultar o mostrar elementos HTML o componentes declarados por medio de tu selector y haciendo una de una condición true false. El elemento que contiene la directiva y todos sus elementos anidados (hijos) también aplican la directiva.


```html
<app-header *ngIf="mostrarHeader"></app-header>

<Section *ngIf="mostrar">
    <h1>Ejemplo de ngIf </h1>
    <div>
        información
    </div>
</Section>

<app-footer *ngIf="10%2 === 0"></app-footer>

```

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.scss']
})

export class AppComponent {

  mostrar = false;
  mostrarHeader = false;

}
```

La directiva ngFor nos nos permite recorrer un arreglo de elementos y generar una vista para cada uno de Ellos. Nos es muy util para mostrar una lista de datos o para mostrar en una tabla o menu.

```html
  <ul>
    <li *ngFor="let elemento of elementos">
        <p>{{ elemento }}</p>
    </li>
  </ul>
```

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.scss']
})

export class AppComponent {
  elementos = ['elemento 1', 'elemento 2', 'elemento 3'];
}
```

Es importante resaltar que un elemento __no__ puede aplicar más de una directiva de tipo estructural. Sin embargo podemos aplicar una anidación de elementos con directivas.

```html
  <ul *ngIf="elementos !== null">
    <li *ngFor="let elemento of elementos">
        <p>{{ elemento }}</p>
    </li>
  </ul>
```

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.scss']
})

export class AppComponent {
  elementos = ['elemento 1', 'elemento 2', 'elemento 3'];
}
```

### Directivas de atributo

La directiva ngClass nos sirve para aplicar una o varias clases de CSS a un mismo elemento en función a las condiciones lógicas establecidas.

```html
<div [ngClass]="{'class1': condicion1, 'class2': condicion2}"></div>

```

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.scss']
})

export class AppComponent {
  condition1 = true;
  condition2 = false;
}
```

La directiva ngStyle la utilizamos para aplicar estilos CSS a un elemento HTML, es similar a ngClass pero en lugar de aplicar clases de css, aplicamos estilos.

```html
<input [(ngModel)]="nombre" type="text">
```

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.scss']
})

export class AppComponent {
  nombre = 'BEDU';
}
```
