# El operador de propagación para propiedades de objetos

No quería dejar de hablar de una de las funciones más útiles del operador de propagación: la posibilidad de utilizarlo con propiedades de objetos.

Aunque sea una propuesta para la siguiente versión del estándar (ECMAScript 2016 o ES7), en el momento de escribir estas líneas se encuentra en **Stage 2**, así que es bastante seguro comenzar a utilizarlo desde hoy mismo gracias a la potencia de Babel.

Como podemos ver en el siguiente ejemplo, el [operador de propagación para propiedades de objetos](https://github.com/sebmarkbage/ecmascript-rest-spread) resulta muy útil para añadir nuevas propiedades a un objeto, o sobreescribirlas al vuelo: 

```javascript
const worker = {
  id: 1337,
  name: 'John',
  surname: 'Woo',
  age: 35,
  job: 'UI designer'
};

const f = function({worker} = {}){
  return {
    ...worker,
    fullName: `Mr./Mrs. ${worker.surname}, ${worker.name}`,
    age: `${worker.age} years old`
  };
};

console.log(f({worker}));
```

El objeto que devuelve la consola tendrá la nueva propiedad `fullName` y también habrá cambiado el tipo de la propiedad `age` a algo más legible. Pero como utilizamos el operador de propagación, también tendrá el resto de propiedades del objeto `worker`.