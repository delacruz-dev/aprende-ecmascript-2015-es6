# Declaración de variables de ámbito local: `let`

La sentencia `let` declara una variable de alcance local, la cual, opcionalmente, puede ser inicializada con algún valor.

El alcance de `let` es local al bloque, declaración o expresión donde se está usando. Lo anterior diferencia la expresión `let` de la palabra reservada `var`, la cual define una variable global o local en una función sin importar el ámbito del bloque.

Veamos algunos ejemplos:

```javascript
if(x > y) {
    let gamma = 12.7 + y;
    i = gamma * x;
}
````

En el ejemplo anterior, `gamma` solo existe dentro del bloque del `if`.

```javascript
for(let i = 0; i < students.length; i++){
    console.log(students[i].name);
}
```

Podemos utilizar `let` para que la variable sea local al alcance del bucle `for`. Si en su lugar usáramos `var`, la variable sería visible en toda la función que contiene dicho bucle.

```javascript
(function() {
    if(true){
        let x = "hola mundo";
    }
    console.log(x);
}
```

En el ejemplo anterior, la sentencia `console.log` da error, porque `x` ha sido definida dentro del bloque `if`.