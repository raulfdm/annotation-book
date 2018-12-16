# Variáveis e Escopo

## Var

### Escopo
O `var` é a forma com que declaravamos variáveis antes do advento do ECMASCRIPT 2015. Era uma forma bem problemática, pois o escopo dela é apenas de **função**, e não de bloco. Mas, o que isso significa?

Vamos observar o exemplo abaixo:
```js
var name = 'Raul'
var idade = 24

console.log(name) //> Raul
if(idade !== 25){
    var name = 'Carlos'
    console.log(name) //> Carlos
}

console.log(name) //> Carlos
```

Apesar do código acima não fazer muito sentido, veja que tentamos criar uma nova variável com o mesmo nome, e o que tivemos foi uma reescrita da variável declarada anteriormente. Como dito, isso acontece porque o **var** tem escopo apenas de **função**, e não de bloco.

Caso tivessemos uma função, isso seria totalmente possível:
```js
var name = 'Raul'
var idade = 24

console.log(name) //> Raul
function changeName(){
    var name = 'Carlos'
    console.log(name) //> Carlos
}
changeName()
console.log(name) //> Raul
```

Perceba que fizemos a mesma coisa, só mudando para função, e agora **não** sobreescrevemos a variável `name`, apesar de ter o mesmo nome.

### Criação
Outro comportamento bem estranho usando **var**, é que podemos declarar a mesma variável varias vezes e tudo ficará bem:
```javascript
var name = 'Raul'
var name = 'Carlos'
var name = 'Joana'

console.log(name) //> Joana
```

### Hoisting
Além de tudo isso, as variáveis usando **var** sofrem um processo chamado `hoisting`. Antes de explicar o que é, veja este exemplo:
```javascript
console.log(name) //> undefined

var name = 'Raul'
```

O que o Javascript faz nesse caso, é um **içamento** (hoisting) das variáveis para o topo do bloco, que seria equivalente a isso:
```javascript
var name
console.log(name) //> undefined
name = 'Raul'
```

Isso é um tanto bizarro, mas vamos ver que esse problema foi resolvido com let.

--- 

## Let

### Escopo
O let veio com o ES2015 e tem o mesmo papel do `var`, PORÉM, ele tem escopo de **bloco**, e não de função. Pegando o mesmo exemplo anterior, temos o seguinte resultado:

```js
let name = 'Raul'
let idade = 24

console.log(name) //> Raul
if(idade !== 25){
    let name = 'Carlos'
    console.log(name) //> Carlos
}

console.log(name) //> Raul
```

isso acontece porque dentro de cada bloco ( {chaves definem um bloco} ), o escopo será totalmente diferente do de fora.

### Criação
Lembra do var, que poderiamos instanciar a mesma variável sem erros? Com let a coisa muda um pouco de cena:

```javascript
let name = 'Raul'
let name = 'Carla' //> Uncaught SyntaxError: Identifier 'name' has already been declared
```

### Hoisting
Diferente do var, onde podemos chamar uma variável mesmo antes dela ser declarada pelo processo de _hoisting_, com **let** teremos o seguinte erro:

```javascript
console.log(name) //> VM97:1 Uncaught ReferenceError: name is not defined

let name = 'Raul'
```

O que faz muito mais sentido.

---

## Const

### Escopo/Criação
Const veio também no ECMASCRIPT 2015, como uma forma de declarar uma constante (algo que nunca muda, um valor que nunca deverá ser alterado). Com relação ao escopo, temos o mesmo comportamento do **let**, porém, por se tratar de uma constate, não podemos "alterar" seu valor.

```javascript
const name = 'Raul'
name = 'Carlos' //> VM1495:2 Uncaught TypeError: Assignment to constant variable.
```

Porém, ele ainda tem um comportamento falho. Quando dizemos que não podemos alterar o valor, é referente a **ATRIBUIÇÕES**. Veja o exemplo abaixo:

```javascript
const person = {
    name: 'Raul',
    age: 25
}

console.log(person) //> {name: "Raul", age: 25}

person.name = 'João'
person.idade = 33

console.log(person) //> {name: "João", age: 25, idade: 33}
```

> "Ué, não era pra ser uma constane?"

Então.. bugs everywhere. E isso funciona no caso de Arrays também. A única maneira de evitar isso, é fazendo um freeze do objeto logo após sua declaração:

```javascript
const person = {
    name: 'Raul',
    age: 25
}
Object.freeze(person)
console.log(person) //> {name: "Raul", age: 25}

person.name = 'João'
person.idade = 33

console.log(person) //> {name: "Raul", age: 25}
```

Assim, não conseguiremos fazer qualquer alteração de valores.

### Hoisting
Consts tem o mesmo comportamento de let com relação ao hoisting, ou seja, caso eu tente usar uma const antes de sua declaração de fato, teremos erro:

```javascript
console.log(name) //> VM97:1 Uncaught ReferenceError: name is not defined

const name = 'Raul'
```
