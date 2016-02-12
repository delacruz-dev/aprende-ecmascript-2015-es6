# Conceptos previos de orientación a objetos en JavaScript

## Qué es un constructor?
Básicamente un constructor es cualquier función que se utiliza como un constructor. ¿Perogrullada? Estoy seguro, pero es que un constructor no tiene nada de especial hasta que no se utiliza como tal. Esta definición es válida independientemente del lenguaje de programación con el que trabajemos. Veamos un ejemplo de función constructor:

```javascript
var Vehicle = function Vehicle() {
    console.log('¡Sólo soy una función!');
    // ...
}

var motorcycle = new Vehicle();
```

La función Vehicle es una función normal, pero cuando la utilizamos mediante la palabra reservada `new`, además de ejecutar el código del cuerpo de la función, JavaScript hace que pasen cuatro cosas:

1. Se crea un nuevo objeto
2. Establece la propiedad `constructor` del objeto a la función `Vehicle`
3. Configura el objeto para delegar en `Vehicle.prototype`
4. Llama a `Vehicle()`en el contexto del nuevo objeto

El resultado de `new Vehicle()` es este nuevo objeto.

```javascript
typeof Vehicle;
> 'function'
typeof Vehicle();
> 'undefined'
typeof new Vehicle();
> 'object'
```
La diferencia entre las tres llamadas es que mientras `Vehicle` es la definición de la función, `Vehicle()` representa el valor retornado por la función y en este caso no retornamos nada, así que es `undefined`. Por último, `new Vehicle()`. Devuelve un nuevo objeto que será una instancia de `Vehicle`.

** NOTA: No es aconsejable retornar ningún valor en funciones constructoras, ya que el valor retornado sobreescribirá la instancia del objeto creado**

### La propiedad `constructor`
Establecer la propiedad `constructor` en el objeto creado significa dos cosas:

```javascript
motorcycle.constructor == Vehicle // true
motorcycle instanceof Vehicle // true
```

El objeto creado tendrá una propiedad `constructor` bastante especial. No aparecerá si enumeramos las propiedades del objeto, pero podemos crearla y asignarla al nuevo objeto, sobreescribiendo la propiedad original:

```javascript
motorcycle; // {}

var Postman = function Postman() {};
motorcycle.constructor = Postman;
motorcycle; // Postman { constructor: [Function: Postman] }
```

En el fragmento de código anterior hemos creado una nueva función constructora llamada `Postman` (cartero, en inglés). Posteriormente, asignamos a esa función una propiedad constructor de nuestro objeto `motorcycle`. Si evaluamos ahora `motorcycle`, veremos que ahora tiene una propiedad `constructor` que no es más que la función `Postman`. Pero, ¿ha cambiado el tipo de nuestro objeto?

```javascript
motorcycle.constructor == Postman // true
motorcycle instanceof Postman // false
motorcycle instanceof Vehicle // true
```

Como puedes comprobar tú mismo, `motorcycle` sigue siendo un vehículo. El constructor subyacente no es algo que podamos modificar tras crear una instancia de un objeto, solo podemos hacerlo en tiempo de construcción del mismo objeto.


## Creando clases en JavaScript (ES5)
Una vez explicados los conceptos anteriores, ya tenemos la capacidad de crear clases en JavaScript. Esta es una manera (no es la única, pero sí una de ellas muy válida):

```javascript
//ES5

// Class definition / constructor
var Vehicle = function Vehicle(color) {
  // Initialization
  this.color = color;
}

// Instance methods
Vehicle.prototype = {
  go: function go() {
    return "Vroom!";
  }
}
```

## Subclases
La flexibilidad de JavaScript también nos permite crear algo muy cercano a lo que sería "herencia" en otros lenguajes de programación orientados a objetos, aunque con sus limitaciones.

```javascript
ES5
var Car = function Car() {};
Car.prototype = new Vehicle("tan");
Car.prototype.honk = function honk() { return "BEEP!" };
var car = new Car();
car.honk();             // "BEEP!"
car.go();               // "Vroom!"
car.color;              // "tan"
car instanceof Car;     // true
car instanceof Vehicle; // true
```
El problema con esta aproximación es que el constructor de `Vehicle` solo puede llamarse una vez: para configurar el prototipo de `Car`. Necesitamos asignar el color del coche en ese momento, así que no podemos tener distintos coches de distintos colores. Por eso no llega a ser una herencia pura, en el sentido más estricto del paradigma de orientación a objetos. Algunos *frameworks* de JavaScript han resuelto esto definiendo sus propias implementaciones de clase.