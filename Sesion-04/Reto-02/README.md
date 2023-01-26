# Reto # - Consultas a servidores REST


## Objetivo


* Uso de HTTPClient para conexión con servicios REST
* Implementación de RXjS para consultas de datos

## Desarrollo

1. Crea un servicio API para realizar la consulta a la siguiente api publica: https://www.boredapi.com/
   Implementa la consulta get para obtener actividades y por medio de un botón desde tu componente el cual al recibir un click lance una consulta.

<br>

2. Implementa la siguiente API pública: https://genderize.io/
   
   Usa el endpoint https://api.genderize.io?name={name}, donde el atributo name debe salir de un input de tu vista y la consulta ser realizada por medio de un botón en la misma vista.

<!--<details> -->
    <summary>Solución</summary>

Servicio API:

```typescript
import { HttpClient } from '@angular/common/http';
import { Injectable } from '@angular/core';
import { Observable } from 'rxjs';
import { ActivityModel, GenderModel } from 'src/app/models/activity.model';

@Injectable({
  providedIn: 'root'
})
export class EjemplosService {

  constructor(private httpClient: HttpClient) { }

  getActivity(): Observable<ActivityModel> {
    return this.httpClient.get<ActivityModel>('https://www.boredapi.com/api/activity');
  }

  getGender(name: string): Observable<GenderModel> {
    return this.httpClient.get<GenderModel>(`https://api.genderize.io?name=${name}`);
  }

}
```
### consulta 1
Componente para consultar actividades:

```html
<!-- activity-component -->
<button (click)="getActividad()">obtener actividad</button>
```
```typescript
// activity-component
import { Component } from '@angular/core';
import { EjemplosService } from '../../../services/api/ejemplos.service';

@Component({
  selector: 'app-activity',
  templateUrl: './activity.component.html',
  styleUrls: ['./activity.component.scss']
})
export class ActivityComponent {

  constructor(private ejemplosService: EjemplosService) { }
  
  getActividad() {
    this.ejemplosService.getActivity().subscribe(activity => {
      console.log(activity);

    }), (err: any) => {
      window.alert('error al obtener actividad');
    };
  }
}

```
### Consulta 2

Importamos __FormsModule__ dentro de __AppModule__ para hacer uso de la directiva ngModel.

```typescript
@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    BrowserModule,
    AppRoutingModule,
    FormsModule,
    HttpClientModule,
  ],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

```html
<!-- gender-component -->
<input type="text" [(ngModel)]="nombre" placeholder="Nombre">

<button (click)="getTipoGenero()">Consultar género</button>

```

```typescript
import { Component } from '@angular/core';
import { EjemplosService } from 'src/app/services/api/ejemplos.service';

@Component({
  selector: 'app-gender',
  templateUrl: './gender.component.html',
  styleUrls: ['./gender.component.scss']
})
export class GenderComponent {

  nombre: string = '';
  constructor(private ejemplosService: EjemplosService) { }

  getTipoGenero() {
    this.ejemplosService.getGender(this.nombre).subscribe(gender => {
      console.log(gender);
    }), (err: any) => {
      window.alert('error al consultar datos');
    };
  }

}

```


</details>