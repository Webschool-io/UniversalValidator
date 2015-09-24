Um validador local ou via serviço(REST e Eventos) para  automatizar os testes poder validar no Frontend, na API, Model; emitindo eventos
ou requisições HTTP para validar.

Primeiramente vamos entender como seria um módulo de pessoa baseando-se no [Mongoose]()

Para utilizá-lo, uma ideia:

```js
var schema = {
  nome: {type: String, default: "", required: true, validate: validaNome},
  cpf: {type: String, default: "", required: true, validate: validaCPF},
  email: {type: String, default: "", required: true, validate: validaEmail}
};
var Validator = require(universal-validator)(schema);
```

Ou como serviço REST:


```js
var schema = {
  nome: {type: String, default: "", required: true, validate: validaNome},
  cpf: {type: String, default: "", required: true, validate: validaCPF},
  email: {type: String, default: "", required: true, validate: validaEmail}
};
var Validator = require(universal-validator)(schema, 'http://api.universalvalidator.com/meu-user'); //mas tb pode ser um localhost da vida
```

Nesse caso cada validação é atômica e unitária, pois acontece para apenas aquele campo sem nenhum efeito colateral.

Podemos utilizar eventos padrão como `beforeAction` e `afterAction`.

```js
Model.afterInsert = function() {
    EventEmitter.emit(afterInsert);
    // vai emitir o evento de afterInsert
    // onde o EventEmitter seria um tipo de Mediator de eventos
    // essse evento que irá chamar a função de validação
};
```

Por exemplo no `beforeSave` o model chamará a função `validate()` com regras de negocio do modulo.

A ideia principal é criar pequenos testes que possam ser re-usáveis e automatizados por um módulo/serviço, o UniversalValidator, para que possa ser utilizado em qualquer sistema escrito em qualquer linguagem, deixando os testes padronizados quando se trabalha com equipes de linguagens diferentes.

## Automatização