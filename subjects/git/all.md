# GIT

## Objetivo
O objetivo deste gist é escrever sobre o Básico de Git para fixar o conhecimento adquirido através do curso básico de git e servir de consulta sempre que necessário.

---

## Lifecycle
O ciclo de vida do Git é definido por 4 estágios:

* Untracked: Quando os arquivos _não_ estão sendo controlados pelo Git;
* Unmodified: Quando os arquivos já estão sendo controlados pelo Git, e não sofreram alteração nenhuma;
* Modified: Quando um arquivo que está no controle do Git, foi modificado, com relação à ultima versão dele;
* Staged: Quando adicionamos (```git add <arquivo>```) as mudanças no arquivo (estão prontos para commitar).

Abaixo, uma imagem extraída da documentação oficial do GIT sobre seu ciclo de vida:

![Git lifecycle](https://git-scm.com/book/en/v2/book/02-git-basics/images/lifecycle.png)

---

## Configurações
É possível fazer diversas configurações quando usamos Git. Eu gosto de dividir em duas partes, são elas:

### Obrigatórias
São duas configurações básicas para um funcionamento `ok` do Git:

1. _user.name_: Onde ficará guardado o seu nome (ou apelido) para identificar você;
1. _user.email_: Onde ficará guardado o seu e-mail, que também será usado para sua identificação;

Ambas as configurações acima, são necessárias para identificar o autor dos commits e "quem é que ta trabalhando" no determinado repositório.

Podemos fazer uma configuração no proprio repositório ou uma configuração global. Eu particularmente prefiro fazer global, pois, no meu caso, eu só atuo em projetos particulares, usando sempre o mesmo e-mail. Assim, configuramos com o comando:

* Nome: `git config --global user.name "<seu nome aqui>"`
* E-mail: `git config --global user.email "<seu email aqui>"`

Para saber quais são as configurações já realizadas, basta digitar `git config --global --list`, que toda a configuração global será listada. Já as configurações do repositório, retire o `--global`.

### Opcionais e interessantes
O Git também possui uma infinidades de configurações bacanas, segue abaixo algumas:

#### core.editor
Por padrão, o git usa o VIM para ações que você precisa escrever algo. Entretanto, você pode configurar um editor de texto qualquer, basta informar o comando que abre ele (via terminal), por exemplo, o do visual studio code é `code`, logo, faço a seguinte configuração:

`git config --global core.editor code`

#### alias
Podemos também adicionar álias (apelidos) para nossos comandos repetitivos do git. Por exemplo, usamos a todo momento o comando `git status`, que verifca o Status do repositório, logo, podemos adicionar um apelido que quando digitarmos `git s`, executará o status. A configuração segue a seguinte sintaxe:

`git config --global alias.<o meu apelido> <o que eu quero que ele faça>`

Voltando no exemplo do status:

`git config --global alias.s status`

Logo `git status` => `git s`.

### Remover Configurações
Para remover qualquer configuração é bem simples, basta você usar digitar `--unset` e passar qual a configuração que você deseja remover, por exemplo:

`git config --global --unset alias.s` ou então `git config --global --unset user.name`

---

## Iniciando um repositório
Para iniciar um repositório é bem simples, basta entrar na pasta que você deseja começar a versionar e digitar o comando `git init`. Pronto, os arquivos da sua pasta começarão a ser observados pelo GIT.

---

## Vincular a um repositório remoto
Para vincular seu repositório local a um repositório remoto (github, bitbucket, etc.) basta adicionar um `remote`, assim:

`git remote add origin <url do repo>`

A Url geralmente é fornecida pela plataforma, que pode ser SSH ou HTTPS. 

Para listar todos os os repositórios remotos vinculados, digite o comando `git remote`, ou, para mais detalhes, `git remote --v` (Obs.: o *v* é de *verbose*).


## Atualizar a URL de um repositório remoto
Para atualizar a URL do repositório, basta usar o comando `set-url` e a seguinte sintaxe:

`git remote set-url <nome do repo> <nova url>`

---

## Logs

Os logs são muito importantes, pois, eles guardam informações cruciais de todo o commit que foi feito, por exemplo:

```
commit a4b9224913f32d9e254ddd6d6f50e575663c184b                                                                  
Author: Raul F. de Melo <melo.raulf@gmail.com>                                                                   
Date:   Fri Oct 7 14:54:02 2016 -0300                                                                            
                                                                                                                 
    Alterando a pasta na task server 
```

Todo commit possui um "id" de identificação (HASH). Essa hash, vai ser muito útil quando quisermos reverter, resetar ou voltar o projeto até aquele ponto.

Além disso, vem informando o autor, seu e-mail, a data e a descrição (mensagem escrita pelo autor do commit). Logo, temos várias maneiras de puxar o log.

* Mais simples (`git log`): vai trazer os logs como visto acima;
* Mais decorados (`git log --decorate`): vai trazer o log parecido com o de cima, entretanto, informando os branchs, tags, etc;
* Quando usamos branchs (`git log --graph`): vai trazer um gráfico monstrando onde foi feito os commits (em que branch), os mergs e etc.

Após olharmos os logs, talvez queiramos saber mais informações do que foi alterado naquele commit específico. Assim, apenas precisamos pegar sua *Hash* e digitar o comando `git show <numero da hash>`. Um histórico do que foi feito aparecerá no console.

### Diff

Um comando comando bastante interessante para ver mais detalhes do log, é o ```diff```. Com ele, é possível ver as alterações realizadas. Para utiliza-lo, basta descobrir qual a *hash* do log que você quer saber e digitar:

```
git diff <numero-hash>
```

Um exemplo de reposta, é o abaixo:

```
diff --git a/gulpfile.js b/gulpfile.js                                                            
index e80f5dd..f7e9097 100755                                                                     
--- a/gulpfile.js                                                                                 
+++ b/gulpfile.js                                                                                 
@@ -5,7 +5,7 @@ const gulp = require('gulp'),                                                     
                                                                                                  
 gulp.task('babel', function () {                                                                 
                                                                                                  
-    gulp.src('src/js/app-es6/**/*')                                                              
+    return gulp.src('src/js/app-es6/**/*')                                                       
         .pipe(sourcemaps.init())                                                                 
         .pipe(babel({  
             presets: ['es2015']            
```      

---

## Git Stash
O GIT stash é um comando muito útil. Sua principal funcionalidade é "Salvar o estado atual" das modificações relaizadas em arquivo separado e descarta-las apó salvo.

Um exemplo para observarmos seu uso, é o caso onde estamos trabalhando em uma funcionalidade, ainda não terminamos e precisamos parar para fazer outra alteração. Uma solução seria commitar as alterações pela metade mesmo, OU ENTÃO, salva-las para mexer depois. E é aí que entra o git stash.

Nesse exemplo, ele vai gerar um arquivo com as suas alterações como *WIP* (Work In Progress) e voltar pro HEAD (última versão válida de seus arquivos). 

### Gerar Stashs
É possível gerar stash de duas formas:

1. ```git stash``` -> com esse comando, ele vai salvar com informações padrões;
2. ```git stash save '<mensagem>'``` -> com esse comando você consegue salvar um stash com uma mensagem personalizada.

Eu particularmente prefiro a forma 2, pela questão de que se você precisar gerar vários stashs, você consegue identificar qual é qual através da mensagem digitada.

### Ver os stashs
Para ver os stashs existentes, basta digitar: ```git stash list```

### Aplicar Stashs
Para aplicar um stash, pode ser feito de duas formas:

1. ```git stash apply``` -> vai subir o último stash (ou o primeiro, not sure about that)
2. ```git stash appy stash@\{<index-do-stash>\}``` -> sobe o stash escolhido pelo index

Eu novamente primeiro o segundo modo, pois, você consegue definir qual o stash exato que você quer voltar, bastando informar qual o índice dele (o índice é informado no ```git stash list```).

Como qualquer comando, para saber mais detalhes, basta digitar: ```git stash --help```.

---

## Fork e Clone

Ambos os comandos, servem para "puxar" o repositório para você, mas, existe uma diferença crucial entre eles. 

Quando você faz um fork em um projeto, você clona ele para seus repositórios, mas mantém uma referência para o original. Ele é mais usado no caso que desejamos contribuir para algum projeto. Imagine que você esteja olhando um projeto e vê um código que pode melhorar ou que tem algum erro. Logo, você faz um fork do projeto, faz as alterações e depois submete um pull request para o mantenedor do projeto, ou seja, informa o dono que você fez algumas alterações e cabe a ele aceitar ou não.

[Mais informações sobre o fork e contribuição](https://git-scm.com/book/pt-br/v1/Git-Distribu%C3%ADdo-Contribuindo-Para-Um-Projeto)

Já o clone, é basicamente fazer uma cópia de um repositório seu. Imagine que você queira trabalhar no mesmo projeto no computador de casa e no computador da empresa. Ou adicione um parceiro no projeto. O que será feito é um clone, e, quando as alterações forem submetidas por ```push```, ela irá para o repositório de onde foi feito o clone. Por isso, geralmente é para o seu próprio ou para um que você tenha permissão de commitar.

---

## Reset
O reset é uma forma de você desfazer commits e alterações para a ultima versão válida. Assim, temos algumas possibilidades:

#### HEAD
O comando ```git reset HEAD [arquivo]``` será último para voltar de staged (pronto para commitar) para unstagged (pronto para adicionar). Então, imagine que você adiciona (```git add [arquivo]```) errado o arquivo e você quer volta-lo para unstage. Assim, basta informar o comando e passar o nome do arquivo que você quer voltar. Caso queira voltar tudo, basta _não_ informar o nome do arquivo e todos eles voltarão para unstage.

#### Voltando commits
Os comandos tem a mesma sintaxe (`git reset --<tipo> <hash do commit anterior>`). Quando falamos commit anterior, é a hash do commit anterior ao que você quer desfazer, por exemplo:

Commit 3
Commit 2
Commit 1

No caso, você quer desfazer o commit 3, logo, passa no comando a hash do commit 2.

Abaixo, cada tipo explicado.

##### Soft
O `git reset --soft` mantém o arquivo _Staged_, ou seja, somente o commit é desfeito, mantendo as alterações adicionadas (`git add`).

##### Mixed
O comando `git reset --mixed` mantém suas alterações, removendo o commit e o stage (add), logo, os arquivos modificados estarão com o status de _modified_.

##### Hard
O comando `git reset --hard` desfaz TODA a alteração realizada, ou seja, commit, stage e volta o arquivo pro estado anterior, sem nenhuma alteração.

---

## Revert
O comando de __revert__ é parecido com o reset, mas ele é um pouco mais agressivo (ou nem tanto, comparado ao hard). Basicamente, ele reverte todo seu commit, desconsiderando TUDO o que foi feito, por exemplo:

No commit 2 eu fiz a adição de um arquivo X.txt.
Se eu digitar `git revert 2`, ele simplesmente vai excluir aquele arquivo e gerar um novo commit falando: revertemos o commit tal. Você até pode digitar uma mensagem personalizada para isso. Também, você pode reverter o revert. hahahaha eu sei, isso é confuso, mas vamos imaginar nesse exemplo ainda:

Eu reverti o commit 2 e gerou um commit 3 (revert). Caso eu tenha feito errado e queira voltar aquele commit, eu preciso reverter o commit 3, logo `git revert 3` e o arquivo do commit 2 irá aparecer novamente.

---

## Enviando as alterações para um repositório remoto
Esse passo, basicamente é feito com um comando, o `git push <repositório> <branch>`. Assim, é necessário que haja um repositório cadastrado (mencionado nos tópicos anteiores). Exemplo:
```
repositório: origin
branch: master
```
Assim, para submeter as alterações para ele, basta digitar o comando `git push origin master`, que todas as alterações que foram commitadas, serão enviadas através da internet.

---

## Branch
O branch é um _ponteiro móvel_ apontado para algum lugar, geralmente um repositório principal, que carrega consigo alguns commits, por exemplo:
[branch fácil](https://git-scm.com/figures/18333fig0311-tn.png)

Podemos ver que temos dois branchs apontando para o mesmo lugar, o master (principal) e o iss53, que foi criado provavelmente para resolver algum problema específico. Mas, qual a verdadeira vantâgem de trabalhar com branch? Segue abaixo algumas:

* Evita Conflitos: Quando você cria um branch novo, espelhado no principal, por exemplo, você tem toda a estrutura dele, mas em um ambiente controlado, sem perigos para alterações. Assim, você consegue evitar conflitos na hora de submeter suas alterações (nem todos, existe ainda o conflito do merge, mas isso, falaremos mais adiante);
* Não altera o master: como eu disse, você fica isolado. Caso você escreva um código que quebre a aplicação inteira, o master (main branch) estará a salvo;
* Multiplas pessoas trabalhando: É mais fácil você ter várias pessoas trabalhando em algo, sem alterações diretas, apenas com cópias do projeto e posteriomente, elas vão subindo as correções e avaliando o impacto;
* Fácil de desligar: um branch é muito fácil de criar, e muito fácil de desligar. Se você criou para resolver uma funcionalidade X, ao fazer o merge de suas alterações, basta você excluir o branch e fim de papo.

#### Criação
Para criar um branch, basta digitar o comando `git checkout -b <nome-do-novo-branch>` e fim. Lembrando que, ele criará um branch a partir do que você estiver. Assim, se você estiver no master, será cópia do master, se estiver no develop, será cópia do develop, e assim por diante.

#### Listar Branches
Para obter a lista dos branchs criados, basta digitar `git branch` e a lista será exibida.

#### Trocar de Branch
Para trocar de branch, basta dar um checkout no desejado, por exemplo: `git checkout <nome-do-branch>`.

#### Deletar um Branch
Para deletar, basta digitar `git branch -D <nome-do-branch>`. Muito cuidado. Essa operação é sem volta.

#### Deletar um Branch REMOTO
Basta digitar `git push origin :<nome-do-branch>`. O que define mesmo esse comando, são os dois pontos (:).

---

## Merge
Foi dito anteriormente sobre os branchs e sua importância. Mas, depois de ter criado um branch, feito suas alterações, é  necessário mesclar (merge) suas alterações com o branch alvo. Para isso, usamos dois conceitos: o _merge_ e o _rebase_. Neste tópico, falaremos sobre o merge.

O que o merge faz, basicamente é pegar todas as alterações realizadas, pegar o branch de destino e criar um novo commit, mesclando eles, por exemplo:
[merge git](https://git-scm.com/figures/18333fig0317-tn.png)

No exemplo acima, criamos um branch (iss53) a partir de C2, que no caso, era o master. Então, fizemos um commit (C3) em nosso branch, mas não fizemos merge. Em seguida, alguem fez um merge/commit no branch master, gerando o C4. Depois fizemos outro commit no nosso branch __iss53__ e acabamos todas as correções. O próximo passo é realizar o merge. Como dito, ele vai pegar o Commit 3 e Commit 5 e juntar com o Commit 4, gerando o Commit 6. 

Parece confuso né? Mas calma, é simples. A única coisa que ele faz é juntar as alterações e gerar um novo commit falando: `amigo, juntei tudo pra você desse brach para esse`. Mas claro, isso se não der conflitos. Caso haja conflitos, será necessário você fazer as alterações e novos commits manualmente, para depois de resolvido, fazer o merge.

#### Vantagens e Desvantagens
Existem algumas desvantagens nesse método, mas eu particularmente prefiro ele, segue abaixo:

| Vantagem | Desvantagem  | 
| :------: | :----------: |
|Não apaga nada | Log fica Poluído e/ou confuso|
| Mantém histórico do caminho percorrido| Gera um commit só para fazer o processo|

#### Executando
Para executar um merge, basta entrar no branch que você quer receber o commit e digitar o comando `git merge <nome-do-branch-a-mesclar>` e se não houver conflitos, tudo ocorrerá na paz e tranquilidade.
