# Rebase

O comando `rebase` é muito util quando queremos apenas pegar o que já existe em outro repositório ou até mesmo pegar aquelas novas features, sem ter que fazer um merge.

> Mas, qual a diferença entre o Merge e o Rebase?

A grande diferença é como a árvore de logs é criada, veja a imagem abaixo:
![git merge vs rebase](./media/git-mervge-vs-rebase.png)

Perceba que quando fazemos um merge, a nossa árvore é divida no master (linha principal) e o branch que estamos trabalhando atualmente, seja pra implementar algo ou fazer uma pequena correção.

Já no rebase, o nosso branch atual será um como um commit normal no nosso log, entrando na ordem cronológica.

Então, às vezes não queremos sujar nosso log com algo tipo "Arrumando o Lint". Não faz sentido fazer merge e sujar nossa three para algo assim. Nesse caso, o `rebase` seria ideal.

## Caso real

Estamos no branch `bugfix validation`. Porém, houveram várias mudanças no nosso branch espelho (`master`), sendo uma delas, necessária para o nosso problema.

Neste caso, queremos apenas atualizar a nossa code base pra depois fazer o merge. Assim, faremos:

```sh
git rebase master
```

E todas as alterações que foram feitas depois que nosso branch foi criado serão aplicadas ao nosso branch atual.

Dessa maneira, evitamos fazer um merge e criar um log desnecessário só para pegar as mudanças.
