# Conceptos previos

## Qué es un constructor?
Básicamente un constructor es cualquier función que se utiliza como un constructor. ¿Perogrullada? Estoy seguro, pero es que un constructor no tiene nada de especial hasta que no se utiliza como tal. Esta definición es válida independientemente del lenguaje de programación con el que trabajemos. Veamos un ejemplo de función constructor:

```javascript
var Vehicle = function Vehicle() {
    console.log('¡Sólo soy una función!');
    // ...
}

var vehicle = new Vehicle();
```

La función Vehicle es una función normal, pero cuando la utilizamos mediante la palabra reservada `new`, además de ejecutar el código del cuerpo de la función, JavaScript hace que pasen cuatro cosas:

1. Se crea un nuevo objeto
2. Establece la propiedad `constructor` del objeto a la función `Vehicle`
3. Configura el objeto para delegar en `Vehicle.prototype`
4. Llama a `Vehicle()`en el contexto del nuevo objeto

El resultado de `new Vehicle()` es este nuevo objeto.

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