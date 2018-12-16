# Casting

O casting é simplesmente o fato de fazer uma conversão de um valor em outro valor. Ele pode acontecer de duas formas, explícito e implícito.

## Implícito
No mundo javascript, podemos ter a seguinte operação:

```javascript
const a = "3"

console.log(typeof a) //> string
console.log(a - 2) //> 1

```
Se a constante *a* era uma string, como foi possível realizar uma operação matemática? Sim, casting implícito. O javascript tenta fazer a conversão do valor, como se fosse um `parseInt(a)`, e o valor retornado fosse usado na conta. Ou seja, no momento da operação, ele converte implicitamente o nosso valor.

## Explicito
Não temos tipagem forte no Javascript, mas com o Typescript temos. Para fazer um casting explícito, ou seja, dizer que queremos converter aquele valor, usamos sinal de maior e menor antes do valor, por exemplo:

```typescript
let myText: any = "Raul de Melo"
let myTextSize: number = (<string>myText).lenght
```

Dessa maneira, convertermos o tipo any para String e temos acesso ao seus métodos.
