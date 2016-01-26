# Instalación básica de Babel

## `babel-cli`
El intérprete de línea de comandos **Babel CLI** es una herramienta simple que nos permite compilar archivos con Babel desde nuestro terminal.

Puede instalarse globalmente para tenerlo disponible en cualquier directorio que lo necesitemos, aunque si pensamos en distribuir nuestros proyectos *open source*, es preferible instalarlo a nivel local. En este ejemplo lo haremos de la segunda forma.

### Creando un entorno de pruebas
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

No te preocupes demasiado por entender la sintaxis, ya que la trabajaremos más adelante en detenimiento. Simplemente ten en cuenta que al ejecutar el código en la consola de Node.JS, debería darte el cuadrado de 2, o sea: 4.

### Instalando babel-cli como un script de npm
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

Una vez añadida, ya tendremos una tarea de NPM que podremos ejecutar desde consola para compilar el código. Ejecuta el siguiente comando:

```terminal
$ npm run babel
```

Esto debería producir la siguiente salida de consola:

```terminal
$ npm run babel

> my-dir@1.0.0 babel /path/to/my-dir
> babel my-file.js

const square = n => n * n;
console.log(square(2));
```

### Especificar un archivo de salida
Como verás, se imprime por consola el contenido de tu archivo. Esto tiene escasa utilidad, más allá de comprobar que efectivamente, `babel-cli` está funcionando. Si en lugar de la consola queremos que el *output* tenga como destino un archivo de destino, modificaremos el script en nuestro `package.json` con lo siguiente:

```json
{
    "scripts": {
        "babel": "babel my-file.js --out-file compiled.js"
    },
}
```

En esta ocasión, hemos indicado el nombre del archivo de destino con el modificador `--out-file` (también serviría simplemente `-o`. Si volvemos a ejecutar la tarea `npm run build`, deberíamos observar la siguiente salida en la consola:

```terminal
$ npm run babel

> my-dir@1.0.0 babel /path/to/my-dir
> babel my-file.js --out-file compiled.js
```
Además, en esta ocasión se habrá creado un nuevo archivo `compiled.js` con el contenido del archivo original. Todavía no estamos aplicando ninguna transformación.

### Compilar todo el contenido de una carpeta

Si nuestra aplicación crece, es normal que tengamos varios módulos, así que es poco habitual que solamente compilemos un único archivo. Para especificar todo un directorio, modificaremos nuestro script en el `package.json` de esta manera:

```json
{
    "scripts": {
        "babel": "babel src --out-dir lib"
    },
}
```

Si organizamos todo el código de nuestra aplicación bajo la carpeta `src`, este script compilará todo lo que encuentre y lo escribirá en la carpeta `lib`. Los nombres de carpetas son totalmente arbitrarios, podéis elegir el que más os guste.

## Configuración de Babel

Hasta ahora hemos preparado un entorno para compilar nuestros archivos con Babel, pero realmente no estamos haciendo ninguna transformación al código. Eso se debe a que todavía no le hemos dicho a Babel que haga nada en concreto.

Desde la publicación de Babel 6, esta funcionalidad se ha extraído del núcleo de Babel para ofrecerse como paquetes por separado, a los que sus creadores llaman *presets*. Dichos *presets* son muy específicos y hacen que la herramienta sea mucho más modular y extensible. 

Así que si queremos trabajar con ECMAScript 6, deberemos instalar el preset correspondiente. Lo haremos mediante la siguiente instrucción de línea de comandos:

```terminal
$ npm install --save-dev babel-preset-es2015
```

Ahora, todo lo que necesitamos es crear un fichero `.babelrc` en la raíz de nuestro proyecto y añadir la siguiente configuración:

```json
{
    "presets": [ "es2015" ],
    "plugins": []
}
```

Si lo preferimos, esta configuración puede ir directamente en el `package.json` de la siguiente forma:

```json
"babel": {
    "presets": [ "es2015" ],
    "plugins": []
}
```

Como consejo, te diría que intentes mantener el archivo `package.json` lo más limpio posible y pongas la configuración de Babel en su propio archivo de configuración, ya que el `package.json` tiene bastantes cosas de por si. Aunque es una elección personal.

Una vez configurado, si ejecutamos nuestra tarea de compilación, observaremos un resultado muy distinto en el fichero generado:

```javascript
"use strict";

var square = function square(n) {
  return n * n;
};
console.log(square(2));
```

Como verás, se ha transformado el código ECMAScript 6 en un código de ECMAScript 5 que será compatible con la gran mayoría de navegadores del mercado y además es muy legible.

A partir de ahora, ya podemos incorporar la sintaxis ES2015 a nuestros proyectos, pues tan solo con incluir Babel en nuestro flujo de trabajo podremos desplegar código compatible con cualquier cliente sin preocuparnos por ello.