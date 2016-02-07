# Desestructuración de objetos
```javascript
var persona = {nombre: 'Dani', apellidos: 'de la Cruz'};
var {nombre, apellidos} = persona;

console.log(nombre); // Dani
console.log(apellidos); // de la Cruz
```

Tal y como puedes ver, podemos crear variables al vuelo a partir de un objeto de Javascript, para luego utilizarlas. Las nuevas variables tendrán por defecto el nombre que tenían las propiedades del objeto. Pero, ¿qué pasa si no nos gusta y queremos cambiarlo? En el ejemplo, no es demasiado correcto utilizar nombres de variables en castellano...

Bueno, en esta vida casi todo tiene arreglo:

```javascript
// ES6
var {nombre: name, apellidos: surname} = persona;
console.log(name); // Dani
console.log(surname); // de la Cruz
```

Este comportamiento es especialmente útil a la hora de pasar parámetros a funciones, como veremos a continuación.

```javascript
// ES6
function suma({a, b} = {}) {
  return a + b;
};

var a = 2;
var b = 3;
console.log(suma({a, b}));
```