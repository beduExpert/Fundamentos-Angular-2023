# Reto 01 - Servicios Angular

## Objetivo

* Crear servicios de Angular
* Uso de LocalStorage

## Desarrollo

Crea un servicio Angular para el control del LocalStorage añadiendo los métodos, __almacenar__, __consultar__, __borrar__, __limpiarTodo__.

El localStorage del navegador se basa en objetos clave: valor, donde el valor siempre es almacenado en tipos de datos básicos, por lo que si deseas almacenar un objeto deberás convertirlo a string antes de almacenarlos, y convertirlo a objeto después de leerlo.

<details>
    <summary>Solución</summary>

Para convertir un objeto a string hacemos uso de __JSON__ y su método __stringify()__.
Para convertir un string a objeto hacemos uso de __JSON__ y su método __parse()__.


```typescript
import { Injectable } from '@angular/core';

@Injectable({
  providedIn: 'root'
})
export class LocalStorageService {

  constructor() { }

  almacenar(llave: string, valor: any) {
    localStorage.setItem(llave, JSON.stringify(valor));
  }

  consultar(llave: string) {
    return JSON.parse(localStorage.getItem(llave)|| '');
  }

  borrar(llave: string) {
    localStorage.removeItem(llave);
  }

  limpiarTodo() {
    localStorage.clear();
  }
}

```

</details>