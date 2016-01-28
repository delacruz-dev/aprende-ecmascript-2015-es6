# Declaración de variables de ámbito local: `let`

Ahora con ECMAScript 6 podemos declarar variables utilizando la palabra reservada `let` en lugar de `var` si no queremos que sean accesibles más allá de un ámbito. Por ejemplo:

```javascript
(function() {
    if(true){
        let x = 'hola mundo';
    }
    console.log(x);
    // Da error, porque "x" ha sido definida dentro del "if"
})();
```

A diferencia de ECMAScript 5, en ESCMAScript 6 el bloque de una sentencia condicional también actúa como ámbito de bloque. En el ejemplo `console.log(x)` no tiene acceso a `let x = "hola mundo"`.

En el siguiente ejemplo la consola imprime `Hola Dani`, ya que la variable `x` en el bloque del `if` se mantiene dentro de su ámbito.

```javascript
(function() {
    let x = 'Hola Dani';
    
    if(true) {
        let x = 'Hola Joan';
    }
    console.log(x);
    // Imprime en consola Hola Dani
})();
```