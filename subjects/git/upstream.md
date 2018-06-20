# --set-upstream

`--set-upstream` no git é a forma de dizer qual é o branch que ele deverá ficar ouvindo alterações, ou seja, se você precisar faze rum rebase por exemplo, qual branch deverá ser usado como base.

Exemplo:

Comando base:

```sh
git branch --set-upstream-to={remote}/{branch} {local-branch}
```

Comando real:

```sh
git branch --set-upstream-to=origin/master my-branch
```

Nesse caso, definimos que `my-branch` usará como base o branch remoto `origin/master`.
