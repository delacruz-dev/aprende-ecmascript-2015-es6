# Desestructuración de arrays y objetos

## Desestructuración de Arrays

```javascript
var numbers = ["1", "2", "3"];

// without destructuring
const one   = foo[0];
const two   = foo[1];
const three = foo[2];

// with destructuring
var [one, two, three] = foo;
```

Podemos asignar de forma desestructurada sin una declaración en la asignación:

```javascript
var one, two;
[one, two] = [ "1", "2"];
```

Yendo un poco más allá, podemos utilizar funciones para devolver un conjunto de valores y asignarlos de forma desestructurada:

```javascript
function f() {
    return ["1", "2"];
}
```

De este modo podemos devolver cualquier número de valores de forma arbitraria. Hasta aquí ninguna novedad, pero si utilizamos la asignación desestructurada:

```javascript
var one, two;
[one, two] = f();
console.log(one, two); // 1, 2
```

La asignación de variables se realiza en orden, el primer valor se asigna a la primera variable, el segundo a la segunda... y así.

## Desestructuración de objetos
```javascript
// ES6
var persona = {nombre: 'Dani', apellidos: 'de la Cruz'};
var {nombre, apellidos} = persona;

console.log(nombre); // Dani
console.log(apellidos); // de la Cruz
```

Tal y como puedes ver, podemos crear variables al vuelo a partir de un objeto de Javascript, para luego utilizarlas. Las nuevas variables tendrán por defecto el nombre que tenían las propiedades del objeto. Pero, ¿qué pasa si no nos gusta y queremos cambiarlo? En el ejemplo, no es demasiado correcto utilizar nombres de variables en castellano...

Bueno, en esta vida casi todo tiene arreglo:

```javascript
// ES6
var {nombre: name, apellidos: surname} = persona;
console.log(name); // Dani
console.log(surname); // de la Cruz
```

Este comportamiento es especialmente útil a la hora de pasar parámetros a funciones, como veremos a continuación.

```javascript
// ES6
function suma({a, b} = {}) {
  return a + b;
};

var a = 2;
var b = 3;
console.log(suma({a, b})); // 5
```
Como ves, la función `suma` espera un objeto con dos propiedades: `a` y `b`, cuyo valor desconoce. Pero tan solo declarando dos variables del mismo nombre, podemos crear un objeto al vuelo y pasárselo como argumento a la función. El código siguiente es equivalente al anterior, pero con algo más de ceremonia:

```javascript
// ES6
console.log(suma({a: a, b: b})); // 5
```
Obviamente, nadie utiliza esta segunda forma, ya que ECMAScript asigna automáticamente los valores a propiedades del mismo nombre.

## Parámetros por defecto en funciones

La asignación desestructurada nos facilita muchísimo la vida al trabajar con funciones que reciben parámetros.

Veamos un ejemplo en ECMAScript 5:

```javascript
// ES5

function drawCircle(options){
    options = options === undefined ? {} : options;
    var radius = options.radius === undefined ? 30 : options.radius;
    var coords = options.coords === undefined ? { x: 0, y: 0 } : options.coords;
    
    console.log(radius, coords);
    // finally, draw the circle
}
```

ECMAScript 5 nos obligaba a realizar una programación demasiado defensiva en el interior de la función, violando además el Single Responsibility Principle: una función solo debería tener un motivo para cambiar. Y la función `drawCircle` tiene demasiadas responsabilidades: comprobar la integridad de los parámetros proporcionados y dibujar el círculo. 

Pero aquí no terminan los inconvenientes. ¿Qué es options? La firma del método no especifica qué debe ser, si un entero, una cadena de texto o un objeto con propiedades completamente arbitrarias. Y si intentásemos cambiar esto por una firma más explícita como la siguiente tampoco mejoraríamos el problema, ya que estaríamos obligando al consumidor de la función a pasar los argumentos en un orden concreto, complicando la mantenibilidad del código posterior:

```javascript
// ES5
function drawCircle(radius, coords) { ... }
```

Para resolver estos problemas, llegua ECMAScript 6 al rescate. Veamos el ejemplo anterior utilizando algunas de las características del nuevo estándar:

```javascript
function drawCircle({radius = 30, coords = { x: 0, y: 0}} = {}) {
    console.log(radius, coords);
    // draw the circle
}
```
Como ves, todo el *bootstrapping* de programación defensiva que había que realizar en ES5 solo para que nuestro código no lanzase una excepción, ha desaparecido. O para ser más precisos, se ha camuflado dentro de la firma de la función con un objeto, que por defecto puede estar vacío y cuyas propiedades tienen valores por defecto que tomarán si no se las asigna.

De este modo, nuestro código no lanzará un error si no asignamos algún valor, la firma del método es mucho más descriptiva y deja de importar el orden de los argumentos a la hora de invocar a `drawCircle`.

Todos los ejemplos siguientes funcionarían:

```javascript

drawCircle(); // radius: 30, coords.x: 0, coords.y: 0 }
drawCircle({radius: 10}); // radius: 10, coords.x: 0, coords.y: 0 }
drawCircle({coords: {y: 10, x: 30}, radius: 10}); // radius: 10, coords.x: 30, coords.y: 10 }
```

## Sintaxis del operador de propagación

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
## El operador de propagación para propiedades de objetos

No quería dejar de hablar de una de las funciones más útiles del operador de propagación: la posibilidad de utilizarlo con propiedades de objetos.

Aunque sea una propuesta para la siguiente versión del estándar (ECMAScript 2016 o ES7), en el momento de escribir estas líneas se encuentra en **Stage 2**, así que es bastante seguro comenzar a utilizarlo desde hoy mismo gracias a la potencia de Babel.

Como podemos ver en el siguiente ejemplo, el [operador de propagación para propiedades de objetos](https://github.com/sebmarkbage/ecmascript-rest-spread) resulta muy útil para añadir nuevas propiedades a un objeto, o sobreescribirlas al vuelo: 

```javascript
const worker = {
  id: 1337,
  name: 'John',
  surname: 'Woo',
  age: 35,
  job: 'UI designer'
};

const f = function({worker} = {}){
  return {
    ...worker,
    fullName: `Mr./Mrs. ${worker.surname}, ${worker.name}`,
    age: `${worker.age} years old`
  };
};

console.log(f({worker}));
```

El objeto que devuelve la consola tendrá la nueva propiedad `fullName` y también habrá cambiado el tipo de la propiedad `age` a algo más legible. Pero como utilizamos el operador de propagación, también tendrá el resto de propiedades del objeto `worker`.