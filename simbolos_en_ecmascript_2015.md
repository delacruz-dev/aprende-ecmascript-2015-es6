# Símbolos en ECMAScript 2015

Los símbolos son uno tipo primitivo en ECMAScript 2015. Un símbolo es un tipo de dato **único** e **inmutable** que puede ser utilizado como identificador para propiedades de objetos. 

## Sintaxis

```javascript
Symbol([description]);
```
### Parámetros
#### description `optional`
De tipo string, opcional. Una descripción del símbolo que puede ser utilizada para depurar, pero no para acceder al propio símbolo.

## Uso
Para crear un nuevo símbolo primitivo, simplemente escribimos `Symbol()` con un parámetro opcional de tipo string como cadena de texto a modo de descripción.

```javascript
var symbol = Symbol();
var anotherSymbol = Symbol("another");
```

