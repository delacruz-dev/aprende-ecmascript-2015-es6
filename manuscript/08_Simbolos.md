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

El hecho de utilizar una descripción para la creación un símbolo, no significa que el símbolo creado contenga ese string. Se crea un símbolo nuevo cada vez, aunque se utilice la misma descripción. De este modo, dos símbolos con la misma descripción no son iguales:

```javascript
Symbol("foo") === Symbol("foo"); //false
```

Tampoco tiene sentido utilizar la palabra reservada `new` para crear un símbolo:

```javascript
var symbol = new Symbol(); // TypeError
```

