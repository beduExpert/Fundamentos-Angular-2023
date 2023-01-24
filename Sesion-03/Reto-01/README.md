# Reto 01 - Asociar nuestros componentes a una ruta específica

## Objetivo

- Identificar la manera en que podemos administrar nuestros proyectos por medio de rutas y módulos.

## Desarrollo

1. Con base en nuestro ejemplo 01, necesitamos que el módulo **home** posea la ruta **principal**, **contacto** y **ayuda**.

2. Crearemos una ruta **login** para nuestro módulo **login**, y una ruta **dashboard** para nuestro componente **dashboard**.

<details>
  <summary>Solución</summary>

### Actvidad #1

Primero creamos los componentes a utilizar para cada página:

```
ng g c home/components/principal

ng g c home/components/contacto

ng g c home/components/ayuda
```

Ahora configuraremos las rutas asociándolas con sus componentes.

```typescript
// home-routing.module.ts
const routes: Routes = [
  { path: "", component: PrincipalComponent },
  { path: "ayuda", component: AyudaComponent },
  { path: "contacto", component: ContactoComponent },
];
```

### Actividad #2

Crearemos los componentes necesarios.

```
ng g c login/components/login
ng g c dashboard/components/dashboard
```

Ahora configuraremos las rutas asociándolas con sus componentes.

```typescript
// login-routing.module.ts
const routes: Routes = [{ path: "login", component: LoginComponent }];
```

```typescript
// dasboard-routing.module.ts
const routes: Routes = [{ path: "dashboard", component: DashboardComponent }];
```

</details>
