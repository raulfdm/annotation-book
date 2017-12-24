# Classe de Caracteres

Classe de caracteres são classes que definimos quais os caracteres que podem aparecer em determinada posição.

Seu uso é feito através de colchetes `[]`. Quando utilizamos classe de caracteres, não precisamos mais ESCAPAR (`usar barra \`) da expressão, ou seja, um metachar dentro da classe, será avaliado como seu valor literal, exemplo:

```javascript
//Ponto direto na expressão
const regex = /\./;

//Ponto na classe
const regex = /[.]/;
```

## Excessão

O `-` dentro de uma classe não tem seu valor literal. Ele indica **ATÉ**, ou seja, `[x-y]` indica `x até y`. Exemplo real:

```javascript
//Sem usar hífem
const regex = /[0123456789]/;

//Usando hífem
const regex = /[0-9]/;
```
