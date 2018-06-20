# Problemas e soluções

* [Alterar o editor do VIM para o VSCODE. Porém, ao tentar executar, gera um erro inesperado ](https://stackoverflow.com/questions/30024353/how-to-use-visual-studio-code-as-default-editor-for-git#answer-36644561)

* [Quero pegar apenas um commit específico de um branch e trazer para o meu atual branch](./cherry-pick.md)

## Subi um código errado para produção, como reverter?

### Melhor maneira

A melhor majeira de fazer isso é com o `git revert`, pois, ele mantém o log antigo e cria um novo, preservando a integridade do histórico.

1. Digite o comando `git log` e pegue hash do log do commit que está em perfeito funcionamento
1. Digite o comando `git revert {numero-do-hash}`
1. Digite uma mensagem (opcional)
1. Feito isso, de um `push` novamente para o branch de produção.

### Pior maneira

Podemos resolver isso usando `git reset`, porém, não é uma boa maneira de faze-lo, pois altera o log da tracking e isso pode gerar muito problema. Um dos usos recomendados é usa-lo apenas entre branches locais.

1. Digite o comando `git log` e pegue hash do log do commit que está em perfeito funcionamento
1. Digite o comando `git reset` e escolha qual a maneira que você deseja reverter:
    1. --hard: vai desconsiderar TUDO o que você fez e voltar pro estado do commit escolhido;
    1. --soft: vai pegar suas mudanças e colocar novamente em `staging`;
1. git reset --hard|--soft {hash-do-log-que-eu-quero-voltar}
