# Ejemplo 03 - Protección de rutas

- Identidicar el uso de Guards.
- Proteger nuestras rutas de Angular.

## Desarrollo

Angular nos ofrece los guard como método de seguridad de rutas con los cuales podemos hacer diferentes validaciones para determinar si el usuario tiene o no acceso a la ruta.

Para crear un Guard hacemos uso de CLI, para una mejor organización, generamos los guards dentro de una carpeta guards:

```
ng g guard guards/auth
```

En este ejemplo usaremos CanActivate. Una vez generado el guard, debemos añadirlo a los **providers** de nuestro módulo.

```typescript
// app.module.ts
import { NgModule } from "@angular/core";
import { BrowserModule } from "@angular/platform-browser";

import { AppRoutingModule } from "./app-routing.module";
import { AppComponent } from "./app.component";
import { HomeModule } from "./home/home.module";
import { LoginModule } from "./login/login.module";
import { DashboardModule } from "./dashboard/dashboard.module";
import { AuthGuard } from "./guards/auth.guard";

@NgModule({
  declarations: [AppComponent],
  imports: [
    BrowserModule,
    AppRoutingModule,
    HomeModule,
    LoginModule,
    DashboardModule,
  ],
  providers: [AuthGuard],
  bootstrap: [AppComponent],
})
export class AppModule {}
```

Nuestra clase Guard generada tiene la siguiente estructura:
```typescript
import { Injectable } from '@angular/core';
import { ActivatedRouteSnapshot, CanActivate, RouterStateSnapshot, UrlTree } from '@angular/router';
import { Observable } from 'rxjs';

@Injectable({
  providedIn: 'root'
})
export class AuthGuard implements CanActivate {
  canActivate(
    route: ActivatedRouteSnapshot,
    state: RouterStateSnapshot): Observable<boolean | UrlTree> | Promise<boolean | UrlTree> | boolean | UrlTree {
    return true;
  }

}
```
Dentro de la función canActivate podemos implementar las condiciones necesarias o autorizar o no el acceso a la ruta, por ejemplo revisar en localstorage que exista un ítem llamado token.

Ya tenemos disponible nuestro guard, ahora lo podemos implementar sobre las rutas que deseemos, por ejemplo si no queremos que el usuario acceda a la ruta **dashboard** a menos que posea un token de autenticación, añadimos el guard a la ruta:

```typescript
// dashboard-routing.module.ts
const routes: Routes = [
  {
    path: "dashboard",
    component: DashboardComponent,
    canActivate: [AuthGuard],
  }
];
```
