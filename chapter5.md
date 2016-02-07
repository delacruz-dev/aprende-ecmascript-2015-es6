# Capítulo 5: Desestructuración

## Desestructuración de arrays

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
var persona = {nombre: 'Dani', apellidos: 'de la Cruz'};
var {nombre, apellidos} = persona;

console.log(nombre); // Dani
console.log(apellidos); // de la Cruz
```

Tal y como puedes ver, podemos crear variables al vuelo a partir de un objeto de Javascript, para luego utilizarlas. Las nuevas variables tendrán por defecto el nombre que tenían las propiedades del objeto. Pero, ¿qué pasa si no nos gusta y queremos cambiarlo? En el ejemplo, no es demasiado correcto utilizar nombres de variables en castellano...

Bueno, en esta vida casi todo tiene arreglo:

```javascript
var {nombre: name, apellidos: surname} = persona;
console.log(name); // Dani
console.log(surname); // de la Cruz
```

## Parámetros por defecto

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