# Generics

Tipos genéricos existem em diversas linguagens fortemente tipadas. Eles auxiliam os casos onde não queremos definir explicitamente o tipo recebido.

Antes de criar os nossos próprios tipos genéricos, vamos ver os que existem dentro de TS:

## Built-in generics

Vamos imaginar que queremos criar uma lista e dizer o tipo dela:

```ts
const listOfNames: [] = [];
```

Estamos dizendo que `listOfNames` será do tipo array vazio (o que não faz muito sentido). Se tentarmos adicionar um nome na lista, teremos um erro:

```ts
listOfNames.push("Raul"); // Argument of type '"Raul"' is not assignable to parameter of type 'never'.
```

Ora, sabemos que `name` sempre será string, logo, podemos dizer que nosso array será um array de strings:

```ts
const listOfNames: string[] = [];
listOfNames.push("Raul");

console.log(listOfNames); // ["Raul"]
```

Poderíamos definir que esse array recebe qualquer tipo:

```text
number[]
string[]
User[]
```

Porém, essa é a forma simplificada de declarar um Array tipado. Ao utilizarmos o `Array` generics do TS, teríamos o mesmo resultado:

```ts
const listOfNames: Array<string> = [];
listOfNames.push("Raul");

console.log(listOfNames); // ["Raul"]
```

Assim, podemos dizer que `Generics` sempre terão a assinatura:

1. Nome do tipo
1. `<`
1. Lista de tipos esperados
1. `>`

```text
Generic<type>
```

Outro exemplo de built-in generics é o tipo `Promise`.

Vamos imaginar que temos uma função que retorna uma promise e como resultado, uma string:

```ts
function getString() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve("Your string is here, baby");
    }, 3000);
  });
}

getString().then(str => {
  console.log(str.split(" ")); // Property 'split' does not exist on type 'Promise<unknown>'.(2339)
});
```

TS não é capaz de entender que a promise resolverá uma string e infere que `str` será do tipo `Promise<unknown>`, o que nos impede de chamar qualquer método string em `str`.

Para corrigir isso, podemos usar o generics Promise e dizer que o retorno será do tipo string:

```ts
function getString(): Promise<string> {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve("Your string is here, baby");
    }, 3000);
  });
}

getString().then(str => {
  console.log(str.split(" ")); // ✅
});
```

## Custom Generics

Podemos também criar nossos próprios tipos genéricos. Para ver como seria essa criação, vamos imaginar uma função bem boba que tem como proposito, dado um objeto e uma key, retornar o valor daquela key:

```js
// Vanilla js
function getProp(obj, key) {
  return obj[key];
}

console.log(getProp({ name: "Raul" }, "name")); // Raul
```

Como podemos definir o tipo dessa função? Bem, podemos dizer que `obj` é sempre um `object`, `key` sempre uma `string` e o retorno pode ser `any`, afinal, não sabemos o valor guardado.

```ts
function getProp(obj: object, key: string): any {
  return obj[key]; // Error: Element implicitly has an 'any' type because expression of type 'string' can't be used to index type '{}'.
  //No index signature with a parameter of type 'string' was found on type '{}'
}
```

Acontece que ao definir essa estrutura, TS nos dá um erro dizendo que não existe nenhuma `key` do tipo string em um `{}`. Sim, quando definimos type `object`, é um objeto vazio (`{}`).

Para além disso, dizemos que `key` é do tipo `string`, que pode ser QUALQUER coisa. A única maneira de fazer uma declaração dessa dar certo, é definindo a exata estrutura de `obj` e os exatos parametros possíveis:

```ts
function getProp(obj: { name: string; age: number }, key: "name" | "age"): any {
  return obj[key];
}

console.log(getProp({ name: "Raul", age: 80 }, "name")); // Raul
console.log(getProp({ name: "Raul", age: 80 }, "age")); // 80
```

Sem problemas de compilação, mas, deu pra perceber que perdemos a flexibilidade? Definimos tipos específicos para o objeto e as keys. Não poderemos reutilizar essa função em nenhum outro contexto, mesmo sendo uma função utilitária.

Bom, é para resolver este tipo de problema que `Generics` existem.

Para resolver essa questão, faremos:

```ts
function getProp<T, U>(obj: T, key: U): any {
  return obj[key]; //Type 'U' cannot be used to index type 'T'
}
```

!> Em genérics, existe uma convenção de usar apenas a primeira letra do que você quer representar. Caso os próximos tipos também sejam da mesma "representação", segue-se a ordem do alfabeto.

No caso, dizemos T (que vem de `Type`), pode ser qualquer um que você passar como objeto e `U`, também pode ser qualquer um que você passar.

Mas, ainda assim teremos um erro, afinal, `U` não necessariamente é uma chave de `T`. E aí entra o conceito de `Constraints` dentro de Generics.

## Constraints

É quando queremos limitar o que pode ou não pode ser no tipo genérico.

No caso da função `getProp` queremos que:

1. `T` seja do tipo `object`, mas QUALQUER object;
1. `U` esteja presente em `T`, ou seja, se passarmos um objeto `{name: 'raul'}`, queremos que o único valor possível de `key` seja `name`;
1. `U` ainda seja do tipo `string`. Se deixarmos aberto, `U` pode ser QUALQUER coisa que você passar, inclusive numbers, functions, outros objects.

Como definimos então essas regras?

```ts
function getProp<T extends object, U extends keyof T>(obj: T, key: U): any {
  return obj[key];
}

console.log(getProp({ name: "Raul", age: 80 }, "name")); // Raul
console.log(getProp({ name: "Raul", age: 80 }, "age")); // 80
```

Para definir `constraints`, usamos a keyword `extends`, que no fim, define uma regra.

#### `T extends object`.

Nessa afirmação, dizemos que T só pode ser do tipo `object`. Se tentarmos passar qualquer outro tipo, receberemos um erro:

```ts
console.log(getProp(true, "age")); // Argument of type 'true' is not assignable to parameter of type 'object'.(2345)
```

### `U extends keyof T`

`keyof` é um `utility` que nos permite olhar para dentro de um objeto de pegar todas as keys dele.

Logo, dizemos que `U` pode ser QUALQUER key presente em `T`.
