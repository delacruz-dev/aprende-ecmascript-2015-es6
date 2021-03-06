# Clases

El paradigma de orientación a objetos es algo que siempre ha generado gran controversia entre la comunidad de desarrolladores Javascript. Si bien muchos defienden la programación funcional reactiva más pura, lo cierto es que Javascript siempre se ha definido como un lenguaje de programación orientado a objetos, así que ambas abstracciones son válidas.

A día de hoy, con la introducción de ECMAScript 2015 la controversia sigue vigente, sobre todo desde la introducción de la palabra reservada `class` en el lenguaje. Toda una declaración de intenciones.

Y no es justo ahora vayamos a poder utilizar clases en Javascript: ya era algo que podíamos hacer en versiones anteriores del estándar. Pero con una sintaxis mucho menos intuitiva.

En este capítulo nos detendremos a refrescar algunos conceptos que ya eran vigentes en ECMAScript 5, antes de ver cómo creamos las mismas estructuras de código en la versión 6 del estándar.

## Sintaxis básica de declaración de clases
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
```

Si obtienes el tipo de la clase `Point`, te darás cuenta de que es no es más que una función.

```javascript
typeof Point; // function
```

A diferencia de las funciones constructoras, no podemos utilizarla directamente. En su lugar, tenemos que crear una instancia utilizando `new`: 

```javascript
Point();
> TypeError: Classes can’t be function-called
```

## Sintaxis de declaración de subclases
La forma de hacer subclases sería la siguiente:

```javascript
class ColorPoint extends Point {
    constructor(x, y, color) {
        super(x, y);
        this.color = color;
    }
    toString() {
        return `${super.toString()} in ${this.color}`;
    }
}

const cp = new ColorPoint(25, 8, 'green');
cp.toString(); // (25, 8) in green
cp instanceof ColorPoint // true
cp instanceof Point // true
```
La "herencia" de propiedades de la clase se realiza mediante la palabra reservada `extends`. Esto provoca que el nuevo objeto instanciado sea tanto del tipo asignado como del tipo heredado.

En el constructor, mediante la sentencia `super()` se llama a la función constructora de la clase padre.

## El cuerpo de una definición de clase
El cuerpo de una clase solo puede contener métodos. Los prototipos que tienen propiedades contenedoras de datos generalmente se consideran un antipatrón, así que esta particularidad de las clases solo refuerza que se siga esta buena práctica.

Los tipos de métodos que puede contener el cuerpo de una función son:

* constructor
* métodos estáticos
* métodos de prototipo

```javascript
class Sample{
    constructor(value){
        this.value = value;
    }
    static staticMethod(){
        return 'this is a class method';
    }
    prototypeMethod(){
        return 'this is a prototype method';
    }
}

const sample = new Sample(123);
```

### Método constructor de clase
No es más que una función constructora, tal y como ya existían en ES5. Sin embargo, el constructor de una clase tiene la particularidad de poder llamar a `super`, lo cual nos da la ventaja de poder inicializar las propiedades de la clase padre (o "superclase"). Algo que no era posible con el estándar anterior del lenguaje.

```javascript
// ES6
class Example extends Sample {
    constructor(key, value){
        super(value);
        this.key = key;
    }
}

const example = new Example(987, 123);
example// Example { value: 123, key: 987 }
```

### Métodos estáticos
Las propiedades estáticas, o propiedades de clase, son propiedades de la propia clase, por lo tanto no necesitan de una instancia para ser utilizados, a diferencia de los métodos de prototipo:

```javascript
Sample.staticMethod(); // this is a class method
Sample.prototypeMethod();// TypeError: Sample.prototypeMethod is not a function
```

### Métodos de prototipo
En contraposición a los métodos estáticos, los métodos de prototipo son heredados por todas las instancias de la clase:

```javascript
const sample = new Sample();
sample.prototypeMethod(); // this is a prototype method
sample.staticMethod(); //TypeError: sample.staticMethod is not a function
```

Fíjate que los métodos estáticos no se transmiten a las instancias de la clase.