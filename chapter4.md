# Capítulo 4: Plantillas de cadenas de texto

La manipulación de **strings**, o cadenas de texto en JavaScript siempre ha estado algo verde respecto a las posibilidades que ofrecen otros lenguajes como Java o C#, por citar un par de ejemplos. 

Con ECMAScript 6 se ha tratado de dar respuesta a algunas de las necesidades más básicas de los programadores a la hora de trabajar con strings, introduciendo la característica de la **interplación de plantillas de cadenas de texto**. Tremendo palabro para lo que a mi me gusta llamar coloquialmente *strings dinámicos*. Veamos unos ejemplos:

En ES5, si queríamos crear un string con contenido no estático, no había muchas formas mejores de hacerlo que la siguiente:

```javascript
var dani = {
    name: "Daniel",
    age: 32
};

var greet = function(person){
    return "Hello! My name is " + person.name + " and I'm " + dani.age + " years old";
};

greet(dani);
```

Sin embargo, con ES2015 ahora podemos convertir la función `greet` en:
```javascript
var greet = function(person){
    return "Hello! My name is ${person.name} and I'm ${person.age} years old";
};
```
También podemos disponer de strings de múltiples líneas, y pasar de esto:
```javascript
var quijote = "En un lugar" +
" de la mancha" +
", de cuyo nombre" +
" no quiero acordarme";
```
A esto:
```javascript
var quijote = "En un lugar
 de la mancha
, de cuyo nombre
 no quiero acordarme";
```
