# Reto #2 - Uso de RouterLink

## Objetivo

- Utilizar la directiva RouterLink para crear la navegación de rutas desde la aplicación.

## Desarrollo

1. Los componentes de la ruta principal, contacto y ayuda necesitan tener un botón de navegación entre ellos, y un botón de login para las redirecciones.
2. Añadir al componente login un botón para navegar a la ruta dashboard.
3. El componente dashboard debe tener un botón log out el cual nos enviará a la ruta principal.

<details>
  <summary>Solución</summary>

### Actvidad #1

Haremos uso de la directiva routerLink dentro de nuestras template:

```html
<!-- principal.component.html -->
<a [routerLink]="['contacto']">Contacto</a>
<a [routerLink]="['ayuda']">Ayuda</a>
<button [routerLink]="['login']">Login</button>
```

```html
<!-- ayuda.component.html -->
<a [routerLink]="['/']">Inicio</a>
<a [routerLink]="['contacto']">Contacto</a>
<button [routerLink]="['login']">Login</button>
```

```html
<!-- contacto.component.html -->
<a [routerLink]="['/']">Inicio</a>
<a [routerLink]="['ayuda']">Ayuda</a>
<button [routerLink]="['login']">Login</button>
```

### Actividad #2

```html
<!-- login.component.html -->
<button [routerLink]="['dashboard']">Login</button>
```

### Actividad #3

```html
<!-- dashboard.component.html -->
<button [routerLink]="['/']">Log out</button>
```

</details>
