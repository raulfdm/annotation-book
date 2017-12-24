# Atalhos terminal linux

Para criar atalhos dos comandos mais usados no terminal, precisamos editar o arquivo `~/.bashrc` e adicionar a nomenclatura `alias atalho=comando`, por exemplo:

```bash
#...
# some more ls aliases

alias upg='sudo apt-get upgrade'

#...
```

Para editar o arquivo basta abri-lo com qualquer editor (no meu caso, o padrão é o pluma) e adicionar o atalho:
```bash
$ sudo pluma ~/.bashrc
```

## OH_MY_ZSH
Caso você utilize o `oh-my-zsh`, basta você criar um arquivo na pasta libs e gravar os seus atalhos:
```bash
$ sudo touch ~/.oh-my-zsh/libs/my-hotkeys.zsh
$ sudo pluma ~/.oh-my-zsh/libs/my-hotkeys.zsh
```

Salvando e dando reload no terminal, seus comandos estarão disponíveis!
