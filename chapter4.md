# Capítulo 4: Plantillas de cadenas de texto

La manipulación de **strings**, o cadenas de texto en JavaScript siempre ha estado algo verde respecto a las posibilidades que ofrecen otros lenguajes como Java o C#, por citar un par de ejemplos. 

Con ECMAScript 6 se ha tratado de dar respuesta a algunas de las necesidades más básicas de los programadores a la hora de trabajar con strings, introduciendo la característica de la **interpolación de plantillas de cadenas de texto**. Tremendo palabro para lo que a mi me gusta llamar coloquialmente *strings dinámicos*. Veamos unos ejemplos:

En ES5, si queríamos crear un string con contenido no estático, no había muchas formas mejores de hacerlo que la siguiente:

```javascript
// ES5
var dani = {
    name: "Daniel",
    age: 32
};

var greet = function(person) {
    return "Hello! My name is " + person.name + " and I'm " + dani.age + " years old";
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

También podemos disponer de strings de múltiples líneas, y pasar de esto:

```javascript
// ES5
var quijote = "En un lugar" +
" de la mancha" +
", de cuyo nombre" +
" no quiero acordarme";
```

A esto:

```javascript
// ES6
var quijote = `En un lugar
 de la mancha
, de cuyo nombre
 no quiero acordarme`;
```

## Plantillas de cadena de texto con postprocesador
Una forma más avanzada de plantillas de cadenas de texto son aquellas que contienen una función de postprocesado . Con ellas es posible modificar la salida de las plantillas, usando una función. El primer argumento contiene un array con las cadenas de texto de la plantilla ("Hola" y "mundo" en el ejemplo). El segundo y subsiguientes argumentos con los valores procesados ( ya cocinados ) de las expresiones de la plantilla (en este caso "15" y "50"). Finalmente, la función devuelve la cadena de texto manipulada. El nombre "tag" de la función no es nada especial, se puede usar cualquier nombre de función en su lugar.

```javascript
// ES6
var a = 5;
var b = 10;

function tag(strings, ...values) {
  console.log(strings[0]); // "Hola "
  console.log(strings[1]); // " mundo "
  console.log(values[0]);  // 15
  console.log(values[1]);  // 50

  return "Bazinga!";
}

tag`Hola ${ a + b } mundo ${ a * b}`;
// "Bazinga!"
```

    TODO: Mejorar los ejemplos y las descripciones. 
    
    TODO: Hablar de utilizar tags para i18n. 
    
    TODO: Completar con información de MDN: https://developer.mozilla.org/es/docs/Web/JavaScript/Referencia/template_strings
    
