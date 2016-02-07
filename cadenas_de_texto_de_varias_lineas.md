# Cadenas de texto de varias líneas

Podemos disponer de strings de múltiples líneas, y pasar de esto:

```javascript
// ES5
var text = ['En un lugar', 'de la mancha,', 'de cuyo nombre', 'no quiero acordarme'].join('\n');
```

A esto:

```javascript
// ES6
var quijote = `En un lugar
 de la mancha, 
 de cuyo nombre
 no quiero acordarme`;
```