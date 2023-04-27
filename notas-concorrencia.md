# revisão sobre concorrencia

concorrente e paralela;

## historico

- 50's 2000's
- win 95 - mono processador
- 2003 - pentium dual core
- 2006 - classe java nio (sun)
- 2013 - usage nio / nodejs

```js
const contador = 1 // race condition
soma(contador, 100)
    .then(_ => soma(contador, 10))
    
// imperativo e bloqueante
criarUsuario(name: "batatinha")
criarPerfil()

// reativo / nonblocking
criarUsuario(name: "batatinha")
    .then(_ => criarPerfil())
```


