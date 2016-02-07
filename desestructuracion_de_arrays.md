# Desestructuración de Arrays

```javascript
var numbers = ["1", "2", "3"];

// without destructuring
const one   = foo[0];
const two   = foo[1];
const three = foo[2];

// with destructuring
var [one, two, three] = foo;
```

Podemos asignar de forma desestructurada sin una declaración en la asignación:

```javascript
var one, two;
[one, two] = [ "1", "2"];
```

Yendo un poco más allá, podemos utilizar funciones para devolver un conjunto de valores y asignarlos de forma desestructurada:

```javascript
function f() {
    return ["1", "2"];
}
```

De este modo podemos devolver cualquier número de valores de forma arbitraria. Hasta aquí ninguna novedad, pero si utilizamos la asignación desestructurada:

```javascript
var one, two;
[one, two] = f();
console.log(one, two); // 1, 2
```

La asignación de variables se realiza en orden, el primer valor se asigna a la primera variable, el segundo a la segunda... y así.
