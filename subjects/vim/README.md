# Minhas anotações sobre o vim

## Comandos

- Para buscar por algo, podemos simplesmente passar '/' e a palavra que queremos procurar (/header)/
- Para desfazer algo (ctrl+z): `u` no modo `normal`
- Para refazer algo (ctrl+shift+z): `ctrl+r` no modo `normal`
- Para adicionar uma nova linha em baixo da linha em foco: `o` no modo `normal`
- Para adicionar uma nova linha ACIMA da linha em foco: `shift + o` no modo `normal`;
- Ir para o começo do arquivo: `gg` no `normal mode`
- Ir para o final do arquivo: `shift + g` no `normal mode`
- Para ir até alguma palavra específica, podemos digitar `/`+ o nome do que queremos. Isso é avaliado como uma expressão regular, logo, caracteres de barra (slash /) precisam ser escapados. Por exemplo
```vim
:/<\/a>
```
Esse comando vai navegar até o primeiro elemento `</a>` encontrado.

Caso você queira navegar para a próxima ocorrência, é possível usar o atalho `n` (next) e caso queira voltar para a ocorrência anterior, `ctrl+n`. Tudo isso, no modo `normal`

- Para substituir algum texto rapidamente, podemos utilizar o comando `%s`. Como isso é um comando, primeiro precisamos entrar no modo de comando através da tecla: `:` e em seguida passar o nosso comandix:
```vim
:%s
```

Dessa forma, precisamos passar qual texto deverá ser substituido, em seguida, pelo o que ele deverá ser substituido em por ultimo, opções para a expressão, tudo isso, separado por barras (/), por exemplo:

```vim
:%s/texto invalido/texto valido/g
```

Assim, temos que:
 - Texto a ser subsituido: 'text invalido'
 - Texto que será colocado no lugar: 'texto valido'
 - Opções:
   - g: significa global

Entretanto, caso tenhamos várias ocorrências desse texto a ser substituido, será feito o replace em todos eles. 

As vezes podemos querer decidir o que mudar exatamente. Para casos como esse, podemos passar além do comando `g`, o comando `c` (choose). Dessa forma, ele fará a varredura em todas as ocorrencias no arquivo e nós quem iremos dizer se queremos alterar ou não aquela ocorrência.

```vim
:%s/texto invalido/texto valido/gc
```
No caso do uso da regex, quando queremos usar algum quantifier como por exemplo o `?`, temos que escapar ele:

```vim
:%s/<\/\?ul>//gc
```
No caso da expressão acima, queremos selecionar todas as `<ul>` e `</ul>` e subsituir por nada.

## Visual Mode
O modo visual é um modo que nos ajuda a fazer seleções de texto mais facilmente. Para acessa-lo, basta digitar o comando `shift-v`

### Comandos
- Para copiar uma linha inteira: `shift-v`
- Depois de copiado, para selecionar linhas acima: seta pra cima ou `k`
- Depois de copiado, para selecionar linhas abaixo: seta para baixo ou `j`
- Para copiar a seleção atual: `y`
- Para colar o texto copiado: `p`

## Visual Block
O modo visual block é um modo que ajuda a selecionar partes do texto também, mas diferente do `line`, ele enxerga o texto como blocos. Ideal para os casos onde queremos remover textos errados em blocos.

Para entrar nesse modo, basta digitar `ctrl+v`

## Divisão de tela
As vezes precisamos abrir dois arquivos um do lado do outro. O vim possui uma solução pra isso e nos permite abrir dentro dele quantos arquivos quisermos lado a lado, ou um em cima do outro.

### Lado a lado
Para dividirmos lado a lado, precisamos no modo de `comando`, passar o comando `vs` e em seguida o caminho ou nome do arquivo que queremos alterar, exemplo:

```
:vs css/index.css
```

Isso abrirá o arquivo `index.css` verticalmente ao arquivo que já está aberto.

### Um embaixo do Outro
Para uma aba não vertical, temos o comando `sp`. Logo, ele funciona da mesma forma que o comando `vs`, ou seja, no modo de `comandos` passamos `sp` + `o path+nome do arquivo`:

```
:sp css/index.css
```

### Trocando de tela
Para trocar entre os arquivos abertos, o atalho no mod `normal` é o `ctrl + ww`
 
## Plugins
As vezes precisamos de algumas ferramentas para poder nos ajudar com alguma tarefa manual. Essa é uma das finalidades de um plugin.

Entretanto, instalar um plugin manualmente pode ser uma dor de cabeça, logo, é recomendado que usemos um gerenciador de plugins.

Para tal missão, usaremos o [Pathogen](https://github.com/tpope/vim-pathogen). Mas antes, precisamos configurar o ambiente.

### Criando as pastas
No HOME do vim, precisamos criar uma pasta `.vim`. Caso você não saiba onde é a HOME, entre no vim sem nenhum arquivo e no modo de comando digite `:echo $HOME`.

Dentro da pasta nova (`.vim`), devemos criar uma pasta chamada `autoload` e a outra pasta chamada `bundle`.

#### AutoLoad
Autoload é a pasta que contém tudo que o VIM vai executar antes de ser iniciado.

#### bundle
Bundle é a pasta que o Pathogen vai carregar ao ser inicializado.

### Baixando o Pathogen
Após criadas as pastas, precisamos baixar o Pathogen dentro da pasta `autoload`:

```bash
curl -LSso ~/$HOME/.vim/autoload/pathogen.vim https://tpo.pe/pathogen.vim
```

