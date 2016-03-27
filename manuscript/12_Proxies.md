# Proxies
Los proxies te permiten interceptar y personalizar operaciones realizadas en los objetos. Son una característica de _metaprogramación_.

En el siguiente ejemplo, `proxy` es el objeto cuyas operaciones estamos interceptando y el `handler` es el objeto que maneja dichas intercepciones. En este caso, solamente estamos interceptando una única operación: `get`:

```javascript
const target {};
const handler = {
    get(target, propKey, receiver) {
        console.log(`get ${propKey}`);
        return 'hello';
    }
}

const proxy = new Proxy(target, handler);

console.log(proxy.foo); 
// get foo
// hello
```