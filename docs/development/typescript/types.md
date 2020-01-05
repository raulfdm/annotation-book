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
