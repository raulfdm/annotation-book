# Type Casting

Conversão de tipos é uma feature que nos ajuda a trabalhar melhor com TS pelo simples fato de que às vezes a ferramenta não consegue dar um diagnóstico preciso do que estamos tentando fazer.

Imagine se estamos utilizando TS no front-end e queremos pegar um elemento `p` no dom:

```ts
const paragraph = document.querySelector("p");
```

TS definirá que o `paragraph` tem o tipo `HTMLParagraphElement | null`, o que é acertado, afinal:

1. HTMLParagraphElement -> `p` é um paragraph element
2. null -> o elemento pode não estar lá

Mas e se precisássemos pegar por id?

```ts
const paragraph = document.querySelector("#my-paragraph");
```

Agora, `paragraph` é do tipo `Element | null`.

A diferença nesse caso não tanta, pois `Element` e `HTMLParagraphElement` tem quase as mesmas propriedades. Entretanto se tivessemos um input element, não poderiamos acessar várias propriedades exclusivas de um input:

```ts
const inputName = document.querySelector("#input-name")!;

console.log(inputName.value); // Property 'value' does not exist on type 'Element'.(2339)
```

!> a exclamação no final significa um "ignore o nulo, eu tenho CTZ que o elemento estará disponível".

A única forma de passar esse erro, é fazendo uma conversão de tipos, ou seja, dizendo para TS que aquele elemento que estamos tentando pegar é do tipo `HTMLInputElement`, e para isso, temos algumas formas diferentes.

## Angle brackets < >

Uma das formas é usar o sinal de maior e menor e no meio, o tipo que queremos converter:

```ts
const inputName = <HTMLInputElement>document.querySelector("#input-name")!;

console.log(inputName.value);
```

Essa abordagem funciona, mas em React por exemplo, haverá errors pois a ferramenta entenderá que `<HTMLInputElement>` é um elemento `JSX` e tentará compilar erroneamente.

## as

A forma mais safe é usando o operator `as`:

```ts
const inputName = document.querySelector("#input-name")! as HTMLInputElement;

console.log(inputName.value);
```

Tem o exato mesmo efeito do primeiro modelo, mas com uma sintaxe diferente.

## ! operator

Como dito anteriormente, `!` é uma forma de dizer para o TS:

> dev: "Olha, eu tenho CERTEZA que o elemento estará lá, pode desativar essa validação de `null`! :)
>
> TS: "OK, por sua conta e risco (desativando regra...)".

Mas lembre-se de que essa validação é apenas em tempo de compilação. Caso desejarmos fazer uma validação em tempo de execução, precisamos fazer o velho `if`:

```ts
const inputName = document.querySelector("#input-name"); // Element | null

if (inputName) {
  console.log((inputName as HTMLInputElement).value);
}
```

Perceba que mudamos nossa conversão de tipos de lugar. Isso se da pelo fato de que se fizermos a conversão lá em cima, TS entenderá que ele só pode ser do tipo `HTMLInputElement` e não nullo.
