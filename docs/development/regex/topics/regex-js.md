# Regex em Javascript

Há duas formas de se declarar uma Expressão Regular em Javascript.

A primeira é em forma de objeto: 

```javascript
//aplicando a regex \w\s
const myRegex = new RegExp('\\w\\s','g');
//obs.: para \, é necessário escapar utilizando outra \
``` 
A segunda é usando a criação literal (mais recomendada):

```javascript
//aplicando a regex '\w\s'
const myRegex = /\w\s/g;
```

A segunda é recomendada quando o pattern não é dinâmico, ou seja, já sabemos o que queremos exatamente.

## Executando
Após declaramos uma variável com o tipo regex, temos dois métodos bastante utilizandos e comum. O primeiro é o EXEC que applica a expressão em um alvo e retorna o resultado encontrado. Apesar dele retornar o resultado, esse método é um daqueles que a gente precisa executar até não retornar mais nada, assim, precisamos aplicar um laço `while`:

```javascript
const target = '22a33b44c'
const pattern = /\d{2}\w/g
let result = '';

while(result = pattern.exec(target)){
    console.log(result)
}
/* Resultado
[ '22a', index: 0, input: '22a33b44c' ]
[ '33b', index: 3, input: '22a33b44c' ]
[ '44c', index: 6, input: '22a33b44c' ]
*/
```

Caso execurtamos apenas uma vez, teremos o seguinte resultado:
```javascript
const target = '22a33b44c'
const pattern = /\d{2}\w/g
let result = pattern.exec(target)

console.log(result)
/* Resultado
[ '22a', index: 0, input: '22a33b44c' ]
*/
```

### Grupos
Como sabemos, quando definimos um grupo, seu resultado será retornado (a menos que usamos `?:`). Assim, o resultado será:

```javascript
const target = '22a'
const pattern = /\d{2}(\w)/g
console.log(pattern.exec(target))
/* Resultado
[texto_que_obedece_regex,grupo_1,onde_começa,target]
[ '22a', 'a', index: 0, input: '22a' ]
*/
```

Consequentemente, se tivermos 10 grupos, teremos 10 elementos no array após o primeiro elemento (que representa o texto encontrado pela regex).


## 1,2,3 TESTANDO
As vezes não queremos pegar o resultado, apenas queremos saber se aquele target obedece um padrão. Logo, temos o método `test` no objeto regex que apenas returna um `boolean` (`true or false`) dizendo: Aplica | Não Aplica:

```javascript
const target = '22a33b44c'
const target2 = 'raul felipe de melo'
const pattern = /\d{2}\w/g


console.log(pattern.test(target)) //true
console.log(pattern.test(target2)) //false
```


## Exercicios e Idéias

### Exercício 1
Dado a data '25-05-2017', troque o hífem (`-`) por barra (`/`).

```javascript
const date = '25-05-2017'
const regex = /-/g
const newDate = date.replace(regex,'/')
console.log(newDate) // 25/05/2017
``` 

### Exercício 2
Dado uma linha do que era pra ser um CSV (`'100,200-150,200;20'`), separe os valores considerando virgula (`,`), hífen (`-`), ponto-e-virgula (`;`):

```javascript
const csvData = '100,200-150,200;20'
const regex = /[,\-;]/g
const dataFixed = csvData.split(regex)
console.log(dataFixed) //[ '100', '200', '150', '200', '20' ]
``` 

### Exercício 3
Dado uma string com códigos concatenados (`A121B12112C12212F12G01`), cada código deve começar com uma letra maíscula seguida de 1 ou mais números. Escreva uma Regex que pegue cada código e retorne um array com os elementos.

Obs.:
Objetos do tipo `String` possuem um método chamado `Match`, onde é recebido uma expressão regular e retornado um array com cada correspondência encontrada.

```javascript
const codigos = 'A121B12112C12212F12G01';
const exp = /[A-Za-z]\d+/g;
const result = codigos.match(exp);

console.log(result) //[ 'A121', 'B12112', 'C12212', 'F12', 'G01' ]
```

### Desafio
Com as suas palavras, tente explicar o que a regex abaixo encontra: `<(a)\s+href="(.+)"(?:>(.*)<\/\1>)`

- Quais grupos ela seleciona?
- Quais são os grupos que ela não seleciona?
- Há back-references?
- Qual alvo daria um match inteiro?

Sempre analise por partes, começando no início!

RESPOSTA:

- Quais grupos ela seleciona?
Ela selecionará:
  - o elemento (a);
  - o link de referência (href);
  - o conteúdo da LI ();
- Quais são os grupos que ela não seleciona?
  - (?:>(.*)<\/\1>)
- Há back-references? Sim, (a).
- Qual alvo daria um match inteiro? <a href="#">Home</a>
