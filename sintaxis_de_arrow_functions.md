# Sintaxis de arrow functions

El ejemplo más simple de *arrow function* es el siguiente, aunque veremos en los ejemplos siguientes que existen diversas variaciones.

```javascript
// ES6
const echo = text => text;
```

Esta función sería equivalente a la siguiente:

```javascript
// ES5
var echo = function(text) {
    return text;
};
```

En ambos casos, la ejecución de la función daría la siguiente salida:

```javascript
console.log(echo('Hola Mundo!')); // Hola Mundo!
```

Como con cualquier función, podemos pasar tantos argumentos como queramos a la función:

```javascript
const sum = (a, b) => a + b;
```