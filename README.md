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

alias achoq  antes as validações atomicas de cada campo
tipo no mongoose
a ideia eh criar um validador atomico
q os testes sejam re-usaveis
igual progração funcional
q q c acha?
ou eu sou mto louco?
pq assim
eu ja sei de cabeça varios testes q vc temq  fazer SEMPRE
Itacir Pompeu
2:42pm
Itacir Pompeu
pompeulimp@gmail.com
Eu ta passei ja

Nossa
Show, net aki ta osso
Jean Carlo Nascimento
2:43pm
Jean Carlo Nascimento
tipo cada campo c vai validar todos tipos de entrada e só 1 retornar true
função vc testa retorno
do CRUD
tipo a gente ja da os testes do CRUD
automatizados
pq nao tem pra q ficar criando isso sempre
e por eventos eh mai loco