# Declaración de variables inmutables: `const`

<<<<<<< HEAD
Hay dos formas de resolver el problema del **hoisting**: Acotando el ámbito de definición de las variables con `let` o impidiendo que una variable se modifique a lo largo del código. Para este último caso, se ha introducido la nueva palabra reservada `const`, que permite crear variables de solo lectura cuyo valor no puede ser modificado. Veamos un ejemplo:
=======
Hay dos formas de resolver el problema del **hoisting**: Acotando el ámbito de definición de las variables con `let` o impidiendo que una variable se modifique a lo largo del código. Para este último caso, se ha introducido la nueva palabra reservada `const`, que permite crear variables de solo lectura cuyo valor no puede ser modificado. 

Veamos un ejemplo:
>>>>>>> 2edad64074821198e6e56b089a60a0725c03bf07

```javascript
(function(){
    const HELLO = 'hello world';
    HELLO = 'hola mundo';
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
<<<<<<< HEAD
```

Por convención las variable inmutables las definiremos en mayúsculas.
=======
```
>>>>>>> 2edad64074821198e6e56b089a60a0725c03bf07
