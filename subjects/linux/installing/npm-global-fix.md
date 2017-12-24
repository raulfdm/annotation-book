# Correções para o path global (LINUX)

1. Digite o comando `npm config get prefix`
1. Copie o Caminho impresso
1. Abra o arquivo das variavés de ambiente `sudo gedit /etc/environment`
1. Adicione o caminho obtido no config do **npm** às pastas *bin*, *lib* e *etc*
   - `:/<path>/bin`
   - `:/<path>/etc`
   - `:/<path>/lib`
  
1. O resultado será parecido com o abaixo:
```
PATH="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/home/raul/.npm-global/bin/:/home/raul/.npm-global/lib/:/home/raul/.npm-global/etc/"
```
