# Promesas
> Un objeto **Promise** representa un valor que puede no estar disponible aún.

El objeto **Promise** se utiliza para realizar operaciones asíncronas. Típicamente, llamadas a sistemas remotos o a procesos que pueden demorarse y bloquear la ejecución de nuestro código.

La promesa representa un valor que no es necesario conocer en el momento en el que dicha promesa es creada. Nos permite asociar un *handler* a la acción asíncrona que eventualmente puede completarse con éxito o fallar por cualquier motivo. De este modo, los métodos asíncronos pueden retornar valores como si fuesen síncronos. De ahí el nombre de promesa: son métodos que *prometen* devolver un valor en algún momento del futuro.

## Sintaxis

```javascript
new Promise(function(resolve, reject) { ... });
```

El constructor de la promesa recibe una función de *callback*, que a su vez contiene dos argumentos que podremos llamar una vez que la operación se haya completado:

* **`resolve`**: Completa la promesa devolviendo el valor.
* **`reject`**: Rechaza la promesa.

Internamente una Promesa puede estar en uno de los siguientes tres estados:

* *pending*: El estado inicial, ni completada ni rechazada.
* *fullfilled*: Significa que la operación se ha completado con éxito.
* *rejected*: Significa que la operación ha fallado.

## Utilidad del uso de Promise
Las promesas son una forma fantástica de hacer tu código más limpio, reducir dependencias de librerías externas y simplificar el conocido *callback hell*, con el que tenemos que lidiar los que programamos en JavaScript tanto en lado del cliente como en servidor.

Para demostrar el problema con los *callbacks*, probaremos lo siguiente:
1. Ejecutar un código
2. Esperar un segundo
3. Ejecutar otro código
4. Esperar otro segundo
5. Ejecutar un tercer fragmento de código

Este es el patrón que normalmente utilizaríamos para hacer animaciones con CSS3. Lo implementaremos utilizando `setTimeout`, a modo ilustrativo:

```JavaScript
runAnimation(0);
setTimeout(function() {
  runAnimation(1);
  setTimeout(function() {
    runAnimation(2);
  }, 1000)
}, 1000);
```
Parece horrible, ¿verdad? Imagina una aplicación que requiere animaciones complejas, con 10 pasos en lugar de 3. La anidación de funciones de *callback* convertiría tu código en algo completamente ilegible y difícil de debugar. De hecho, es un problema tan peliagudo que se ha popularizado el uso de *callback hell* (el infierno de los *callbacks*) para definirlo. Las promesas vienen a poner fin a este infierno.



TODO: Completar con información de:
* https://www.promisejs.org/
* http://jamesknelson.com/grokking-es6-promises-the-four-functions-you-need-to-avoid-callback-hell/#exercise
