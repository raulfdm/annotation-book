# Anotações Pessoais

- O `/g` do Regex do Javascript significa `GLOBAL`, ou seja, ele informa que desejamos pegar TODAS as ocorrencias que correspondem ao padrão, não só a primeira.

- No exemplo abaixo, uma opção de pegar todas as tags `<code>`, podemos usar a expressão `<\?code>`, onde indica que pode ou não ter uma barra na tag que queremos.
```
No <code>for</code>, o valor de <code>i</code> começa de zero e é incrementado a cada volta enquanto <code>i < 10</code>, portando o bloco de código do for é executado 10 vezes.
```

- Caracteres especiais não são contabilizados por classes de caracteres como `[A-Za-z]`, assim, precisamos adiciona-los manualmente: `[A-Za-zçóôáã]`

- Para selecionar frases, podemos usar a expressão: `[\w\s]+` (pegue as correspondências onde tenha qualquer word character ou espaço em branco que possa aparecer 1 ou mais vezes)

- Tags HTML: `<h1[^>]+>` (pegue toda correspondência de h1(`<h1`), qualquer coisa que não seja um sinal de maior (`[^>]`), que possa ocorrer uma ou mais vezes (`+`) até encontrar o sinal de maior (`>`))

- Além de âncora, o `^` pode ser usado para negação: `[\w]` (tudo que for word char) - `[^\w]`, tudo que **NÃO FOR** word char. Obs.: vale dentro de um grupo (`[]`)

- Dentro de um grupo de caracter, se tiver um hífe (`-`) entre dois outros caracteres, ele vai ser avaliado como RANGE. Caso não seja esse o propósito, será necessário escapa-lo: `[;-,] //Erro __________ [;\\-,] //Sucesso`
