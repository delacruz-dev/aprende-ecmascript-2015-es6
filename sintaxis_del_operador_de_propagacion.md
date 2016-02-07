# Sintaxis del operador de propagación

El operador de propagación, o *spread operator*, nos permite una aproximación mucho más directa al acceso del contenido dentro de un array o de cualquier objeto. Veamos cómo funciona:

```javascript
const values = [1, 2, 3, 4];

console.log(values); // [1, 2, 3, 4]
console.log(...values); // 1 2 3 4
```

En la primera impresión por consola, enviamos directamente el array a la función `log`. En cambio, en la segunda, *descomponemos* el array en un conjunto de parámetros que se pasan como argumentos a la función log, así que imprime cada valor directamente.

Esto nos da mucha flexibilidad a la hora de pasar parámetros a una función, ya que si antes teníamos, por ejemplo:

```javascript
// ES5

var f = function(x, args) {
    return x + args.length;
};

var parameters = [ "hello", true ];
console.log(f(3, parameters)); // 5
```

```javascript
// ES6

var f = function (x, ...y){
  return x + y.length;
};

console.log(f(3, "hello", true)); // 5
```

Como puedes observar, la utilización del *spread operator* nos permite pasar un número arbitrario de parámetros a una función y recogerlos en una variable, sin necesidad de crear un array para ello.

También podemos hacerlo a la inversa, utilizándolo a la hora de pasar los parámetros, en lugar de en la declaración del método:

```javascript
// ES6

function f(x, y, z) {
  return x + y + z;
}
console.log(f(...[1, 2, 3])); // 6
```