# Sesión #4: Inyección de dependencias y consumo de API REST

## :dart: Objetivos

- Integrar un API Rest a proyectos Angular por medio del servicio HTTPClient.
- Comprender y aplicar la librería RxJS. 

## ⚙ Desarrollo

En esta sesión aprendimos a consumir aplicaciones backend por medio de un API Rest usando el servicio HTTPClient que nos proporciona Angular y la librería RxJS.

### Asegúrate de comprender

El uso de la libreria RxJS para la gestion de eventos asincronos.

### Indicaciones generales

+ Conecta tu proyecto Angular a los servicios API REST desarrollados a lo largo del curso por medio de HTTPClient.
+ Implementa tus propios servicios para compartir información entre  componentes.
+ Conecta tu componente de login a los servicios API REST desarrollados en los módulos anteriores y almacena tu token dentro del localStorage para que tu Guard de rutas privadas pueda hacer uso de él.
+ Haz uso de un interceptor para modificar una solicitud HTTP añadiendo el atributo token obtenido de tu API desarrollada en sesiones pasadas.

A continuación te dejamos una lista de recursos donde podrás profundizar acerca de los interceptores de Angular y la libreria RxJS:
* https://amoelcodigo.com/interceptor-angular/
* https://medium.com/ngconf/rxjs-for-beginner-angular-developers-part-2-fundamentals-535b939378d5
* https://osmancea.medium.com/programación-reactiva-con-rxjs-bebc9432485f

No olvides revisar el checklist del postwork en la AppBedu