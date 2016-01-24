# Instalación de Babel

## `babel-cli`
El intérprete de línea de comandos **Babel CLI** es una herramienta simple que nos permite compilar archivos con Babel desde nuestro terminal.

Puede instalarse globablmente para tenerlo disponible en cualquier directorio que lo necesitemos, aunque si pensamos en distribuir nuestros proyectos *open source*, es preferible instalarlo a nivel local. En este ejemplo lo haremos de la segunda forma.

Para comenzar, abrimos una nueva sesión de terminal del sistema e inicializamos un nuevo repositorio de npm:

```terminal
$ npm init -y
```

Esto debería crear la siguiente estructura de archivos en el directorio:

```terminal
.
├── node_modules
└── package.json
```

Una vez creado el repositorio, añadiremos un nuevo archivo:

```terminal
$ touch my-file.js
```

Y copiaremos el siguiente código:

```javascript
const square = (n) => n * n;
console.log(square(2));
```

No te preocupes demasiado por entender la sintaxis, ya que la trabajaremos más adelante en detenimiento. Simplemente ten en cuenta que al ejecutar el código en la consola de Node.JS, debería daarte el cuadrado de 2, o sea: 4.

Volviendo a Babel, el archivo que acabamos de crear nos servirá para mostrar el resultado de una compilación de ES6 a ES5.

Pero antes tenemos que instalarlo y configurarlo como uno de los scripts de `npm` de nuestro proyecto. Para instalarlo, escribe:

```terminal
$ npm install --save-dev babel-cli
```

Y luego, en el archivo `package.json`, añadiremos la siguiente línea:

```json
{
    "scripts": {
        "babel": "babel my-file.js"
    },
 }
```

    TODO: Completar con información del Babel Handbook: https://github.com/thejameskyle/babel-handbook/blob/master/translations/es-ES/user-handbook.md