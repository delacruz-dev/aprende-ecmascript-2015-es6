# Parámetros por defecto en funciones

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