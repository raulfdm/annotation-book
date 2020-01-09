# Types

<!-- TODO: Write Basics -->

## Hash Map or Index Properties

Às vezes precisamos definir tipos para objetos na qual não sabemos as propriedades. Para esses casos, podemos:

```ts
type HashMap = {
  [key: string]: string;
};

// ou interface

interface IHashMap {
  [key: string]: string;
}
```

Estamos dizendo que `key` é dinamico e precisa ser do tipo string, o que é um pouco óbvio, afinal, em objetos comuns (não Map), `key` é sempre uma string.

Já com o valor ser do tipo `string`, isso vai depender de que tipo de objeto você espera. Poderia ser `unknown`, `any`, algum tipo próprio.

## Unknown

> Presente a partir da versão 3

O Tipo `unknown` é um tipo-seguro que contrapõe ao tipo `any`, porém, com várias restrições diferentes:

```ts
function addOne(a: any) {
  return a + 1;
}
```

Não temos nenhum erro ao declarar essa operação, afinal, `any` pode ser QUALQUER coisa, inclusive os tipos onde essa operação pode dar certo.

Porém, se definissimos `unknown`, teriamos um erro de compilação:

```ts
function addOne(a: unknown) {
  return a + 1; //Object is of type 'unknown'.(2571)
}
```

Neste caso, um uso possível seria de uma função que pode retornar algum tipo que a gente nem imagina:

```ts
function addOne(a: any): unknown {
  return a + 1;
}

const value = addOne(2); // 3
const string = addOne("hey "); // hey 1
```

Mas qualquer variável que use essa função, terá o tipo inferido de `unknown`:

```ts
//const value: unknown
const value = addOne(2);
```

Uma forma de contornarmos isso é utilizando casting, afinal, sabemos o que a função fará e sabemos o que estamos passando (nesse caso, claro):

```ts
//const value: number
const value = addOne(2) as number;
```

## Never

O tipo `never` é usado para definir retorno de função que NUNCA retornarão nada, como é o caso de uma função que tem o objeto de dar `throw` em um erro:

```ts
// Function returning never must have unreachable end point
function error(message: string): never {
  throw new Error(message);
}

// Inferred return type is never
function fail() {
  return error("Something failed");
}
```
