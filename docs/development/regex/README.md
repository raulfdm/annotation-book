# Curso Regex Alura

Repositório com foco em fazer anotações e resenhas sobre o [Curso online de Expressões regulares: Capturando textos de forma mágica](https://www.alura.com.br/curso-online-expressoes-regulares)

## Ferramentas
- [PROJETO ONLINE](https://studentraul.github.io/regex/)
- [https://regex101.com/](https://regex101.com/)
- [http://regexr.com/](http://regexr.com/)

## Anotações pessoais
[Rascunhos e ideias](aulas/anotacoes.md)

## Lista com as expressões

| caracter          | Tipo                      | Significado                                                                               | Metachar  |
| :---:             | :---:                     | ---                                                                                       | :---:     | 
| \d                | _**Classe de caracter**_  | Dígitos de 0-9                                                                            | Não       |
| \w                | _**Classe de caracter**_  | Alfanumérico, ou seja, [A-Za-z0-9_]                                                       | Sim       |                     | Não       |
| \s                | _**Classe de caracter**_  | O caracter pode qualquer espaço em branco (tab, space, etc)                               | sim       |
| .                 | _**Classe de caracter**_  | Qualquer caracter                                                                         | Sim       |
| [ ]               | _**Classe de caracter**_  | Define um conjunto de caracteres que PODEM aparecer                                       | sim       |
| {n}               | _**Quantifier**_          | O caracter pode aparecer exatamente `n` vezes                                             | Sim       |
| {n,}              | _**Quantifier**_          | O caracter pode aparecer `n ou mais` vezes                                                | Sim       |
| {n,m}             | _**Quantifier**_          | O caracter pode aparecer `n até m` vezes                                                  | Sim       |
| +                 | _**Quantifier**_          | O caracter pode aparecer `1 ou mais` vezes.                                               | Sim       |
| *                 | _**Quantifier**_          | O caracter pode aparecer `0 ou mais` vezes.                                               | Sim       |
| ?                 | _**Quantifier**_          | O caracter pode aparecer `0 ou 1` vez                                                     | Sim       |
| ( )               | _**Group**_               | Define um GRUPO de caracteres (será trazido nos resultados)                               | sim       |
| (?:)              | _**Group**_               | (noun-capturing group) Usado dentro do grupo, define que o resultado da expressão **NÃO** deverá ser retornado   | sim       |
| \b                | _**Âncora**_              | Define um range de posição EXCLUINDO palavras que comecem ou terminem com \w              | sim       |
| \B                | _**Âncora**_              | Define um range de posição INCLUINDO palavras que comecem ou terminem com \w              | sim       |
| ^                 | _**Âncora**_              | Início do alvo, ou seja, o alvo começa a partir daqui                                     | sim       |
| $                 | _**Âncora**_              | Final do alvo, ou seja, o alvo termina aqui                                               | sim       |
| ^ minha\_regex $  | _**Âncora**_              | Define um range, só trará resultados quando a Regex começar e terminar daquela maneira    | sim       |


