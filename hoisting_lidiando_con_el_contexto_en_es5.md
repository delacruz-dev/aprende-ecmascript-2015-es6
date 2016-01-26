# Hoisting: Lidiando con el contexto en ECMAScript 5

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

Uno de los mayores problemas a los que nos hemos enfrentado siempre los desarrolladores de JavaScript es el conocido como **hoisting** ("elevación"). El término *hoisting*, el cual no está definido dentro del actual ECMAScript, es comúnmente utilizado para describir el particular comportamiento que JavaScript hace de las variables en el interior de las funciones.

Se entiende como *hoisting* el comportamiento por defecto de cualquier intérprete de JavaScript, que ubica cualquier variable declarada al comienzo de su contexto.

    TODO: definir contexto en javascript. Recursos:
    http://ryanmorr.com/understanding-scope-and-context-in-javascript/
    https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/this

Dicho funcionamiento ha sido ampliamente discutido por la comunidad de desarrolladores sobre si se trataba de un *bug* o una *feature*. Por citar un ejemplo, **John Resig**, creador de **jQuery**, es un poderoso aliado a la hora de gestionar los ámbitos que alcanzan nuestras variables. Sin embargo hay otros que pensamos que se trata de una fuente irremediable de inconsistencias en nuestros códigos y errores potenciales difíciles de diagnosticar.

Por ejemplo, observemos el siguiente código:

```javascript
function foo(){
    bar();
    var x = 1;
}
```

Cuando dicho código pase a ser tratado por un intérprete de JavaScript, se convertirá en lo siguiente:

```javascript
function foo(){
    var x;
    bar();
    x = 1;
}
```

Algo que podría parecer trivial, puede llegar a ocasionar comportamientos no esperados:

```javascript
var x = 'Hello World'; // variable global
 
(function foo() {
 console.log(x); // esperamos el valor global
 var x = 'New Value'; // redefinimos la variable en contexto local
 console.log(x);  // esperamos el nuevo valor local
})();
```

En el ejemplo anterior, declaramos la variable `x` en el contexto global. Dentro de la función `foo()`, se define un nuevo contexto, local a la función declarada. En la primera sentencia esperamos que la consola imprima `Hello World`, para después re-definir el valor de `x` y volverla a imprimir por consola, esta vez con el nuevo valor: `New Value`. Sin embargo, lo que ocurre es lo siguiente:

```terminal
> undefined
> New Value
```

¿Qué ha ocurrido? Por qué el intérprete imprime un `undefined` en lugar del esperado `Hello World`?

La respuesta, como te imaginarás, es el **hoisting**. Al crear un nuevo contexto de función, la declaración de la variable se eleva hasta el inicio del nuevo contexto, quedando la función tal que así:

```javascript
var x = 'Hello World';
 
(function foo(){
 var x;
 console.log( x );
 x = 'New Value';
 console.log( x );
})();
```

Como ves, `x` se *define* antes de la primera impresión por consola, sobrescribiendo el valor asignado en contexto global. Sin embargo, no es hasta después del primer `console.log` cuando se le asigna el nuevo valor.

Esto, como imaginarás, genera todo tipo de inconsistencias en el código de aplicaciones complejas que obligan a pensar dos veces dónde declarar y asignar valores a nuestras variables. 

Por este motivo, se dice que es una buena práctica declarar las variables al principio del contexto, ya que así además incrementamos la legibilidad del código. 

