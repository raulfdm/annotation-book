# Como instalar o Franz no Linux e ter vários mensageiros no mesmo app

Para instalar o Franz no Linux e ter vários mensageiros no mesmo app, você só precisa fazer o seguinte:

1. Abra um terminal;
  1. Caso já tenha feito alguma instalação manual, apague a pasta, o link e o atalho anterior com esse comando;
  ```shell
  sudo rm -Rf /opt/franz*
  sudo rm -Rf /usr/bin/franz
  sudo rm -Rf /usr/share/applications/franz.desktop
  ```

1. Confira se o seu sistema é de `32 bits` ou `64 bits`, para isso, use o seguinte comando no terminal:
  ```
  uname -m
  ```

  ### 32 bits
  Caso seu sistema seja `32bits`, use o comando abaixo para baixar o programa (Se o link estiver desatualizado, acesse essa página, baixe a última versão e salve-o com o nome **franz.tgz**):
  ```sh
    wget https://github.com/meetfranz/franz-app/releases/download/4.0.4/Franz-linux-ia32-4.0.4.tgz -O franz.tgz
  ```

 ### 64 bits
  Caso seu sistema seja `32bits`, use o comando abaixo para baixar o programa (Se o link estiver desatualizado, acesse essa página, baixe a última versão e salve-o com o nome **franz.tgz**):
   ```sh
    wget https://github.com/meetfranz/franz-app/releases/download/4.0.4/Franz-linux-x64-4.0.4.tgz -O franz.tgz
  ```

1. Crie uma pasta para o programa:
  ```sh
  sudo mkdir /opt/franz
  ```

1. Descompact os arquivos do `.tgz` baixado na pasta criada anteriormente

  ```sh
  sudo tar -vzxf franz.tgz -C /opt/franz/
  ```

1. (opciona) Crie um atalho para facilitar a execução do programa:

  ```sh
  sudo ln -sf /opt/franz/Franz /usr/bin/franz
  ```

1. Se seu ambiente gráfico atual suportar, crie um lançador para o programa:

  ```shell
  echo -e '[Desktop Entry]\n Version=1.0\n Name=franz\n Exec=/opt/franz/Franz\n Icon=/opt/franz/resources/app.asar.unpacked/assets/franz.png\n Type=Application\n Categories=Application' | sudo tee /usr/share/applications/franz.desktop
  ```

Pronto! Agora, quando quiser iniciar o programa, digite franz em um `terminal`, seguido da tecla TAB. Ou então, se a sua distribuição suportar, coloque o atalho na sua área de trabalho usando o gerenciador de arquivos do sistema ou os comandos abaixo, e use-o para iniciar o programa.

```bash
sudo chmod +x /usr/share/applications/franz.desktop

# Se seu SO estiver em portugues
cp /usr/share/applications/franz.desktop  ~/Área\ de\ Trabalho/
## ou
# Se o seu SO estiver em inglês
cp /usr/share/applications/franz.desktop ~/Desktop
```


### Fonte
[http://www.edivaldobrito.com.br/whatsapp-skype-hangouts-e-outros-mensageiros-no-mesmo-lugar/](http://www.edivaldobrito.com.br/whatsapp-skype-hangouts-e-outros-mensageiros-no-mesmo-lugar/)
