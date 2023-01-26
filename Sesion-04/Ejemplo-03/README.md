# Ejemplo #03 - Principales servicios Angular

## Objetivo

- Implementar el servicio Router como solución a la navegación desde la lógica del componente.
- Uso del ActivatedRoute para obtener información de la ruta actual.

## Desarrollo

El servicio Router nos ayuda a navegar entre las rutas de nuestra aplicación desde la lógica de nuestro componente. Un ejemplo de uso es al terminar las validaciones dentro de un método, mover al usuario a otra página de la aplicación o después de consultar información por medio de HTTPClient.

Es indispensable tener importado el módulo __AppRoutingModule__ dentro de nuestro módulo principal __AppModule__.

Para hacer uso del Router lo tenemos que inyectar en nuestro componente:

```typescript
constructor(private router: Router) { }
```

Una vez inyectado haremos uso de su método **navigate([])** para hacer el llamado a moverse a la nueva ruta declarada en su primer parámetro.

```typescript
this.router.navigate(["inicio"]);
```

Si deseamos pasar un parámetro lo podemos hacer de las siguientes formas:

```typescript
// forma 1
goToDetalleProducto(id: string) {
  this.router.navigate([`producto/detalle/${id}`]);
}
// forma 2
goToDetalleProducto(id: string) {
  this.router.navigate([`producto/detalle/`, id]);
}
```

ActivatedRoute nos sirve para consultar los parámetros de nuestra ruta actual, normalmente lo usamos para obtener ids o información relevante obtenida al momento de navegar en la ruta.

Un ejemplo común de uso es pasar el ID de un elemento a la ruta a navegar para que al momento de ser creado el componente principal de la nueva ruta se lea este parámetro y se realicen las consultas necesarias al servidor backend
Otro uso es si el usuario recarga la página o comparte un link con parámetros, el sistema pueda realizar las consultas iniciales para mostrar la información compartida.

```typescript
constructor(private route: ActivatedRoute) { }
```

Para poder consultar los parámetros tenemos dos alternativas, consultar el dato directamente o usar un suscriptor que nos mantendrá informados si el parámetro cambia en algún momento.

```typescript
constructor(private route: ActivatedRoute) { 
  route.snapshot.paramMap.get('nombre-parametro-declarado-en-ruta');
  route.snapshot.paramMap.get('id');
}
```

```typescript
constructor(private route: ActivatedRoute) {
  let productoID = route.snapshot.paramMap.get('idProducto');

  route.paramMap.subscribe(params => {
    params.get('nombre-parametro');
    params.get('id')
  });
}
```


