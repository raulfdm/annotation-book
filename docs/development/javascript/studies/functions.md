# Functions 

## Default properties
Muitas vezes queremos definir um valor padrão em uma função, caso o parametro não seja passado. Isso evita do nosso código quebrar. Antes do ES6 era feito da seguinte forma:

```javascript
function sayHello(name, surname){
    name = name || 'João'
    surname = surname || 'da Silva'    
    
    console.log('Hello ' + name + ' ' + surname)
}

sayHello() //> Hello João da Silva
sayHello('Raul') //> Hello Raul da Silva
sayHello('Raul', 'de Melo') //> Hello Raul de Melo
```

com ES6, declaramos o valor *default* logo no recebimento dos parametros:
```javascript
function sayHello(name = 'João', surname = 'da Silva'){
    console.log('Hello ' + name + ' ' + surname)
}

sayHello() //> Hello João da Silva
sayHello('Raul') //> Hello Raul da Silva
sayHello('Raul', 'de Melo') //> Hello Raul de Melo
```

Assim, teremos o mesmo resultado, porém, com bem menos código.

---

## Arrow Function
Arrow function é uma nova forma de declarar funções que veio com o ECMASCRIPT 2015. Com ela, é possível escrever funções de uma forma bem elegante e semântica:

```javascript
// Com function convencional
const sum = function(x,y){
    return x+y
}

// Com arrow function
const sum = (x,y) => x + y
```

Parece estranho, mas a Arrow function te proporciona uma *suggar syntax* bem interessante. Perceba que no exemplo acima, não precisamos usar a palavra `return` para dizer que iremos retornar a soma dos dois numeros. Isso acontece porque temos apenas UMA linha (single line). Caso tivessemos mais lógica para fazer, essa estratégia não seria possível.

```javascript
const sum = (x,y) => {
    if(isNaN(parseInt(x)) || isNaN(parseInt(y)))
        throw new Error('As variáveis Não são números')
    else
        return x+y
}
```

Ainda temos o caso onde recebmos apenas um parametro, no qual não precisaremos passar o mesmo entre parenteses:
```javascript
const sayHello = name => console.log('Hello ' + name)
```

## Escopo

Apesar de ser muito interessante, temos que tomar muito cuidado com o escopo de *Arrow functions*, pois, o tratamento do escopo é bem diferente da normal function.

O caso que fica mais fácil de enxergar isso, é quando queremos atribuir uma função ao evento de click de um botão: 

```javascript
const $myButton = document.querySelector('#send-form')

$myButton.addEventListener('click',function(){
    console.log(this)
})
```

O `this` é um objeto que retorna o local que você se encontra. Caso você abra um navegador e imprima `console.log(this)`, será impresso o objeto `window`.

No caso do exemplo acima,  o `this` será o botão no qual estamos chamado a função `addEventListener`. Porém, com a arrow function, ela pega como `this` o contexto no qual está sendo chamada.

![Normal Function](http://i.imgur.com/wQ5sE0K.png)

![Arrow Function](http://i.imgur.com/dnWAsSv.png)

Outro exemplo de escopo:

```javascript
const myFunctions = {
    normalFunction: function(){
        console.log(`I'm a normal function`,this)
    },
    arrowFunction: () => console.log(`I'm an arrow function`,this)
}

myFunctions.normalFunction()
//> I'm a normal function {normalFunction: ƒ, arrowFunction: ƒ}

myFunctions.arrowFunction()
//> I'm an arrow function Window {stop: ƒ, open: ƒ, alert: ƒ, confirm: ƒ, prompt: ƒ, …}
```

Então veja que a `normalFunction` chama this, mas this é o próprio objeto `myFunction`. Entretanto, a função `arrowFunction` ao chamar this, chama o `window`, que é o contexto onde está sendo chamado.

Assim, precisamos tomar cuidado e saber os momentos de usar cada uma.
