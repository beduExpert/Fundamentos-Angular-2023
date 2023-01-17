# Reto 2: Imprementar caracteristicas de TypeScript

## Objetivo

- Utilizar las funciones y variables en nuestro componente.

## Desarrollo

Dentro de tu archivo TypeScript del componente inicial de tu aplicación:

1. Crea una función que imprima en consola un mensaje de bienvenida.

2. Crea una función para calcular el índice de masa corporal de una persona, esta función debe recibir el peso y la altura como parámetro y regresar el resultado.

3. Crea una función que imprima el resultado en consola obtenido de la función para calcular IMC.

<details>
    <summary>Solución 1</summary>

```typescript
class AppComponent {
  constructor() {
    this.bienvenida();
    const imc = this.calcularIMC(70, 1.8);
    this.imprimirIMC(imc);
  }

  bienvenida() {
    console.log("bienvenido al curso!");
  }

  calcularIMC(peso: number, altura: number): number {
    const base = altura * altura;
    const resultado = peso / altura;
    return resultado;
  }

  imprimirIMC(imc: number) {
    console.log("tu IMC es: " + imc);
  }
}
```

</details>

  </br>

<details>
  <summary>Solución 2</summary>

```typescript
class AppComponent {
  constructor() {
    this.bienvenida();
    const imc = this.calcularIMC(70, 1.8);
    this.imprimirIMC(imc);
  }

  bienvenida() {
    console.log("bienvenido al curso!");
  }

  calcularIMC(peso: number, altura: number): number {
    return peso / (altura ^ 2);
  }

  imprimirIMC(imc: number) {
    console.log("tu IMC es: " + imc);
  }
}
```

</details>

</br>

> Nota: No elimines la variable **title** ya que esta se encuentra conectada a la vista del componente, eliminarla podría generar un error en tu proyecto.