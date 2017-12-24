# Regex

Regex, ou expressão regular é um padrão utilizado para identificar determinadas combinações em textos.

## Vocabulário

- Target: Texto que eu quero analisar.
- Pattern: **Regex** que será usada para avaliar o texto
- Match: Resultado após aplicar o **Pattern** no **Target**
- Metachar: São caracteres que não são entendidos pela engine como o seu significado semântico, por exemplo, o `.` é entendido como `qualquer caracter` e não como `caracter ponto`. Podemos escapar de metachars utilizando `\`, por exemplo, `\.`
- quantifier: conjunto de caracteres especiais que definem quantas vezes o caracter deve aparecer. Represetado por colchetes: `{<qtde de vezes>}`

## Fluxo
A avaliação de um texto feito com expressão regular, necessita de uma engine para acontecer, obedencendo o fluxo abaixo:

![Imgur](http://i.imgur.com/PJqicpC.png)
