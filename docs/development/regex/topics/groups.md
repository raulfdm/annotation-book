# Trabalhando com Grupos
[<-- Voltar](/README.md)

Grupos de caracteres são definidos por `()`. Como o próprio nome já diz, ele avalia uma expressão pelo conjunto dentro do parenteses, por exemplo:

```js
const date = '20 de Maio de 2015';
const regex  = /[1-3]?\d\s(de\s)[A-Za-z][a-zç]{3,8}\s(de\s)[1-2]\d{3}/
```

Perceba que a preposição `de ` agora faz parte de um grupo único, ou seja, `de + whitespace = um grupo`.

Além do mais, podemos ainda dizer que tal grupo **PODE OU NÃO** aparecer com o quantifier `?`. Assim, nossa regex ficaria:

```diff
- const regex_old  = /[1-3]?\d\s(de\s)[A-Za-z][a-zç]{3,8}\s(de\s)[1-2]\d{3}/
+ const regex_new  = /[1-3]?\d\s(de\s)?[A-Za-z][a-zç]{3,8}\s(de\s)?[1-2]\d{3}/
```

Entretanto, quando fazemos isso, no resultado da regex será retornado como um valor de seleção, ou seja, aplicando essa regex nessa data, terá o retorno:

```
1º grupo retornado: 20 de Maio de 2015 
2º grupo retornado:  de 
3º grupo retornado:  de 
```

Caso desejamos que um grupo **NÃO SEJA RETORNADO**, podemos dizer através do non-capturing groups (`?:`) dentro do grupo. Dessa maneira, teriamos:

```diff
- const regex_old  = /[1-3]?\d\s(de\s)?[A-Za-z][a-zç]{3,8}\s(de\s)?[1-2]\d{3}/
+ const regex_new  = /[1-3]?\d\s(?:de\s)?[A-Za-z][a-zç]{3,8}\s(?:de\s)?[1-2]\d{3}/
```

Agora, teremos apenas o grupo `20 de Maio de 2015` como resultado.

Podemos tirar proveito do retorno dos grupos e querer extrair além da data inteira, apenas o mês. Assim, podemos criar um grupo para o ano:

```diff
- const regex_old  = /[1-3]?\d\s(?:de\s)?[A-Za-z][a-zç]{3,8}\s(?:de\s)?[1-2]\d{3}/
+ const regex_new  = /[1-3]?\d\s(?:de\s)?[A-Za-z][a-zç]{3,8}\s(?:de\s)?([1-2]\d{3})/
```
Agora, teremos como resultado:
```
1º grupo retornado: 20 de Maio de 2015 
2º grupo retornado: 2015
```

Isso pode ser **EXTREMAMENTE** útil!

[Desafio](/aulas/4/desafio.md)

[Aula 5 - Expressões gananciosas ou pregriçosas -->](/aulas/5/ganancioso-ou-preguicoso.md)
