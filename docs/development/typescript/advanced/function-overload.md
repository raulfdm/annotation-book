# Function Overload

Sabe quando temos uma função que, dependendo do tipo de parametro que passamos, ela pode retornar um tipo diferente?

```ts
type AddParamType = string | number;

function add(p1: AddParamType, p2: AddParamType) {
  if (typeof p1 === "string" || typeof p2 === "string") {
    return p1.toString() + p2.toString();
  }

  return p1 + p2;
}
```

Na função acima - apesar de muito genérica -, dizemos que tanto `p1` quanto `p2` podem ser `string` ou `number`, mas, caso um deles for string, acontecerá a concatenação de strings. Caso ambos sejam números, faremos uma soma matemática.

Acontece que TS fará inferencia de que a função add, tem a seguinte assinatura:

```ts
function add(p1: AddParamType, p2: AddParamType): AddParamType;
```

Perceba que o tipo de retorno é `AddParamType` mas sabemos que isso vai depender de quais os parametros passados. Ora, se um deles for string, o retorno vai ser string. Se ambos forem numbers, o retorno será number.

E o efeito ruim disso, é que caso eu guarde o retorno da função em uma variável, eu não poderei chamar os métodos daquele tipo:

```ts
const result = add("Raul ", "de Melo");
result.split(" "); /* Property 'split' does not exist on type 'AddParamType'.
  Property 'split' does not exist on type 'number'.(2339) */
```

`Function overload` vem pra resolver exatamente esse caso:

```ts
type AddParamType = string | number;

function add(p1: string, p2: number): string;
function add(p1: number, p2: string): string;
function add(p1: number, p2: number): number;
function add(p1: string, p2: string): string;
function add(p1: AddParamType, p2: AddParamType) {
  if (typeof p1 === "string" || typeof p2 === "string") {
    return p1.toString() + p2.toString();
  }

  return p1 + p2;
}
```

Dessa forma, informamos TS que:

1. Se receber string e number, o retorno será string;
1. Se receber number e string, o retorno será string;
1. Se receber string e string, o retorno será string;
1. Se receber number e number, o retorno será number;

TS entenderá essa definição e fará um `merge` entre todas as assinaturas. Logo, o código de chamada anterior passará a funcionar:

```ts
const result = add("Raul ", "de Melo");
result.split(" "); // ✅
```

Perceba que esse código é exclusivo TS, ou seja, será removido durante a compilação:

```ts
"use strict";
function add(p1, p2) {
  if (typeof p1 === "string" || typeof p2 === "string") {
    return p1.toString() + p2.toString();
  }
  return p1 + p2;
}
const result = add("Raul ", "de Melo");
result.split(" ");
```
