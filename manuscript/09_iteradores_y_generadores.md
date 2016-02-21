# Iteradores y generadores

Los iteradores son una solución que propone ECMAScript 2015 para recorrer colecciones de objetos de forma ordenada. Los generadores son un nuevo tipo de función que puede devolver más de un valor. Una vez devuelto un valor por primera vez, podemos volver a llamarla y continuará ejecutándose en el mismo punto en que la dejamos. Un generador, por tanto, conserva el contexto de ejecución.

En este capítulo veremos cómo utilizar ambas características.

## Iteradores
Si has programado algo en JavaScript, es muy probable que hayas terminado haciendo algo como esto:

```JavaScript
var colors = [ 'red', 'green', 'blue' ];

for (var i = 0; i < colors.length; i++) {
  console.log(colors[i]);
}
```
El código anterior no es más que un bucle estándar que utiliza la variable `i` para mantener un cursor sobre el índice del array que se está recorriendo. Aunque es un ejemplo bastante sencillo, la complejidad aumenta cuando tenemos que crear bucles anidados.

Los **iteradores** no son más que objetos con una interfaz específica. La interfaz consiste en un método `next()` que devuelve un objeto con un resultado. Dicho objeto, contiene dos variables: `value`, que representa el valor siguiente; y `done`, el cual solo valdrá `true` cuando no haya más valores que devolver.

Veamos un ejemplo de iterador:

```javascript
function makeCountDown(counter) {
  let _counter = counter;
  return {
    next: function() {
      const value = _counter--;
      const done = _counter <= 0;

      return {
        value,
        done
      };
    }
  }
}

const countdown = makeCountDown(5);
console.log(countdown.next()); // { value: 5, done: false }
console.log(countdown.next()); // { value: 4, done: false }
console.log(countdown.next()); // { value: 3, done: false }
console.log(countdown.next()); // { value: 2, done: false }
console.log(countdown.next()); // { value: 1, done: true }
console.log(countdown.next()); // { value: 0, done: true }
```

## Sintaxis de un generador

Un generador es un tipo especial que funciona como factoría para iteradores. Una función se convierte en un generador si contiene una o más expresiones `yield` (producir) y si utiliza la sintaxis `function*` en su declaración.

```javascript
const enumerator = function* () {
  let index = 0;
  while(true)
    yield index++;
};

const enumGenerator = enumerator();

console.log(enumGenerator.next().value); // 0
console.log(enumGenerator.next().value); // 1
console.log(enumGenerator.next().value); // 2
```
Los generadores computan sus valores *producidos* bajo demanda, lo cual les permite representar secuencias de valores que son caras , computacionalmente hablando. O incluso infinitas, como se ha demostrado en el ejemplo anterior.

El método `next()` también permite un valor que puede ser utilizado para modificar el estado interno del generador. Un valor pasado por parámetro a `next()` será tratado como el resultado de la última expresión `yield` que pausó el generador.

Modifiquemos un poco el enumerador del ejemplo anterior para que sea reseteable:

```javascript
const enumerator = function*() {
  let index = 0;
  while(true) {
    let reset = yield index++;
    if(reset)
      index = 0;
  }
}

const enumGenerator = enumerator();

console.log(enumGenerator.next().value); // 0
console.log(enumGenerator.next().value); // 1
console.log(enumGenerator.next().value); // 2
console.log(enumGenerator.next().value); // 3
console.log(enumGenerator.next().value); // 4
console.log(enumGenerator.next(true).value); // 0
console.log(enumGenerator.next().value); // 1
```
