> Work in progress. Check: https://github.com/tvcutsem/harmony-reflect/wiki

# Reflection

*Reflect* es un nuevo objeto que proporciona métodos para interceptar operaciones de JavaScript. A diferencia de la mayoría de objetos globales, *Reflect* no es una función constructora. No es posible utilizarlo con el operador `new`o invocarlo como una función. Todas las propiedades y métodos de *Reflect* son estáticas (igual que en el objeto *Math*, por ejemplo).

La técnica de la *reflexión* es casi tan antigua como las ciencias de computación. Los primeros ordenadores estaban programados en **lenguaje de ensamblador**, el cual es reflexivo de forma inherente. Ha permanecido vigente hasta hoy en día, con estandartes como Java o C# haciendo gala de su uso; si bien no todos los lenguajes de programación han encontrado la necesidad de implementarla.

En ECMAScript 5 también era posible utilizar esta técnica, mediante la evaluación de funciones o utilizando algunos de los métodos proporcionados por `Object` o `Function`. Ahora, gracias a ECMAScript 2015, disponemos de una API más específica, flexible y segura a tal efecto.

Consiste en la capacidad de un programa de **modificar su estructura y comportamiento en tiempo de ejecución**.

## Por qué usar `Reflect` ##

### Valores de retorno más útiles ###
Los métodos de `Reflect` son muy similares a los que podemos encontrar llamando a `Object`, pero proporcionan un resultado más significativo.

```JavaScript
// ES 5
try {
  Object.defineProperty(obj, name, desc);
  // property defined successfully
} catch (e) {
  // possible failure (and might accidentally catch the wrong exception)
}
```
El código anterior era válido en ES5 para definir una propiedad dentro de un objeto, sin embargo podía devolver varioes tipos de error si algo no iba bien, que nos obligaban a gestionar con bloques `try-catch`.

Con ES2015, podemos refactorizar el código anterior en lo siguiente:

```JavaScript
if(Reflect.defineProperty(obj, name, desc)) {
  // success
} else {
  // failure
}
```
Al devolver un booleano, nos libramos de la gestión de errores y podemos actuar en consecuencia si la propiedad que se ha intentado definir no ha sido creada.

### Aplicación de funciones más fiable ###
En ES5, cuando queríamos llamar a una función `f` con un número de argumentos variable vinculando el valor de `this` a un objeto, podíamos utilizar:

```JavaScript
f.apply(obj, args);
```

Sin embargo, `f` podría ser un objeto en el que alguien ya hubiese definido un método `apply`. Si queremos asegurarnos de que vamos a llamar al método `apply` proporcionado por el lenguaje, hasta ahora podíamos hacerlo de la siguiente forma:

```JavaScript
// ES 5
Function.prototype.apply.call(f, obj, args);
```

Con ECMAScript 2015 tenemos una alternativa igual de fiable y más fácil de llamar:

```JavaScript
// ES 6
Reflect.apply(f, obj, args);
```

### Constructores con un número arbitrario de argumentos
Si queremos llamar a un constructor con un número arbitrario de argumentos, en ES6, gracias a la sintaxis del operador de propagación, podemos hacerlo de la siguiente manera:

```JavaScript
var obj = new F(...args);
```

En ES5 esto es más complicado de escribir, ya que tan solo podríamos utilizar `F.apply` o `F.call` para llamar a una función con un número variable de argumentos. Pero no existe una función `F.construct` para instanciar la función constructora con un número arbitrario de parámetros. Con `Reflect`, ahora podemos:

```JavaScript
var obj = Reflect.construct(F, args);
```

Veámoslos en detalle:

## `Reflect.apply()` ##

Llama a una función de destino cuyos argumentos se especifican utilizando el parámetro `argumentsList`.

### Sintaxis

```JavaScript
Reflect.apply(target, thisArgument, argumentsList)
```

* **target**: La función de destino a llamar
* **thisArgument**: El valor de `this` para proporcionar a la llamada de la función de destino.
* **argumentsList**: Un array de objetos que representa los argumentos con los que se debe llamar a la función de destino.

En ES5, podíamos utilizar `Function.prototype.apply()` para llamar a una función proporcionándole un valor para `this` y una lista de argumentos:

```javascript
// ES5
Function.prototype.apply.call(Math.floor, undefined, [1.75]);
```

Con `Reflect.apply`, el comportamiento es idéntico, pero menos *verboso* y fácil de entender. Veamos algunos ejemplos:

```javascript
// ES6
Reflect.apply(Math.floor, undefined, [1.75]);
// 1;

Reflect.apply(String.fromCharCode, undefined, [104, 101, 108, 108, 111]);
// "hello"

Reflect.apply(RegExp.prototype.exec, /ab/, ["confabulation"]).index;
// 4

Reflect.apply("".charAt, "ponies", [3]);
// "i"
```

## `Reflect.defineProperty()`

```javascript
var obj = {};
Reflect.defineProperty(obj. "x", {value: 7}); //true
obj.x; // 7
```
