# Aumentando a velocidade do Linux

## Swapiness
Este é um ponto importante, a memória SWAP ajuda o sistema a trabalhar quando muitas aplicações estão sendo executadas, o caso é que em computador mais novos, especialmente os que tem mais de 2 GB de RAM a memória SWAP nem precisaria ser utilizada. O padrão de Swapiness do Ubuntu é 60, numa escala que vai de 0 até 100, isso significa que quando você estiver usando 40% da sua memória, ou seja, 60% da sua memória estiver livre alguns pequenos arquivos começarão a ser passados para o SWAP no HD, como é de se esperar o HD é muito mais lento do que a memória RAM, o que vamos fazer é modificar a prioridade da Swapiness para 10%.

### Aplicando
Abra o terminal e cole os seguintes comandos para testar:

```bash
sudo sysctl vm.swappiness=10
```

A vantagem de usar este comando é que o Swapiness é definido para 10 somente nessa sessão, use o computador para ver se você sente alguma diferença no uso, caso tenha obtido melhoras vamos tornar essa modificação permanente com os comandos:

```bash
sudo gedit /etc/sysctl.conf
```
No arquivo que se abrir, cole a seguinte linha do final:

```bash
vm.swappiness=10
```

Reinicie o computador: 
```bash
sudo reboot
```

Depois de reiniciar para confirmar que a Swapiness ficou definida em 10 execute o comando abaixo:

```bash
cat /proc/sys/vm/swappiness
```

---

## Prelink
Para quem ainda não conhece, o Prelink é um software livre escrito por Jakub Jelínek da Red Hat para sistemas operacionais compatíveis com o POSIX, principalmente o GNU/Linux, porque ele modifica executáveis ELF. Ele destina-se a aceleração de um sistema, reduzindo o tempo que um programa precisa para iniciar. Esta é uma ferramente que já vem instalada por padrão no Diolinux OS.

Para instalar no Ubuntu abra o terminal e cole o seguinte comando:
```bash
sudo apt-get install prelink
```

Depois de instalado rode o seguinte comando para abrir o arquivo de configuração do Prelink:
```sh
sudo gedit /etc/default/prelink
```

Procure a linha `PRELINKING=unknown` e muda para `PRELINKING=yes`

Agora execute o Prelink para que ele possa linkar as bibliotecas dos programas:
```bash
sudo /etc/cron.daily/prelink
```
A primeira vez deve demorar um pouco mais, espere o processo com calma até que o terminal volte ao seu estado normal, repita esse comando de tempos em tempos, especialmente quando você instalar ou desinstalar programas

---

## Melhorando o tempo de boot 
Como todo o sistema existem aplicativos que se iniciam juntamente com o Ubuntu, procure na Dash por "Aplicativos de Sessão" porém por padrão o Ubuntu não mostra todos os serviços que são iniciados juntamente com o sistema, para exibir todas as entradas rode o seguinte comando:

```sh
sudo sed -i s/NoDisplay=true/NoDisplay=false/g /etc/xdg/autostart/*.desktop
```

Agora entre novamente em aplicativos de sessão e estarão disponíveis vários serviços que você pode desabilitar a seu gosto.

Com esse procedimentos o Ubuntu deverá ficar um pouco mais rápido, até a próxima dica.

### Fonte
[Seu Ubuntu ficou mais lento depois de um tempo? Aprenda a acelerá-lo novamente](http://www.diolinux.com.br/2013/05/ubuntu-lento-como-deixar-rapido.html)
