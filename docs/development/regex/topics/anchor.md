# Encontrando a posição certa com âncoras
[<-- Voltar](/README.md)

## Âncoras
> Âncoras marcam uma posição específica no alvo

Âncoras permitem que nós selecionamos um texto específico entre uma condição, por exemplo: `Raul Felipe de Melo, irmão de Rayla Idei`.

Se quisermos pegar o `de`, podemos criar uma regex `/de/`. Entretanto, nesse formato, irá selecionar o `de` de `i**de**i`, e não queremos isso. 

Do modo antigo, podemos usar `\s` no inicio e fim, ficando `/\sde\s/`, entretanto, a correspondência será `white_space+de+white_space` e queremos apenas o `de`. Assim, a âncora serve para você pegar esse valor específico, dentre a nossa expressão.

## Tipos
### \b => Word([A-Za-z0-9_]) boundary => Limite de caracteres

> Antes e depois da minha expressão não pode ter um WORLD CHAR [\w]

Ele delimita exatamente o que você quer encontrar. Assim, basta você definir um `\b` + `sua regex` + `\b` que o resultado exato da sua expressão será selecionado.

Exemplo:
```javascript
//sem boundary
var texto = "aaa aaaa aaa aaaa aaa"
var regex = /aaa/

regex.exec(texto); // Irá me retornar 5 posições, incluindo os "a" com 4 letras.

//com boundary
var regex = /\baaa\b/

regex.exec(texto); //irá me retornar apenas 3 posições que correspondem EXATAMENTE com 'aaa'
```
### \B => o inverso do \b
```javascript
//sem boundary
var texto = "português proporcional compor"

var regex = /\bpor\b/

regex.exec(texto); //sem resultado

regex = /\Bpor\B/
regex.exec(texto); //resultado: proPORcional
```


### ^ e $

Usamos esses âncoras quando queremos avaliar uma linha inteira, ou seja, do começo ao fim. Assim, `^` tem valor de _inicio_ e `$` tem valor de fim.

Por exemplo: `file:///Users/nico/Downloads/regex/index.html`

Queremos validar essa linha inteira. Assim, a regra será: começa com `file` e termina `.html`

```javascript
var texto = 'file:///Users/nico/Downloads/regex/index.html';
var regex = /^file.+\.html$/
```

[Aula 4 - Trabalhando com Grupos -->](/aulas/4/grupos.md)
