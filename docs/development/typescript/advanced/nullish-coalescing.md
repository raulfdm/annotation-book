# Nullish Coalescing

Essa funcionalidade vem pra resolver o seguinte problema:

```js
const agreedWithTerms = false;

const user = {
  name: "Raul",
  agreedWithTerms: agreedWithTerms || true
};

console.log(user); // { name: 'Raul', agreedWithTerms: true }
```

Perceba o problema, quando fazemos a condicional `ou` (`||`), JS nativamente considera o primeiro valor como `falsy`, ou seja, será entendido como falso:

| valores "falsy" |
| --------------- |
| `''`            |
| `0`             |
| `NaN`           |
| `false`         |
| `null`          |
| `undefined`     |

> https://developer.mozilla.org/en-US/docs/Glossary/Falsy

Só que no fim, o que queriamos era dizer que se `agreedWithTerms` for `undefined` ou `null`, então assuma como valor padrão `true`.

Nullish coalescing vem pra resolver EXATAMENTE essa questão, pois somente considera undefined ou nullo para retornar o valor padrão:

```ts
const agreedWithTerms = false;

const user = {
  name: "Raul",
  agreedWithTerms: agreedWithTerms ?? true
};

console.log(user); // { name: 'Raul', agreedWithTerms: false }
```

Que no fim é convertido de:

```text
se for falsy, retorne `true`
```

para:

```text
se for `undefined` ou `null`, retorne `true`
```
