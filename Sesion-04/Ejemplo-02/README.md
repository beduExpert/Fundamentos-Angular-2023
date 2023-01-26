# Ejemplo #02 - HTTPClient y RxJS

## Objetivo

- Consultar servicios REST por medio de solicitudes HTTP.
- Conocer el uso de observables y suscriptores de la librería RxJS.
- Control de errores en peticiones HTTP.

## Desarrollo

Para poder realizar solicitudes HTTP necesitamos usar el servicio HTTPClient ofrecido por Angular. Este servicio podemos ocuparlo directamente dentro de nuestros componentes, pero para un mejor control de la aplicación y reusabilidad usamos este servicio dentro de un servicio personalizado que se encargue de gestionar y compartir nuestras solicitudes.

Para hacer uso del servicio HTTPClient, debemos importar en nuestro módulo principal __AppModule__ el modulo __HttpClientModule__.

```typescript
@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    BrowserModule,
    AppRoutingModule,
    HttpClientModule,
  ],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

Creamos un servicio **Producto** que gestionará todo lo relacionado a las solicitudes

```
ng g s services/api/producto
```

```typescript
import { Injectable } from "@angular/core";

@Injectable({
  providedIn: "root",
})
export class ProductoService {
  constructor() {}
}
```

Ahora inyectamos el servicio HTTPClient:

```typescript
import { Injectable } from "@angular/core";
import { HttpClient } from "@angular/common/http";

@Injectable({
  providedIn: "root",
})
export class ProductoService {
  constructor(private httpClient: HttpClient) {}
}
```

El servicio HTTPClient nos ofrece diferentes métodos para realizar solicitudes recibiendo como primer parámetro el endpoint a usar, y como segundo parámetro para los métodos PUT POST DELETE, el cuerpo de la solicitud

```typescript
this.httpClient.get("https://api.bedu.com/producto");

this.httpClient.post("https://api.bedu.com/producto", {});
```

Todos estos métodos nos regresan un Observable el cual retornaremos para que el componente o servicio que lo implemente haga uso de él

```typescript
import { Injectable } from "@angular/core";
import { HttpClient } from "@angular/common/http";

@Injectable({
  providedIn: "root",
})
export class ProductoService {
  constructor(private httpClient: HttpClient) {}

  getProducto() {
    return this.httpClient.get("https://api.bedu.com/producto");
  }

  postProducto() {
    return this.httpClient.post("https://api.bedu.com/producto", {
      alumno: "bedu",
      edad: 20,
      curso: "Fundamentos de Angular",
    });
  }

  putProducto(id: string) {
    return this.httpClient.put(`https://api.bedu.com/producto/${id}`, {
      curso: "Fundamentos de Angular 2023",
    });
  }

  deleteProducto(id: string) {
    return this.httpClient.put(`https://api.bedu.com/producto/${id}`, null);
  }
}
```

Gracias a TypeScript podemos tipar el tipo de objeto que nos retornará el observable y el método:

```typescript
import { Injectable } from '@angular/core';
import { HttpClient } from '@angular/common/http';
import { ProductoModelo } from '../../models/producto.model';
import { Observable } from 'rxjs';

@Injectable({
  providedIn: 'root'
})
export class ProductoService {

  constructor(private httpClient: HttpClient) { }

  getProducto(): Observable<ProductoModelo> {
    return this.httpClient.get<ProductoModelo>('https://api.bedu.com/producto');
  }

  postProducto(): Observable<ProductoModelo> {
    return this.httpClient.post<ProductoModelo>('https://api.bedu.com/producto',
      {
        alumno: 'bedu',
        edad: 20,
        curso: 'Fundamentos de Angular'
      });
  }

  putProducto(id: string): Observable<boolean> {
    return this.httpClient.put<boolean>(`https://api.bedu.com/producto/${id}`,
      {
        curso: 'Fundamentos de Angular 2023'
      });
  }

  deleteProducto(id: string): Observable<boolean> {
    return this.httpClient.put<boolean>(`https://api.bedu.com/producto/${id}`, null);
  }

}
```
Ahora podemos inyectar el servicio en nuestro componente y hacer uso de los métodos.

Los observables son objetos que emiten un valor o varios valores a lo largo del tiempo, en el caso de solicitudes HTTP solo envían un valor en el momento que reciben la respuesta.

Los observables son implementados por Subscriber que nos permite mantenernos escuchando los cambios emitidos por el observable.

En el caso de observables de solicitudes HTTP, cuando algún método realiza la suscripción a él, envía la solicitud establecida y emite la respuesta una vez se obtiene del servidor consultado.

Si todo salió bien con nuestra solicitud la información recibida llegará al subscribe por medio del arrow function.

Implementemos nuestro primer suscriptor dentro de nuestro componente:

```typescript
import { Component, OnInit } from '@angular/core';
import { ProductoService } from '../../services/api/producto.service';

@Component({
  selector: 'app-product',
  templateUrl: './product.component.html',
  styleUrls: ['./product.component.scss']
})
export class ProductComponent implements OnInit {

  public productoData: any;

  constructor(private productoService: ProductoService) {
  }
  ngOnInit(): void {
    this.consultarProducto();
  }

  consultarProducto() {
    this.productoService.getProducto().subscribe(respuesta => {
      console.log('Respuesta en caso de que la solicitud retorne un estado success: ', respuesta);
    });
  }
}
```

Para controlar los errores de una solicitud HTTP podemos añadir un arrow fuction más por el cual obtendremos el error.

```typescript
import { Component, OnInit } from '@angular/core';
import { ProductoService } from '../../services/api/producto.service';

@Component({
  selector: 'app-product',
  templateUrl: './product.component.html',
  styleUrls: ['./product.component.scss']
})
export class ProductComponent implements OnInit {

  public productoData: any;

  constructor(private productoService: ProductoService) {
  }
  ngOnInit(): void {
    this.consultarProducto();
  }

  consultarProducto() {
    this.productoService.getProducto().subscribe(respuesta => {
      console.log('Respuesta en caso de que la solicitud retorne un estado success: ', respuesta);
    }), (error: any) => {
      console.log('error : ', error);
      // lógica a ejecutar en caso de error
    }
  }
}
```

