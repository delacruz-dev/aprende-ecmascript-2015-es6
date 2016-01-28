# Capítulo 4: Plantillas de cadenas de texto

La manipulación de **strings**, o cadenas de texto en JavaScript siempre ha estado algo verde respecto a las posibilidades que ofrecen otros lenguajes como Java o C#, por citar un par de ejemplos. 

Con ECMAScript 6 se ha tratado de dar respuesta a algunas de las necesidades más básicas de los programadores a la hora de trabajar con strings, introduciendo la característica de las **plantillas de cadenas de texto**. 

## Sintaxis
El constructor de una plantilla de texto se invoca delimitando la string con (` ` `). Es decir, lo que antes de ES2015 hubiese sido:

```javascript
var hello = 'Hola Mundo';
// o bien
var hello = 'Hola Mundo';
```

Ahora puede expresar con:

```javascript
let hello = `Hola Mundo`;
```

## Strings de múltiples líneas
También podemos disponer de strings de múltiples líneas, y pasar de esto:

```javascript
// ES5
var text = ['En un lugar', 'de la mancha,', 'de cuyo nombre', 'no quiero acordarme'].join("\n");
```

A esto:

```javascript
// ES6
var quijote = `En un lugar
 de la mancha, 
 de cuyo nombre
 no quiero acordarme`;
```

## Interpolación

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

## Funciones de posprocesado
Sin duda la auténtica potencia de los nuevos *template strings* que permite utilizar ES2015 se hace evidente cuando utilizamos las funciones de posprocesado.

Dichas funciones nos permiten procesar la cadena de texto antes de que sea consumida por el cliente.

```javascript

function tag(strings, ...values) {
    
}
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
    
