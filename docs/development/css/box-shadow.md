# Box e Text Shadow

## Box Shadow
Box shadow é uma propriedade que nos permite criar sombras nas nossas caixas (boxes). Podemos especificar de vários valores de como deverá ser nossa sombra.

Como toda propriedade CSS, a quantidade de parametros dirá o que e qual propriedade aquele valor se refere. Vamos ver então todos e a cada nova propriedade, uma breve explicação.

### Passando valores

#### 3 valores
Dada a propriedade `box-shadow` com os seguintes valores: `60px -16px black`, temos:

- 1o valor (60px): Descolamento no eixo x (eixo horizontal)
- 2o valor (-16px): Descolamento no eixo y (eixo vertical)
- 3o valor (black): Cor da sombra

Como resultado, temos:
[primeiro exemplo](https://jsfiddle.net/raulfdm/rxhmxksk/)

#### 4 valores
Dada a propriedade `box-shadow` com os seguintes valores: `10px 5px 5px black`, temos:

- 1o valor (10px): Descolamento no eixo x (eixo horizontal)
- 2o valor (5px): Descolamento no eixo y (eixo vertical)
- 3o valor (5px): Raio do borrão (blur). Neste, quanto mais próximo de 0, mais sólido será a cor
- 4o valor (black): cor da sombra

Como resultado, temos:
[segundo exemplo](https://jsfiddle.net/raulfdm/rxhmxksk/1/)

#### 5 valores
Dada a propriedade `box-shadow` com os seguintes valores: `2px 2px 2px 1px rgba(0, 0, 0, 0.2)`, temos:

- 1o valor (2px): Descolamento no eixo x (eixo horizontal)
- 2o valor (2px): Descolamento no eixo y (eixo vertical)
- 3o valor (2px): Raio do borrão (blur). Neste, quanto mais próximo de 0, mais sólido será a cor
- 4o valor (1px): Será o raio de "espalhamento" da sombra, ou seja, o quanto que aquela sombra vai se espalhar. Em outras palavras, vai ser o tamanho dela.
- 5o valor (black): cor da sombra

Como resultado, temos:
[terceiro exemplo](https://jsfiddle.net/raulfdm/rxhmxksk/2/)

### Sombra interna
Além da sombra externa, ou seja, aquela sombra que vai pra fora do elemento, podemos também colocar uma sombra interna, ou seja, de fora pra dentro do nosso elemento. Para isso, precisamos passar o valor `inset` e seguida os valores da sombra, como já vimos acima.

Abaixo, um exemplo com uma sombra simples para dentro (`box-shadow: inset 10px 5px 5px black;`):
[quarto exemplo](https://jsfiddle.net/raulfdm/rxhmxksk/3/)

### Multiplas Sombras
Por último, mas não menos importante, podemos aplicar multiplas sombras para nossos elementos. Para isso, basta apenas passarmos cada borda separadas por virgula.

Vamos ver o exemplo abaixo com o valor as sombras `60px -16px black` e `-16px 60px  gold`:

[quinto exemplo](https://jsfiddle.net/raulfdm/rxhmxksk/4/)

## Text Shadow

<PENDING>
