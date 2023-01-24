# Ejemplo 02 - Creación de rutas
## Objetivo

* Uso de rutas de Angular.
* Gestionar las rutas de Angular de manera modular.

## Desarrollo

Una vez definidas las rutas que deseemos usar dentro de nuestro módulo, tenemos que crear el componente principal que va a ir asociado a ellas.

Normalmente almacenamos nuestros componentes Angular dentro de una carpeta __/components__ que se encuentre dentro de nuestro módulo contenedor. Por ejemplo, si tenemos un módulo llamado Carrito, para crear los componentes que irán asociados a él por medio de rutas, usamos los siguientes comandos:


```
ng g c carrito/components/lista-precios

ng g c carrito/components/items

ng g c carrito/components/delivery
```
Y recuerda confirmar que tu modulo carrito posea en su lista __declarations__.

una vez creados los componentes, tenemos que declarar nuestro objeto de rutas en el archivo routing del módulo.

```typescript
// carrito-routing.module.ts
const routes: Routes = [
  {path: 'lista-precios', component: ListaPreciosComponent},
  {path: 'items', component: ItemsComponent},
  {path: 'delivery', component: DeliveryComponent},
];
```
Nuestras rutas ahora ya están creadas y podemos acceder a ellas mediante la URL de nuestra aplicación.

Si creamos módulos dentro de módulos, simplemente tenemos que seguir los mismos pasos, crear los componentes dentro del módulo a usar y administrar las rutas desde su archivo de routing.


