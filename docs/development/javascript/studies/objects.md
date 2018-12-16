# Objects

## Herança

O conceito de herança equivale para todas as linguagens: Eu tenho um objeto Animal e o cachorro. Cachorro herda atributos e ações que todo animal possui. Exemplo:

```javascript
let animal = {
    anda: function(){},
    respira: function(){return "estou respirando"},
}

//Deve ter tudo o que um animal pode fazer mais o método de latir
let cachorro = {
    //...Coisas de animais
    late: function(){}
}
```

Em Java e no ES6, já podemos criar classes e extende-las facilmente, mas o foco é estudar herança em ES5. Assim, podemos utilizar a função `create`de construtor `Object`:

```javascript
cachorro = Object.create(animal);

console.log(cachorro(respira)); //"estou respirando"
```

No fundo, o que o `Object.create` faz, é pegar o objeto animal que foi passado pra ele, e adiciona-lo no `prototype` de cachorro. Assim, quando tentamos acessar uma propriedade `respira`, o primeiro lugar onde o JavaScript vai procurar é em `cachorro`. Caso não tenha, ele vai pro prototype `animal` e verifica se tem o método de respirar. No nosso exemplo, o método não existe, mas poderiamos ter que o objeto `animal` possui outro objeto em seu prototype, nesse casso, o JavaScript validaria toda a cadeia de propriedades em cada objeto e seus prototypes até chegar em `nullo` ou `undefined`.

## Getter and Setter

Em ES5, podemos definir métodos `get` e `set` nos nosso objetos. Ambos serão equivalentes a uma função em javascript, mas, com um comportamento bem definido.

### Get

O Get, é uma função que não espera nenhum parâmetro, e como o próprio nome já diz, tem como objetivo acessar alguma propriedade dentro do objeto ou realizar alguma ação para retornar um valor, por exemplo:

```javascript
let pessoa = {
    idade: 23,
    get ehMaiorIdade(){
        if (this.idade>18) return "É maior de idade"
        else return "É menor de idade"
    }
}

console.log(pessoa.ehMaiorIdade); //É maior de idade
```

No caso do get ehMaiorIdade do objeto pessoa, é verificado apenas se a idade de pessoa é maior ou menor de idade. Perceba que mesmo sendo uma função, não precisamos evoca-la (`pessoa.ehMaiorIdade()`) para receber seu valor.

## Set

Já no caso do set, é também uma função que espera receber __NO MÍNIMO__ um valor. Esse valor tem que ser enviado através de atribuição, e não pela chamada como fazemos com funções normais, por exemplo:

```javascript
let pessoa = {
    idade: 23,
    set mudarIdade(novaIdade){
      this.idade  = novaIdade;  
    },
    get ehMaiorIdade(){
        if (this.idade>18) return "É maior de idade"
        else return "É menor de idade"
    }
}
console.log(pessoa.idade); //23
console.log(pessoa.ehMaiorIdade); //É maior de idade
pessoa.mudarIdade = 17;
console.log(pessoa.idade); //17
console.log(pessoa.ehMaiorIdade); //É menor de idade
```

No caso do *set* de exemplo, foi bem simples, poderiamos ter resolvido com apenas uma nova atribuição em idade. Entretanto, podemos usar para abstrair regras complexas, onde apenas queremos definir um valor e a mágica toda acontecer dentro do método *set*.


## Checar se a propriedade X existe:
As vezes queremos verificar se a propriedade X existe no objeto A: 

```javascript
const a = {
  nome: 'raul',
  Sorenome: 'de Melo'
}
```

Para tal, podemos usar o método `hasOwnProperty`. O mesmo retornará `true`para caso a propriedade exista ou false para caso não:
```js
a.hasOwnProperty('nome') //> true
a.hasOwnProperty('idade') //> false
```

## Shorthand Properties (ES6)
Junto com o ES6, ganhamos uma *suggar syntax* ao declaramos propriedades de um objeto. Veja como era feito antigamente:

```javascript
var name = 'Raul'
var surname = 'de Melo'
var age = 25

var person = {
    name: name,
    surname: surname,
    age: age,
    getFullName: function(){
        return this.name + ' ' + this.surname
    }
}

console.log(person) //> {name: "Raul", surname: "de Melo", age: 25, getFullName: ƒ}
```

Veja que tem muita repetição de código e palavras desnecessárias. Veja como fica com o **shorthand properties**:

```javascript
const name = 'Raul'
const surname = 'de Melo'
const age = 25

const person = {
    name,
    surname,
    age,
    getFullName(){
        return this.name + ' ' + this.surname
    }
}

console.log(person) //> {name: "Raul", surname: "de Melo", age: 25, getFullName: ƒ}
```

Perceba que escrevemos menos código, pois não precisamos escrever o nome das variáveis duas vezes ao transforma-la em propriedade do objeto. Também na função, agora não precisamos mais passar a palavra **function**.
