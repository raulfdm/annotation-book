# MAP
O `map`, assim como o `filter`, é uma _higher order function_, ou seja, ele é uma função que recebe uma outra função para acontecer.

Seu propósito é bem parecido com o do `filter`. Iteramos um array item por item e fazemos algo. Mas, diferente do `filter` onde validamos apenas se a condição aplicada for `true|false` e retornamos o objeto/item inteiro, no `map` podemos fazer transformações e gerar um novo array com novos exemplos.

## Problema
Imagina que precisamos iterar um array de objetos `Pessoa`. Nele, cada pessoa possui um nome, sobrenome e idade. Entretanto, queremos gerar um outro array concatenando o nome e o sobrenome e informando quantos anos a pessoa tem, veja abaixo:

```javascript
const listaPessoas = [
    {nome: "João", sobrenome: "da Silva", idade: 25},
    {nome: "Maria", sobrenome: "Cristina", idade: 33},
    {nome: "Douglas", sobrenome: "Brandão", idade: 61},
    {nome: "Juarez", sobrenome: "Mendonça", idade: 42},
    {nome: "Giovana", sobrenome: "Pereira", idade: 29},
]
```

### Sem Map

Para resolver isso sem map, é um pouco moroso e chato, mas vamos lá:

```javascript
let pessoas = [];
let pessoa = {};

for(let index = 0; index < listaPessoas.length; index++){
    pessoa = listaPessoas[index];
    pessoas.push(pessoa.nome + " " + pessoa.sobrenome + " tem "+ pessoa.idade + " anos");  
}

console.log(pessoas);
/*Resultado: 
[ 'João da Silva tem 25 anos',
  'Maria Cristina tem 33 anos',
  'Douglas Brandão tem 61 anos',
  'Juarez Mendonça tem 42 anos',
  'Giovana Pereira tem 29 anos' ]
*/
```
Só o código `for` acima, possui 185 caracteres.

### Com map

Vamos ver o mesmo código, mas usando `map`:

```javascript
let pessoas = listaPessoas.map(function(pessoa){
    return pessoa.nome + " " + pessoa.sobrenome + " tem "+ pessoa.idade + " anos";
});

console.log(pessoas);
/*Resultado
[ 'João da Silva tem 25 anos',
  'Maria Cristina tem 33 anos',
  'Douglas Brandão tem 61 anos',
  'Juarez Mendonça tem 42 anos',
  'Giovana Pereira tem 29 anos' ]
*/
```

Perceba que o código é bem menor, possui 135 caracteres, quase 30% menor do que o primeiro código. Fora que ele é bem mais legível. E pode ficar ainda menor, utilizando o conceito de Arrow Function e Template String (vou escrever sobre ainda os dois), ambas, features do ES2015:

```javascript

let pessoas = listaPessoas.map(pessoa => `${pessoa.nome} ${pessoa.sobrenome} tem ${pessoa.idade} anos`);

console.log(pessoas);

/*Resultado
[ 'João da Silva tem 25 anos',
  'Maria Cristina tem 33 anos',
  'Douglas Brandão tem 61 anos',
  'Juarez Mendonça tem 42 anos',
  'Giovana Pereira tem 29 anos' ]
*/
```
Ou seja, o código acima possui apenas 104 caracteres, 44% menor que o primeiro código.

## Conclusão
Assim como `filter`, o `map`vem pra ajudar a gente a resolver problemas de uma forma muito mais simples e clara, abstraindo as lógicas e escrevendo menos código. E como é de senso comum de todo programador: 

__menos código para fazer a mesma coisa = melhor qualidade de código__
