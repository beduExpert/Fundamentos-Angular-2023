# Ejemplo 01 - Creación de módulos

## Objetivo

* Crear proyectos angular con routing pre configurado.
* Creación y administración de módulos.

## Desarrollo

Para crear un proyecto Angular con el routing principal preconfigurado haremos uso de CLI:

```
ng new proyecto_modular --routing
```

Siempre que generamos un proyecto nuevo de Angular, la template nuestro componente __app.component__ se genera con un ejemplo, borraremos dicho ejemplo y solo dejaremos declarado el componente de routing:

```html
<!-- app.component.html -->
<router-outlet></router-outlet>
```

En este ejemplo vamos a añadir un módulo __home__ que será lo primero que el usuario va a ver al entrar al sitio, un módulo __login__, que será cargado cuando el usuario pulse algún botón de login, y un módulo __dashboard__ que será cargado una vez que el usuario realice un login correcto.

Para realizar esto, primero vamos a generar los módulos a usar junto con su archivo de routing usando CLI.

```
ng g m home --routing

ng g m login --routing

ng g m dashboard --routing

```

Una vez creados nuestros módulos, tenemos que importarlos al módulo principal para que se pueda hacer eso de ellos, si no hacemos esto, las rutas y componentes incluidos en nuestros módulos no van a estar disponibles para nuestra aplicación.

```typescript
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';

import { AppRoutingModule } from './app-routing.module';
import { AppComponent } from './app.component';
import { HomeModule } from './home/home.module';
import { LoginModule } from './login/login.module';
import { DashboardModule } from './dashboard/dashboard.module';

@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    BrowserModule,
    AppRoutingModule,
    HomeModule,
    LoginModule,
    DashboardModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```
Ahora deseamos que una vez el usuario acceda al dashboard pueda dirigirse a las siguientes rutas:
* Listar productos.
* Ver producto.
* Editar producto.

Para esto crearemos un nuevo módulo llamado __producto__ dentro de nuestro módulo __dashboard__.

```
ng g m dashboard/producto --routing
```

Ahora junto al routing y module de dashboard tenemos una carpeta producto que contiene sus archivos de routing y module.

Para terminar, necesitamos importar el módulo de __producto__, pero en esta ocasión será dentro de su módulo contenedor __dashboard__.

```typescript
import { NgModule } from '@angular/core';
import { CommonModule } from '@angular/common';

import { DashboardRoutingModule } from './dashboard-routing.module';
import { ProductoModule } from './producto/producto.module';


@NgModule({
  declarations: [],
  imports: [
    CommonModule,
    DashboardRoutingModule,
    ProductoModule
  ]
})
export class DashboardModule { }
```
Podemos crear módulos que se encarguen de distribuir componentes, directivas o distintas clases compartidas como lo pueden ser botones, header, footer. Generalmente los llamamos __SharedModule__ y no poseen módulo de ruteo.


Crearemos nuestro __SharedModule__ y dentro almacenaremos un componente footer.


```
ng g m shared
ng g c shared/components/footer
```

Ahora importamos nuestro __SharedModule__ dentro de los módulos que deseemos que usen su contenido compartido, por ejemplo loginModule.

```typescript
import { NgModule } from '@angular/core';
import { CommonModule } from '@angular/common';

import { LoginRoutingModule } from './login-routing.module';
import { LoginComponent } from './components/login/login.component';
import { SharedModule } from '../shared/shared.module';


@NgModule({
  declarations: [
    LoginComponent
  ],
  imports: [
    CommonModule,
    LoginRoutingModule,
    SharedModule
  ]
})
export class LoginModule { }
```
Y ahora solo falta añadir a nuestro __SharedModule__ los componentes que deseemos compartir en el arreglo __exports__.

```typescript
import { NgModule } from '@angular/core';
import { CommonModule } from '@angular/common';
import { FooterComponent } from './components/footer/footer.component';
@NgModule({
  declarations: [
    FooterComponent
  ],
  imports: [
    CommonModule
  ],
  exports: [
    FooterComponent
  ]
})
export class SharedModule { }
```