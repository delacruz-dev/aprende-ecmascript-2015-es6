# Promesas
> Un objeto **Promise** representa un valor que puede no estar disponible aún.

El objeto **Promise** se utiliza para realizar operaciones asíncronas. Típicamente, llamadas a sistemas remotos o a procesos que pueden demorarse y bloquear la ejecución de nuestro código.

La promesa representa un valor que no es necesario conocer en el momento en el que dicha promesa es creada. Nos permite asociar un *handler* a la acción asíncrona que eventualmente puede completarse con éxito o fallar por cualquier motivo. De este modo, los métodos asíncronos pueden retornar valores como si fuesen síncronos. De ahí el nombre de promesa: son métodos que *prometen* devolver un valor en algún momento del futuro.

## Sintaxis

```javascript
new Promise(function(resolve, reject)) { ... });
```

El constructor de la promesa recibe una función de *callback*, que a su vez contiene dos argumentos que podremos llamar una vez que la operación se haya completado:

* **`resolve`**: Completa la promesa devolviendo el valor.
* **`reject`**: Rechaza la promesa.

Internamente una Promesa puede estar en uno de los siguientes tres estados:

* *pending*: El estado inicial, ni completada ni rechazada.
* *fullfilled*: Significa que la operación se ha completado con éxito.
* *rejected*: Significa que la operación ha fallado.

Imagina una llamada a una API asíncrona.
