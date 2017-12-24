## Uso do PubSub
O primeiro passo é baixar a depedencia:

```sh
$ yarn add pubsub-js

# ou se preferir

$ npm install --save pubsub-js
```

Agora, faça o import da *lib* no seu projeto através do comando:

```javascript
import PubSub from 'pubsub-js'
```

## Funcionamento

O Pubsub trabalha com a lógica de **publicação** e **inscrição** em eventos (**publish** and **subscribe**), ou seja, caso que eu queira que o evento seja propagado, basta eu publicar os "acontecimentos" em um canal.

Já se eu quiser saber o que está acontecendo em algum canal, basta eu me inscrever em um canal, e, sempre que tiver alguma alteração, eu serei notificado.

### Publish

Para publicar em um canal, basta passar na função `.publish` o nome do canal que será divulgado como primeiro parâmetro e o informar os dados que foram alterados ou que possam interessar os ouvintes do canal:

```javascript
// ...
PubSub.publish('atualiza-lista',novaLista);
// ...
```

### Subcribre

Já para ouvir um canal, basta passar na função `.subcribe` o nome do canal e uma função de **callback**. Essa função de callback receberá dois parâmetros. O primeiro é o nome do tópico e o segundo é o objeto que foi propragado na publicação:

```js
// ...
PubSub.subscribe('atualiza-lista',(topico, novalista)=>{
  //do something...
});
// ...
```

## Conclusão

Dessa maneira, você consegue propagar mensagens e dados por qualquer componente, bastando fazer uso da biblioteca onde for necessário.
