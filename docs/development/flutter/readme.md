# Flutter

## StatelessWidget

Stateless widget como o próprio nome já diz, é um widget que não guarda estado, ou seja, ele só renderiza a UI e não guarda e nem altera nenhuma informação. Ele só se atualizará quando receber uma nova informação de fora dele (`Data input`).

Para criar um StatelessWidget, basta:

```dart
import 'package:flutter/material.dart';

class MyWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    // Implementar o corpo dele
    return null;
  }
}
```

## StatefulWidget

Com os StatefulWidgets as coisas funcionam um pouco diferentes. A recomendação é que você quebre em duas classes:

- Uma que estende a `StatefulWidget`, que tem a habilidade de ser re-renderizada;
- Outra que estende `State`, que vai segurar os widgets e a lógica.

Assim, baseado no exemplo anterior, teriamos algo assim:

```dart
class MyWidget extends StatefulWidget {
  @override
  State<StatefulWidget> createState() {
    return _MyWidgetState();
  }
}

class _MyWidgetState extends State {
  _counter = 0;

  _onIncrement(){
    setState((){
      _counter += 1
    })
  }

  _onDecrement(){
    setState((){
      _counter -= 1
    })
  }

  @override
  Widget build(BuildContext context) {
    //return your Widgets
  }
}
```

Obs.:

- O padrão é sempre usar o mesmo nome do component, porém:
  - Sempre com `underline` como prefixo. Em dart, isso é entendido realmente como privado;
  - com o sufixo `State`, exemplo: `MyApp` -> `_MyAppState`
- Os methods e variáveis da classe devem também serem "escopados" com `underline`, assim, mesmo que importem o seu Widget em outro lugar, ninguém vai ter acesso ao estado ou qualquer função que o manipula diretamente;
- Para alterar o state, é preciso usar a função `setState`, que recebe uma anonimous function.

## Lista dinâmica de widgets

Muitas vezes, dada uma lista de objetos, queremos gerar uma lista de widgets (components), assim como fazemos em react:

```jsx
const list = [
  {
    text: "abc",
    value: 10
  },
  {
    text: "def",
    value: 20
  }
];

const MyComp = () => {
  return (
    <>
      <h1>My List of Stuffs</h1>
      {list.map(obj => (
        <p>
          {obj.text} with value {obj.value}
        </p>
      ))}
    </>
  );
};
```

Com Dart/Flutter, é a mesma lógica, porém, pelo fato de ser fortemente tipado, precisamos pensar de um jeito um poco diferente:

```dart
class MyApp extends StatelessWidget{

  var list = [{
    'text': 'abc',
    'value': 10
  },{
    'text': 'def',
    'value': 20
  }];

  @override
  Widget build(BuildContext context){

  return Scaffold(
      body: Column(
        children: <Widgets>[
          Text('My List of Stuffs'),
          ...list.map((obj){
            return Text(obj['text'] + 'with value' + obj['value']);
          }),
        ],
      ),
    ),
  }
}
```

O children em `Column` espera uma lista de arrays. Se só iterarmos pelo array usando map, o resultado será um array dentro de outro array (`[[]]`). Por isso, podemos usar o spread operator para jogar todos os elementos gerados dentro do array principal.

Para os casos onde temos listas dinamicas, por exemplo:

```dart
var list = [{
    'text': 'abc',
    'value': 10
  },{
    'text': 'def',
    'value': 20
  }];

list[0]['text'] // Queremos o valor de "texto" do primeiro elemento
```

Além de fazermos o loop, precisamos fazer uma conversão de tipos e deixar claro para o dart do que se trata aquele array. Assim, o mesmo código anterior, ficaria assim:

<!-- REPENSAR O EXEMPLO, array dentro de array -->

```dart
class MyApp extends StatelessWidget{

  const list = [{
    'text': 'abc',
    'value': 10
  },{
    'text': 'def',
    'value': 20
  }];

  @override
  Widget build(BuildContext context){

  return Scaffold(
      body: Column(
        children: <Widgets>[
          Text('My List of Stuffs'),
          ...list.map((obj){
            return Text(obj['text'] + 'with value' + obj['value']);
          }),
        ],
      ),
    ),
  }
}
```

## Final vs Const vs Var

### Var

Como o nome já diz, é uma VARIÁVEL, ou seja, é mutável

```dart
void main() {
  var variable = ['some', 'value'];
  print(variable); // [some, value]

  variable = ['another','value']; // Reassign it
  print(variable); // [another, value]

  variable.add('hola'); // Mutating it via .add method
  print(variable); // [another, value, hola]
}
```

### Final

Torna o objeto, valor, o que quer que seja, imutável apenas em tempo de runtime:

```dart
void main() {
  final variables = ['some', 'value'];
  
  void getValue(index){
    final value = variables[index];
    print(value);
    // some
    // value
  }
  
  variables.forEach((value){
    getValue(variables.indexOf(value));
  });
  
  // variables = ['new']; -> THROW ERROR "Setter not found: 'variables'."
  
  variables.add('hola'); // Mutating it via .add method -> Still can do
  print(variables); // [another, value, hola]
}
```

Como você pode ver, na função `getValue`, temos `value` definido como um final. Isso significa que ele será dinamico, ou seja, a cada loop do array `variables`, `value` terá um valor diferente.

Em outras palavras, `final` é uma variável que é alterada apenas no momento de sua criação (compilação). depois disso, ela vira uma constante e um erro aparecerá caso você tente reatribuir algum valor.

### Const

Torna o objeto, valor, o que quer que seja, imutável em tempo de compilação E em tempo de runtime.

Então, diferentemente do `final`, `const` precisa ter um valor definido no momento da compilação:

```dart
void main() {
  final variables = ['some', 'value'];
  
  void getValue(index){
    // const value = variables[index]; -> THROW ERROR: "Not a constant expression."
    
    // print(value);
  }
  
  variables.forEach((value){
    getValue(variables.indexOf(value));
  });
  
  // variables = ['new']; -> THROW ERROR "Setter not found: 'variables'."
  
  variables.add('hola'); // Mutating it via .add method -> Still can do
  print(variables); // [another, value, hola]
}
```

Logo, todos os valores precisam ser fixos e definidos no momento de sua compilação até a execução.

### Outros truques

Dart também permite que você atribua `final` ou `const` para os valores, exemplo:

```dart
void main() {
  var variables = const ['some', 'value'];
  print(variables); // [some, value]
  
  // variables.add('Raul'); // THROWS: "Unsupported operation: add"
  
  variables = ['Another', 'value'];
  variables.add('Raul');
  print(variables); // [Another, value, Raul]
}
```

ou seja, `variables` é uma variável, mas o seu valor é uma constante.
