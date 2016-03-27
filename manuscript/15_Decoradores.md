# Decoradores

## Sintaxis
Quien haya programado en Java o C# seguro que sabrá que existen los atributos de clase, método o propiedad. Estos atributos son programables y modifican de alguna forma el objetivo sobre el que se colocan.
La sintaxis en esos lenguajes es muy similar a la que se ha escogido en JavaScript.

Para una clase:
```javascript
@anotation
class Vehicle { }
```

Para el método de una clase:
```javascript
class Vehicle{  
    constructor(){ }

    @fitipaldi
    run(){}
}
```

También es posible usarlo dentro de una propiedad de una clase:

```javascript
class Vehicle {  
    @uppercase
    get model(){
        return this._model
    }
}
```

## Cómo funciona
Un decorador es una función que intercepta la definición de propiedades de un objeto. Por lo tanto, permite modificar tal definición en tiempo de ejecución. 

Crearemos un decorador de la forma siguiente:

```javascript
const decorator = function ( target, name, descriptor);
```

Lo hace llamando a una función que recibe los mismos parámetros que Object.defineProperty(). Así, el decorador devuelve un objeto que se usará como definición de las propiedades.

El decorador toma tres argumentos:

* **Target**: El objeto al que queremos modificar su definición de propiedades
* **Name**: El nombre de la propiedad a modificar
* **Descriptor**: La descripción de la propiedad del objeto, que explica cómo esta se comporta. La descripción tiene los siguientes puntos:
configurable: si es true la propiedad puede ser modificada;
enumerable: si es true esta propiedad aparece cuando hagamos un for of del objecto;
** **value**: es el valor asociado a la propiedad. Puede ser desde un tipo simple hasta una función;
writable: indica si la propiedad puede ser cambiada con una asignación;
** **get**: si la propiedad es un getter del objeto, aquí podemos escribir una función. Lo devuelto por esa función se asociará al valor del atributo. En caso de no ser una función y ser undefined, se usará value, como vimos antes;
** **set**: similar a lo anterior, pero en este caso la función recibirá el nuevo valor del atributo.

Veamos un ejemplo:

Supón que quieres enviar un mensaje a la consola cada vez que un método es ejecutado. Para ello vamos a crear un decorador llamado logger. Como es un decorador, no es más que una función que recibe tres argumentos.

const logger = function( target, name, descriptor ){}  
De estos tres argumentos, el más importante es el descriptor, que es el que tenemos que devolver; es decir, devolveremos un objeto que sea similar al descriptor que nos ha llegado, pero con las modificaciones especificadas por el decorador:

const logger = function( target, name, descriptor ){  
  // Guardamos una referencia al generador de la función    
  const initializer = descriptor.initializer();

  // Creamos una copia del descriptor original
  let desc = Object.assign({}, descriptor)

  // Modificamos la copia para decorarlo con el log a consola
  desc.initializer = function(){
    return function(...args){
      console.log( `LOGGER: call ${name} with ${args}` )
      initializer.apply(this, args)
    }

  }

  // Devolvemos nuestro nuevo descriptor modificado
  return desc
}
Una vez hemos creado el decorador, solo tenemos que usarlo como hemos visto:

const mathematician = {  
  @logger
  add(first, second){
    console.log( `La suma es ${first + second}` );
  }
}

mathematician.add( 1, 2 )  
La salida de este script es la siguiente:

LOGGER: call add with 1,2  
La suma es 3  
No sé qué os parece a vosotros, pero a mí me parece una forma súper elegante de hacer un logger sobre los métodos que me puedan interesar de un objeto :)

Trabajando con clases
Los decoradores, como hemos visto, también se pueden usar con clases, tanto con algún método de la clase como con su propio constructor. Veamos un ejemplo donde hacemos que un método de una clase sea decorado para que devuelva un string en mayúsculas.

El decorador sería algo así:

const mayusculas = function( target, name, descriptor ){  
  const value = descriptor.value
  descriptor.value = function(){
    return value.apply(this, arguments).toUpperCase()
  }
  return descriptor
}
Devolvemos el objeto descriptor, reescribiéndole solo el atributo value, para que devuelva nuestra función decorada.

Si tuvieramos una clase, así es como lo usaríamos:

class Persona{  
  constructor( name ){
    this._name = name
  }

  @mayusculas
  saluda(){
    return `Hola, me llamo ${this._name}`
  }
}
const persona = new Persona('carlos')  
console.log( `${persona.saluda()}` )  
La salida que obtenemos con esto sería algo así:

HOLA, ME LLAMO CARLOS  
Dando incluso una vuelta de tuerca más, puesto que los decoradores no son más que funciones, también podemos pasarles argumentos a ellos mismos. Esto lo podemos observar en el siguiente ejemplo, donde decoramos el constructor de la clase.

const apellidos = function( apellidos ){  
  return function(Target){
    return class extends Target{
      get apellidos(){
        return apellidos
      }
    }
  }
}
Aquí nuestro decorador es una función que devuelve otra función. Puede sorprenderte que la función que devuelve no tenga los tres argumentos de los casos anteriores, pero eso es debido a que al decorar el constructor de una clase, el decorador solo recibe como úncio argumento el propio constructor. Dicho esto, podríamos usarlo de la siguiente forma:

@apellidos('Villuendas Zambrana')
class Persona{  
  constructor( name ){
    this._name = name
  }

  saluda(){
    return `Hola, me llamo ${this._name}`
  }
}

const persona = new Persona('carlos')  
console.log( `${persona.apellidos}` )  
Como salidas obtenemos:

Villuendas Zambrana  
Presta mucha atención a este último ejemplo, ya que será la piedra angular sobre la que montaremos el concepto de componentes de orden superior en ReactJS.

Bonus
Obviamente nada nos impide apilar los decoradores uno sobre otro e ir aplicándolos en serie. Con este nuevo decorador,

const dots = function( target, name, descriptor ){  
  const value = descriptor.value
  descriptor.value = function(){
    return value.apply(this, arguments).split('').join('.')
  }
  return descriptor
}
puedo crear el siguiente stack de decoración sobre un método:

class Persona{  
  constructor( name ){
    this._name = name
  }

  @mayusculas
  @dots
  saluda(){
    return `Hola, me llamo ${this._name}`
  }
}

const persona = new Persona('carlos')  
console.log( `${persona.saluda()}` )  
Esto nos daría como salida,

H.O.L.A.,. .M.E. .L.L.A.M.O. .C.A.R.L.O.S