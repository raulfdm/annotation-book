# Strings

## String.startsWith (ES6)

O método `startsWith` valida se a string começa com algum valor. O primeiro parâmetro recebido é o valor que será buscado dentro da string. O segundo parametro (opcional), indica a partir de qual posição queremos procurar:

```javascript
const myText = 'Oi, eu sou o goku'

myText.startsWith('Oi') //> true
myText.startsWith('oi') //> false
myText.startsWith('eu', 4) //> true
```

Lembrando que a contagem sempre começa em 0 (O = 0, i = 1... etc)

## String.endsWith
Mesma coisa do startsWith, porém, como o próprio nome já diz, verifica se a string termina com tal texto. Como segundo parâmetro, ao invés de dizer **onde começa**, dizemos **até qual posição** deverá ser considerado:

```javascript
const myText = 'Oi, eu sou o goku'

myText.endsWith('goku') //> true
myText.endsWith('sou') //> false
myText.endsWith('sou',10) //> true
```

## String.includes
Essa é uma das melhores funções de todos os tempos! Com ela, podemos verificar se uma string contém determinado texto: 

```javascript
const myText = 'Oi, eu sou o goku'

myText.includes('goku') //> true
myText.includes('Goku') //> false
```
