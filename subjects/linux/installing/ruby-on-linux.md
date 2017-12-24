# Instalação

1- Primeiro, instale o RVM ([aqui](https://rvm.io/))

2- Após instalado, digite o comando `rvm install ruby` e aguarde a instalação.
Obs.: Caso dê algum erro que contenha a mensagem `Requirements installation failed with status: 100.`, siga esses passos:
 1. Digite o comando `sudo apt-get update` e espere atualizar tudo
 1. Pegue os casos que deram erro (404 e etc), e procure-os na pasta `/etc/apt/sources.list`
 1. Com o nome em mãos, use o comando `sudo rm source-list-com-erro` para remove-los
 1. Tente executar novamente o `rvm install`

3- Após finalizar, confirme se está instalado com `rvm list`:
```sh
rvm rubies

=* ruby-2.4.0 [ x86_64 ]

# => - current
# =* - current && default
#  * - default
```
