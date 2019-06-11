# Ping

Quando a gente pinga em algo servidor, através do protocolo icmp, fazemos um teste em um servidoor:

```bash
# Exemplo no mac
ping google.com
```

Nos é dado como resposta algo semeelhante a:

```
PING www.google.com (172.217.17.36): 56 data bytes
64 bytes from 172.217.17.36: icmp_seq=0 ttl=54 time=14.968 ms
64 bytes from 172.217.17.36: icmp_seq=1 ttl=54 time=11.057 ms
64 bytes from 172.217.17.36: icmp_seq=2 ttl=54 time=11.556 ms
64 bytes from 172.217.17.36: icmp_seq=3 ttl=54 time=13.493 ms
--- www.google.com ping statistics ---
4 packets transmitted, 4 packets received, 0.0% packet loss
round-trip min/avg/max/stddev = 11.057/12.768/14.968/1.562 ms
```

Onde:

- linha 1: fala sobre qual o endeço ip e o escrito do site e quais dados estão sendo enviados;
- linha 2-5:
  - Tamanho do dado retornado;
  - De onde (ip);
  - icmp*seq = Internet Control Message Protocol*"Sequence", ou seja, de uma forma incremental (+1), qual o número daquela requisição/resposta;
  - TTL = time to live, ou seja, por quantas máquinas no máximo ele pode passar. Cada máquina decrementa em 1 esse número;
    time: velocidade da resposta;
- linha 7:
  - Quantidade de pacotes enviados;
  - quantidade de pacotes recebidos;
  - Porcentagem de pacotes perdidos;
