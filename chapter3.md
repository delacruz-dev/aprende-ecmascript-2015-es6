# Capítulo 3: Variables de ámbito local: `let` y `const`

Tomemos como ejemplo la siguiente función en ES5:

```javascript
(function() {
    console.log(x); // x no está definida aún.
    if(true) {
        var x = "hola mundo";
    }
    console.log(x);
    // Imprime "hola mundo", porque "var" hace que la variable sea global a la función
})();
```

Uno de los mayores problemas a los que nos hemos enfrentado siempre los desarrolladores de JavaScript es el conocido como **hoisting**. El término *hoisting*, el cual no está definido dentro del actual ECMAScript, es comunmente utilizado para describir el particular comportamiento que JavaScript hace de las variables en el interior de las funciones.
