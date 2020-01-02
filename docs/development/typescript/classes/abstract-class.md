# Abstract Class

Outro conceito de OOP que TS implementa é o conceito de classes abstratas. Basicamente com ela, você pode OBRIGAR as classes que a herdam que implementem algum método específico.

Em React, quando criamos um class Component que `extends` de `React.Component` ou `React.PureComponent`, somos OBRIGADOS a implementar o método render. Logo, a implementação dessas classes seria algo do tipo:

```ts
abstract class Component {
  constructor(props: any) {
    // Do stuffs here
  }

  abstract render(): React.Node;
}

class MyComponent extends Component {
  constructor(props: any) {
    super(props);
  }

  render() {
    return <div>hi</div>;
  }
}
```

Se não especificássemos `render` dentro de `MyComponent`, teriamos um erro:

> ERROR: Non-abstract class 'MyComponent' does not implement inherited abstract member 'render' from class 'Component'.

Resumindo, quando definimos para o método ser `abstract`, definimos a `blueprint` (assinatura) dele, ou seja, quais os parâmetros que deverá receber e o que **deverá** retornar.

VALE NOTAR QUE, para definirmos um método como `abstract`, a classe PRECISA SER `abstract` e nesse cenário, ela perde o poder de ser instanciada:

```ts
abstract class Component {
  constructor(props: any) {
    // Do stuffs here
  }

  abstract render(): React.Node;
}

const component = new Component(); //> Cannot create an instance of an abstract class.(2511)
```
