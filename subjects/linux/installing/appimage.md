# Instalação de arquivos APPIMAGE

Arquivos appimage são pacotões executáveis. Para instala-los, é necessário primeiro dar permissão:

```bash
chmod a+x <nome-do-arquivo>
```

Em seguida, basta executar:

```bash
./<nome-do-arquivo>
```

## Local para instalacao
Criar uma pasta na home (`~`) chamada `programs` e colocar lá para ficar fácil manutencao.

## Deletar arquivo desktop
Geralmente está nesses locais:
- /usr/share/applications
- /usr/local/share/applications
- ~/.local/share/applications
