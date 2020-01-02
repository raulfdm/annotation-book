# Function Type

Funções em JS nada mais são que objetos com super poderes.

Nessa perspectiva, podemos também definir contratos (interfaces) para funções, por mais estranho que isso possa parecer:

```ts
function sum(num1: number, num2: number) {
  return num1 + num2;
}
```

Ao criarmos uma interface para essa função, seria:

```ts
interface Sum {
  (num1: number, num2: number): number;
}
```

A sintaxe é a mesma de que sempre usamos, porém, não definimos a assinatura em uma `key`. Seria como se tivesse uma `anonimous function` dentro da interface. Logo, podemos dizer que:

```ts
interface Sum {
  (num1: number, num2: number): number;
}

interface CustomMath {
  sum: Sum;
  readonly PI: number;
}

const math: CustomMath = {
  PI: 3.14,
  sum(n1: number, n2: number) {
    return n1 + n2
  }
};
```
