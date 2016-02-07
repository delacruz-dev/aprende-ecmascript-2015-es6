# Interpolación de parámetros en plantillas de cadenas de texto

En ES5, si queríamos crear un string con contenido no estático, no había muchas formas mejores de hacerlo que la siguiente:

```javascript
// ES5
var dani = {
    name: 'Daniel',
    age: 32
};

var greet = function(person) {
    return 'Hello! My name is ' + person.name + ' and I\'m ' + person.age + ' years old';
};

greet(dani);
```

Sin embargo, con ES2015 ahora podemos convertir la función `greet` en:

```javascript
// ES6
var greet = function(person) {
    return `Hello! My name is ${person.name} and I'm ${person.age} years old`;
};
```

Esto tiene una ventaja añadida: la de poder hacer sustituciones no solo por un valor, sino por cualquier expresión válida en JavaScript dentro de los símbolos de interpolación:

```javascript
let myAge = `Mi edad es ${person.age + 3} años`;
```