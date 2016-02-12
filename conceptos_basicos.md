# Conceptos básicos

El siguiente fragmento de código ilustra cómo definiríamos una clase en JavaScript.

```javascript
class Point {
    constructor(x, y) {
        this.x = x;
        this.y = y;
    }
    toString() {
        return `(${this.x}, ${this.y})`;
    }
}
```

Esta definición de clase nos permite utilizarla como cualquier otra función constructor en ES5:

```javascript
var p = new Point(25, 8);
p.toString(); //(25, 8)
````

Si obtienes el tipo de la clase `Point`, te darás cuenta de que es no es más que una función.

```javascript
typeof Point; // function
```

A diferencia de las funciones constructoras, no podemos utilizarla directamente. En su lugar, tenemos que crear una instancia utilizando `new`: 

```javascript
Point();
> TypeError: Classes can’t be function-called
```