# Dicas para usar GIT no VSCODE

O Visual Studio Code fornece uma série de ferramentas para facilitar o uso do GIT em nossos projetos. Para ver o painel de opção do Git nele, basta clicar no botão abaixo:

![Git Button](./media/git-icon-vscode.png)

Caso você controle versão do projeto com git, neste painel, aparecerá os arquivos que sofreram alterações, que estão em `staging` (prestes a serem comitados) e várias outras opções no menu (...).

## Barra Inferior
Na barra inferior do VSCODE, temos uma série de opções e informações sobre o Git.

![Git Button](./media/bottom-bar.png)

### Branches
No exemplo acima, a primeira informação indica que estamos no branch `Master` e o `*` significa que há divergências com a última versão.

Se clicarmos nela, teremos a opção de criar um novo Branch ou então de trocar de branch.

![Git Button](./media/branch-options.png)

### Synchronizer
A segunda opção é a responsável por nos informar sobre as mudanças.
A seta para baixo significa que há mudanças no branch trackeado (remoto) a serem baixadas. Já a seta para cima, significa que há mudanças feitas locais a serem enviadas para o branch remoto.

Clicando nela, ocorre uma sequencia de ações como pull/push para deixar ambos os repositórios iguais.

## Menu ...

![Menu Options](./media/menu-options.png)

O menu do git no VScode apresenta uma série de funcionalidades interessantes.

### Pull from...
Esse comando me permite baixar as mudanças de um branch diferente, exemplo, estou no `development` mas preciso pegar as mudanças do branch `feature/023`.

**Uso:** Usar quando uma feature for finalizada e queremos migrar o código feito para o `master` ou `developemnt`, lembrando que **será feito um commit de MERGE para isso**

### Pull rebase
Esse comando é similar ao `Pull from..`, mas com a diferença que não faz o Merge, Evitando poluição no log.

## Command Pallet
Além disso, o VSCODE provê na sua command Pallet (`View > Command Paller` OU `ctrl[comamand]+shift+P`) uma série de comandos úteis para que possamos utilizar.

Para ver a lista completa, abra o Command Pallet e digite `Git`.

## Libs complementares

### [Git: Add Remote](https://marketplace.visualstudio.com/items?itemName=samschneller.git-add-remote)
Apesar de ser bem completo, o VSCODE ainda não possúi um comando muito útil hoje em dia: o Add remote!

Para ter acesso a isso, precisamos adicionar uma extensão chamada: `Git: Add Remote`

Quando chamamos ela no Command Pallet, ele pergunta qual é o nome do repositório remoto que está sendo adicionado e em seguida a URL. Feito isso, será executado o comando:
`git remote add <nome-fornecido> <url>` no repositório atual.

### [Git Blame](https://marketplace.visualstudio.com/items?itemName=waderyan.gitblame)
Permite você ver o responsável pelas alterações e a has do commit de uma determinada linha dentro do código.
![Blame Preview](./media/blame-preview.gif)

### [Git History](https://marketplace.visualstudio.com/items?itemName=donjayamanne.githistory)
Permite você ver uma representação gráfica de cada commit feito, como está a árvore e ainda comparar as mudanças que foram feitas.![Blame Preview](./media/git-history.gif)
