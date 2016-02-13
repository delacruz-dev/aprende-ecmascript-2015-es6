# Capítulo 10: Object literals

Los "literales de objetos", u *object literals* en JavaScript se definen como una lista de pares de clave valor rodeados por corchetes:

```javascript
var myObject = {
    name: 'Daniel',
    age: 32,
    married: true
}
```
En lenguaje coloquial, a mi me gusta llamar a este conjunto simplemente un *plain object*, u objeto plano y a los *object literals*, propiedades. Pero no se lo digas a nadie ;-)

Los *object literals* pueden ser de cualquier tipo de datos, incluyendo arrays, funciones e incluso otros *object literals* anidados. He aquí otro ejemplo un tanto más complejo.

```javascript
var mySuperCoolObject = {
    images: ["one.gif", "two.gif", "three.gif", "four.gif"],
    location: {
        x: 40.8374,
        y: 300.1771
    },
    move: function(x, y) {
        this.location.x += x;
        this.location.y += y;
    }
};
```

## Novedades en ECMAScript 6
En Javascript, los métodos no son más que propiedades cuyos valores son funciones.

En ES5, los métodos son creados del mismo modo que cualquier otra propiedad, utilizando un literal de objeto:

```javascript
// ES5
var myObject = {
    foo: function() {
        ...
    }
}
```

En ECMAScript 6 se ha introducido una sintaxis especial para definir métodos:

```javascript
// ES6
const myObject = {
    foo() {
        ...
    },
    bar(x, y) {
        ...
    }
}
```

### Nombres de propiedades dinámicos, o computados
En ECMAScript 5 solo teníamos una forma de especificar una clave cuando creábamos una propiedad: mediante un nombre fijo:

```javascript
// ES5
object.foo = true;
```

En ES6 también podemos hacerlo de forma dinámica, o computada:

```javascript
// ES6
const propertyKey = 'foo';
const object = {
    [propertyKey]: true,
    [`b${ar}`]: 123
};
```

Esta nueva sintaxis también sirve para definiciones de métodos:

```javascript
// ES6
const methodKey = 'greeting';
const object = {
    [methodKey]() {
        return 'Hello!';
    }
};
```

### Getters y setters
Los `getters` y `setters` continúan funcionando exactamente igual que en ES5, aunque con la nueva sintaxis han terminado siendo prácticamente iguales que las definiciones de métodos:

```javascript
const obj = {
    get foo(){
        console.log('GET foo');
        return 123;
    }
    set bar(value){
        console.log(`SET bar to ${value}`);
    }
}
```

