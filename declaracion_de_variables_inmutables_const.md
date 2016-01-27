# Declaración de variables inmutables: `const`

Hay dos formas de resolver el problema del **hoisting**: Acotando el ámbito de definición de las variables con `let` o impidiendo que una variable se modifique a lo largo del código. Para este último caso, se ha introducido la nueva palabra reservada `const`, que permite crear variables de solo lectura cuyo valor no puede ser modificado. Veamos un ejemplo:
```javascript
(function(){
    const HELLO = "hello world";
    HELLO = "hola mundo";
    // Dará ERROR, ya que es de sólo lectura
})();
```
En este ejemplo vemos cómo desde el momento en que declaramos la constante `HELLO`, su valor queda blindado y el intérprete lanzará error al tratar de modificarlo.
```javascript
(function() {
    const PI;
    PI = 3.15;
    // Dará ERROR, ya que ha de asignarse un valor en la declaración
})();
```

Por convención las variable inmutables las definiremos en mayúsculas.