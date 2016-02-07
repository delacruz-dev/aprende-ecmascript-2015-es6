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