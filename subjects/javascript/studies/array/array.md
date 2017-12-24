# Arrays

Observações:

- São mutáveis, ou seja, `[1,2,3][0] = 3 === [3,2,3]`
- Adiconar um elemneto por ultimo na lista: `Array.push(<meu-valor>)`
- Remover o ultimo elemento da lista: `Array.pop()` => vai retornar o elemento devolvido e vai alterar o valor do array
- Adicionar um elemento primeiro na lista: `Array.unshift(<meu-valor>)`
- Remover o primeiro elemento da lista: `Array.shift()` funciona igual o `pop`, mas vai ser o primeiro ao invés do último
- Cortar um array em posições especificas: `Array.slice(initial[, end])`. O slice aceita 2 parâmetros (inicio e fim), caso não seja passado o parametro fim, será utilizado `array.lenght`. O indice fim usará o ultimo elemento antes do index passado, por exemplo,  `[1,2,3,4].slice(1,3) //> [2,3]`, ou seja, o índice 3 seria o número 4, mas ele pega o anterior (3).


## Array.from (ES6)
Hoje, temos uma forma bem tranquila de transformar um lista em qualquer que seja o formato para um Array de fato.

É muito comum selecionarmos vários elementos com uma mesma classe e queremos usar os métodos do Array. Entretanto, quando usamos o `querySelectorAll` por exemplo, ele retorna uma lista do tipo `NodeList`, e nela não temos o método `.map` por exemplo. Dessa maneira, podemos agora transformar esse NodeList em um array facilmente:

```javascript
const listOfLis = document.querySelectorAll('#myList li')
const arrayOfLis = Array.from(listOfLis)

arrayOfLis.map(li => console.log(li))
```

## Array.of (ES6)
Ganhamos no ES6 també o método `Array.of`, que basicamente cria um novo array, dado alguns elementos:

```javascript
const myArray = Array.of(1,2,'raul',{cor: 'verde'})
console.log(myArray) //>  [1, 2, "raul", {…}]
```

Segundo a documentação da Mozilla (MDN web docs), a principal diferença entre o `Array.of` e o costrutor do array (`Array()`) é no caso onde queremos criar um array com um número, como no exemplo abaixo:

```javascript
console.log(Array(3)) //> [,,,]

console.log(Array.of(3)) //> [3]
```
