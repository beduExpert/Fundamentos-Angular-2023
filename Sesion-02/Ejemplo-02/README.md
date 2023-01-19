# Ejemplo 2 - Angular Binding

## Objetivo

* Identificar en qué situaciones es necesaria la conexión de datos con la vista.
* Uso del one way binding.
* Uso del two way binding.



## Desarrollo

A Continuación veremos los tipos de comunicación entre vista y componente que nos ofrece Angular.

### Interpolación
Si nuestro objetivo es implementar mostrar el valor de una variable en nuestra vista, y su cambio a lo largo del ciclo de vida del componente hacemos uso de la interpolación.

Mostrando una variable en la vista:
```typescript
// componente app.component.ts
@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.scss']
})

export class AppComponent {
    mensaje = 'Hola BEDU';
}
```
Uso de interpolación en template:
```html
<!--contenido dentro de app.component.html-->
{{mensaje}}
```

Mostrando el resultado de una operación en la vista:
```typescript
// componente app.component.ts
@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.scss']
})

export class AppComponent {
    altura = 20;
    base = 10;
}
```
Uso de interpolación en template:
```html
<!--contenido dentro de app.component.html-->
El área es: {{base * altura}}
```

Mostrando el resultado de una validación en la vista:
```typescript
// componente app.component.ts
@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.scss']
})

export class AppComponent {
    mayorDeEdad = true;
}
```
Uso de interpolación en template:
```html
<!--contenido dentro de app.component.html-->
El usuario es: {{ mayorDeEdad ? 'mayor de edad': 'Menor de edad'  }}
```

### Enlace de propiedad.

Las ocupamos para vincular alguna propiedad de elementos a nuestra lógica dentro del componente, es importante mencionar que esta comunicación es unidireccional , es decir que solo el componente puede mantener actualizando los datos.

Uso en elementos:

```typescript
// componente app.component.ts
@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.scss']
})

export class AppComponent {
    srcImg = 'assets/img/logo.png';
    altImg = 'logo institucional';


}
```

```html
<!--contenido dentro de app.component.html-->

<img [src]="srcImg" [alt]="altImg">

```

### Enlaces de eventos.

Podemos capturar los eventos de la vista y ejecutar una función para actuar en respuesta, por ejemplo realizar una acción después de que el usuario pulsa un botón, o eventos de un input como lo son: onkeypress, onkeydown, onkeyup.

```html
<!--contenido dentro de app.component.html-->
<button (click)="clickButon()">Click me</button>
```

```typescript
// componente app.component.ts
@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.scss']
})

export class AppComponent {
    clickButon(): void {
        console.log('El usuario ha presionado el botón');
    }
}
```
Los eventos generalmente regresan un objeto como respuesta, para hacer eso de ellos usamos la sintaxis `$event` la cual nuestra función de implementación recibe como parámetro:

Ejemplo en acciones dentro de un input:

```html
<!--contenido dentro de app.component.html-->
<input (keydown)="keydown($event)" 
       (keypress)="keypress($event)"
       (keyup)="keyup($event)" >
```

```typescript
// componente app.component.ts
@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.scss']
})

export class AppComponent {
  keydown(e: KeyboardEvent) {
    console.log(e);
  }

  keypress(e: KeyboardEvent) {
    console.log(e);
  }

  keyup(e: KeyboardEvent) {
    console.log(e);
  }
}
```

### Uso de ngModel

Si queremos que una propiedad sea actualizada mediante gestos por parte del usuario (template) y que también el componente pueda tomar la decisión de actualizarlo ocupamos ngModel.

```html
<!--contenido dentro de app.component.html-->
<input [(ngModel)]="value" >
```

```typescript
// componente app.component.ts
@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.scss']
})

export class AppComponent {
    value = '';
}
```

De esta simple forma podemos aplicar una conexión bidireccional.

Para comprobarlo vamos a hacer uso de la interpolación mostrando en la vista el valor del input, veremos cómo desde la interpolación se va cambiando el valor del objeto a medida que el usuario ingresa caracteres dentro del input.

```html
<!--contenido dentro de app.component.html-->
<input [(ngModel)]="value" >

<div>El valor desde el componente es: {{value}}</div>



```

```typescript
// componente app.component.ts
@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.scss']
})

export class AppComponent {
    value = '';
}
```

Ahora vamos a añadir un botón que cuando sea presionado, cambie el valor del input, representando de esta manera el cambio por parte de la lógica o componente.
```html
<!--contenido dentro de app.component.html-->
<input [(ngModel)]="value" >
<div>El valor desde el componente es: {{value}}</div>
<button (click)="reset()">reset</button>

<button (click)="default()">default</button>
```

```typescript
// componente app.component.ts
@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.scss']
})

export class AppComponent {
  value = '';

  reset(): void {
    this.value = '';
  }

  default(): void {
    this.value = 'BEDU';
  }

}
```