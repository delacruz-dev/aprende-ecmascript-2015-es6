# Capítulo 5: Desestructuración

## Desestructuración de arrays

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

## Desestructuración de objetos
```javascript
var persona = {nombre: 'Dani', apellidos: 'de la Cruz'};
var {nombre, apellidos} = persona;

console.log(nombre); // Dani
console.log(apellidos); // de la Cruz
```

Tal y como puedes ver, podemos crear variables al vuelo a partir de un objeto de Javascript, para luego utilizarlas. Las nuevas variables tendrán por defecto el nombre que tenían las propiedades del objeto. Pero, ¿qué pasa si no nos gusta y queremos cambiarlo? En el ejemplo, no es demasiado correcto utilizar nombres de variables en castellano...

Bueno, en esta vida casi todo tiene arreglo:

```javascript
var {nombre: name, apellidos: surname} = persona;
console.log(name); // Dani
console.log(surname); // de la Cruz
```
