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

Uno de los mayores problemas a los que nos hemos enfrentado siempre los desarrolladores de JavaScript es el conocido como **hoisting** ("elevación"). El término *hoisting*, el cual no está definido dentro del actual ECMAScript, es comúnmente utilizado para describir el particular comportamiento que JavaScript hace de las variables en el interior de las funciones.

Se entiende como *hoisting* el comportamiento por defecto de cualquier intérprete de javascript, que ubica cualquier variable declarada al comienzo de su contexto.

    TODO: definir contexto en javascript

Dicho funcionamiento ha sido ampliamente discutido por la comunidad de desarrolladores sobre si se trataba de un *bug* o una *feature*. Por citar un ejemplo, **John Resig**, creador de **jQuery**, es un poderoso aliado a la hora de gestionar los ámbitos que alcanzan nuestras variables. Sin embargo para la mayoría de nosotros, es una fuente irremediable de inconsistencias en nuestros códigos y errores potenciales difíciles de diagnosticar.

Por ejemplo, observemos el siguiente código:

```javascript
function foo(){
 bar();
 var x = 1;
}
```
Cuando dicho código pase a ser tratado por un intérprete de JavaScript, se convertirá en lo siguiente:
