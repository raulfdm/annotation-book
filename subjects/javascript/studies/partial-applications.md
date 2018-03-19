# Partial Application (Bind)

As vezes temos casos onde precisamos compor funções, entretanto, composição é sempre um lugar muito abstrato.

> A + B = C

Imagine uma situação onde temos uma fução que soma dois valores:

```js
const sum = (a, b) => a + b;
```

Então, temos um valor padrão (ficticio) e queremos somar diferentes valores nele:

```js
const PI = 3.14;

const sum = (a, b) => a + b;

console.log(sum(PI, 10.124)); // 13.264000000000001
console.log(sum(PI, 12.00023)); // 15.14023
console.log(sum(PI, 9.010013)); // 12.150013000000001
```

Mas, perceba que precisamos passar TODA VEZ o valor de `PI`. E se quisermos deixar isso fixo?

Bem, pra isso, podemos criar uma segunda função que vai receber apenas o número que queremos somar no PI e devolver a soma, ainda utilizando o `sum`. Confuso? olha o caso:

```js
const PI = 3.14;

const sum = (a, b) => a + b;

// Nova função
const sumWithPI = sum.bind(null, PI);

console.log(sumWithPI(10.124)); // 13.264000000000001
console.log(sumWithPI(12.00023)); // 15.14023
console.log(sumWithPI(9.010013)); // 12.150013000000001
```

O método `bind` é presente em todas as `function`. Ele permite a criação de uma nova função. Os parâmetros que ele aceita, são:
 - **1o**: Qual o contexto, ou seja, o `this`. Podemos alterar o contexto da função ou não. Caso não seja necessário mudar seu contexto, passar `null`
 - **2o...n**: Os paramêtros que a função que está sendo usada vai receber. Perceba que no nosso exemplo, passamos `PI` como segundo parâmetro, isso sigfica que `a` vai receber FIXO `PI`, ou seja, teremos algo assim:
    ```js
    sum(PI, b) => PI + b
    ```

    Ainda nessa lógica, caso passarmos dois parâmetros (excluindo o contexto), a função soma terá os dois valores fixos, exemplo:
    ```js
    // ... código antiror
    const sumWithPI = sum.bind(null, PI, 2);
    console.log(sumWithPI(10.124)); // 5.140000000000001
    console.log(sumWithPI(12.00023)); // 5.140000000000001
    console.log(sumWithPI(9.010013)); // 5.140000000000001
    ```

    ou seja, `a` foi substituido por `PI` e `b` foi substituido por `2` e o parâmetro enviado será desconsiderado.

