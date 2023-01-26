# Ejemplo 01 - Servicios en Angular

## Objetivo

* Crear servicios por medio de CLI.
* Inyección de servicios dentro de uno o múltiples componentes.
* Compartir datos entre componentes a través de servicios.

## Desarrollo

Para crear un servicio Angular haremos uso de CLI.
Normalmente almacenamos todos los servicios de nuestra aplicación en una carpeta services e internamente podemos organizarlos a nuestro gusto, ya sea por funcionalidad, alcance u objetivo.

```
ng g s services/usuario
```

Nuestro servicio generado se verá de la siguiente forma:

```typescript
import { Injectable } from '@angular/core';

@Injectable({
  providedIn: 'root'
})
export class UsuarioService {

  constructor() { }
}
```

Ahora dentro podemos hacer uso de variables y métodos. Por ejemplo, deseamos que este servicio tenga un objeto de tipo __usuario privado__, junto con sus métodos __get__ y __set__.

```typescript
// usuario.modelo.ts
export interface UsuarioModelo {
  nombre: string;
  edad: string;
  curso: string;
}
```

```typescript
import { Injectable } from '@angular/core';
import { UsuarioModelo } from '../models/usuario.modelo';

@Injectable({
  providedIn: 'root'
})
export class UsuarioService {

  private usuario!: UsuarioModelo;
  constructor() { }

  getUsuario() {
    return this.usuario;
  }

  setUsuario(usuario: UsuarioModelo) {
    this.usuario = usuario;
  }
}

```

El __constructor__ de los servicios solo se ejecuta la primera vez que el servicio es inyectado y generado. Por lo que podemos hacer uso de él para declarar valores iniciales.

```typescript
import { Injectable } from '@angular/core';
import { UsuarioModelo } from '../models/usuario.modelo';

@Injectable({
  providedIn: 'root'
})
export class UsuarioService {

  private usuario: UsuarioModelo;
  constructor() {
    this.usuario = { nombre: '', edad: '', curso: '' };
  }

  getUsuario() {
    return this.usuario;
  }

  setUsuario(usuario: UsuarioModelo) {
    this.usuario = usuario;
  }
}

```

Ahora inyectamos nuestros servicio al componente donde lo deseemos ocupar, para eso lo declararemos dentro del constructor de componente:

```typescript
import { Component } from '@angular/core';
import { UsuarioService } from '../../services/usuario.service';

@Component({
  selector: 'app-usuario',
  templateUrl: './usuario.component.html',
  styleUrls: ['./usuario.component.scss']
})
export class UsuarioComponent {

  constructor(private usuarioService: UsuarioService) { }
}
```
Con esta declaración ya podemos hacer uso de nuestro servicio, por ejemplo deseamos que una vez nuestro componente sea inicializado consulte la información del usuario.

```typescript
import { Component, OnInit } from '@angular/core';
import { UsuarioService } from '../../services/usuario.service';
import { UsuarioModelo } from '../../models/usuario.modelo';

@Component({
  selector: 'app-usuario',
  templateUrl: './usuario.component.html',
  styleUrls: ['./usuario.component.scss']
})
export class UsuarioComponent implements OnInit{

  public usuarioActual!: UsuarioModelo;

  constructor(private usuarioService: UsuarioService) { }

  ngOnInit(): void {
    this.usuarioActual = this.usuarioService.getUsuario();
  }
}
```
Todos los componentes que deseemos pueden utilizar el mismo servicio y su estado siempre será el mismo, esto significa que si un componente modifica el valor del atributo usuario en nuestro ejemplo, al leerlo desde otro componente obtendremos el valor más reciente.

Es importante resaltar que el estado del servicio se mantiene siempre y cuando el navegador no sea recargado, ya que si esto pasa, la aplicación liberará todo el uso de memoria y perdiendo la información almacenada.

Si deseamos que alguna información sea persistente como lo puede ser un token de inicio de sesión y no se pierda aun después de recargar la página podemos hacer uso del localstorage.