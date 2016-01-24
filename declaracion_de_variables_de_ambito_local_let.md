# Declaración de variables de ámbito local: `let`

Ahora con ECMAScript 6 podemos declarar variables utilizando la palabra reservada `let` en lugar de `var` si no queremos que sean accesibles más allá de un ámbito. Por ejemplo:

```javascript
(function() {
    if(true){
        let x = "hola mundo";
    }
    console.log(x);
    // Da error, porque "x" ha sido definida dentro del "if"
}
```