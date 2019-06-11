# Traceroute

É uma forma de fazer a avaliação do caminho utilizado até o destino, a partir do protocolo ICMP.

Quando digitamos por exemplo:

```
traceroute google.com
```

Veremos algo semelhante a:

```
$ traceroute google.com
traceroute to google.com (172.217.17.46), 64 hops max, 52 byte packets
 1  xiaoqiang (192.168.31.1)  2.713 ms  2.399 ms  1.053 ms
 2  192.168.178.1 (192.168.178.1)  1.618 ms  2.048 ms  1.647 ms
 3  * * *
 4  gv-rc0052-cr102-ae99-0.core.as9143.net (213.51.174.229)  12.072 ms  12.037 ms  12.727 ms
 5  asd-tr0021-cr101-be156-2.core.as33915.net (213.51.5.38)  14.362 ms  14.508 ms  20.668 ms
 6  nl-ams14a-ri1-ae51-0.aorta.net (213.51.64.186)  14.086 ms  14.261 ms  14.039 ms
 7  74.125.146.228 (74.125.146.228)  14.324 ms  13.965 ms  13.581 ms
 8  108.170.241.225 (108.170.241.225)  14.729 ms
    108.170.241.193 (108.170.241.193)  15.218 ms  14.741 ms
 9  108.170.236.137 (108.170.236.137)  12.653 ms
    108.170.236.135 (108.170.236.135)  20.204 ms
    108.170.236.137 (108.170.236.137)  19.090 ms
10  ams16s29-in-f14.1e100.net (172.217.17.46)  14.070 ms  15.690 ms  16.891 ms
```

Onde:
  - linha 1:
    - pra onde se está fazendo a avaliação;
    - hops max: Quantidade de "saltos" máximo;
    - Tamanho do pacote
  - Linhas sem "*": 
    - Alias do servidor;
    - Endereço IP;
    - Tempo de resposta dos 3 pacotes enviados;
  - Linhas com "*";
    - Significam que o servidor na qual a gente tentou estabelecer a conexão desabilitou conexões ICMP por:
      1. Segurança. Evitar possiveis iniciativas de ataques hacker;
      2. Evitar trafego desnecessário;
  - Última linha: máquina destino (servidor do google);
