# Ejemplo 03 - Navegación entre rutas desde la aplicación.
## Objetivo

* Conocer la forma en la que Angular nos permite navegar entre rutas.
* Navegación desde templates.

## Desarrollo


Angular nos ofrece la directiva routerLink para las etiquetas \<a> o \<buton> las cuales nos permite navegar entre rutas existentes.

```html
<a [routerLink]="['login']">LOGIN</a>

<button [routerLink]="['login']">LOGIN</button>
```

Cuando el usuario pulse la etiqueta, la aplicación navegará a la ruta especificada sustituyendo el componente actual por el componente asociado a la nueva ruta.


Si deseamos usar rutas con parámetros para recibir alguna información al navegar entre rutas como lo puede ser un id, los podemos añadir al configurar nuestras rutas.

```typescript
// carrito-routing.module.ts
const routes: Routes = [
  {path: 'detalle-producto/:id', component: DetalleProductoComponent}
];
```
Para enviar el parametro id desde la directiva routerLink lo hacemos de la siguiente forma:

```html
<!-- app.component.html -->
<a [routerLink]="['detalle-producto',  id ]">Detalle del producto</a>

<button [routerLink]="['detalle-producto', id]">Detalle del producto</button>
```

```typescript
// app.component.ts

export class AppComponent {
  id = '01';
}
```
Al arreglo que asigna el valor a la directiva, el primer ítem es la ruta a la que deseamos acceder y el segundo ítem es el valor del parámetro, en este caso lo tomamos desde nuestro component.ts, pero también puede ser un valor del objeto recibido por la directiva ngfor.