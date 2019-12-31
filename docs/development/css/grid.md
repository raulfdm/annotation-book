# CSS GRID

## Começo

Quando queremos fazer um grid layout, precisamos aplicar `display: grid`:

```css
.container{
  display: grid;
}
```

A partir disso, todos os filhos de `container`, serão tratados como `grid-items`.

## Definindo um template

Quando só definimos grid, por padrão ele não tem nenhum template, porém podemos definir o comportamento tanto das `columns` via `grid-template-columns`, quando das `rows` via `grid-template-rows`.

### grid-template-columns

Como o próprio nome diz, define o template das colunas. Podemos passar qualquer valor mensurável (px, %, rem,etc.) e também fr [(fraction)](#fr-unit).

```css
.container {
  display: grid;
  grid-template-columns: 30px 40px;
}
```

No exemplo acima, dizemos que queremos um grid com 2 colunas, onde a primeira terá exatamente `30px` e a segunda exatamente `40px`.

É importante notar que se houver mais de 2 elementos, neste caso, eles serão jogados para outra `row`, mantendo a regra de ter **APENAS** 2 colunas.

<iframe width="100%" height="300" src="//jsfiddle.net/raulfdm/cpy1gvwo/4/embedded/result,html,css/dark/" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>


### grid-template-rows

Mesmas regras do `column`, porém definidas para as linhas (`rows`).

```css
.container {
  display: grid;
  grid-template-rows: 30px 40px;
}
```

Neste caso, queremos teremos um grid de apenas UMA COLUNA. A primeira row terá `30px`, a segunda terá `40px`.

Como não dissemos para o grid como será o tamanho das outras linhas (caso tenhamos mais que duas), elas terão o tamanho equivalente ao seu conteúdo:

<iframe width="100%" height="300" src="//jsfiddle.net/raulfdm/cpy1gvwo/5/embedded/result,html,css/dark/" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>

## fr unit

Junto com Grid layout, veio a unidade `fr` (fração), que é bem auto explicativa.

Lembra das frações nas aulas de matemática? É isso. 1/2, 1/3, 1/10.

Quando dizemos `1fr`, isso significa que queremos uma fração do todo, ou seja, se pedimos `1fr` de `300px`, teremos 1/1, que seria todos os 300 pixels.

Quando dizemos que queremos `1fr 3fr 2fr` de `300px`, por de baixo dos panos acontece a seguinte matemática:

```text
1fr + 3fr + 2fr = 5fr

300px ----- 5fr
x   ----- 1fr
(regra de 3, lembra?)

1fr = 300px/5fr
se tirarmos as unidades,

1 = 300/5
1 = 60

Voltando as unidades

1fr = 60px
```

Logo, temos:

```text
1fr = 60px
3fr = 3 * 60 = 180px;
2fr = 2 * 60 = 120px
```

Ou seja,

```text
// Em um grid de 300px
1fr 3fr 2fr  = 60px 180px 120px
```

### Casos específicos

Existe um caso mais específico onde o cálculo é feio de outra maneira, que é quando misturamos medidas mais exatas com frações, vejamos o seguinte exemplo:

```text
// Em um grid de 300px
30px 25% 1fr 2fr
```

As `fraction` usarão SEMPRE o restante do grid. Logo, a matemática fica:

1. Tiramos os 30px do total:
    ```text
    300px - 30px = 270px;
    ```
2. Tiramos o percentual do restante da subtração anterior:
    ```text
    25% de 300 = 75px
    270px - 75px = 195px
    ```
3. Com o restante, faremos a conta de em quantas frações precisamos dividir:
    ```text
    195px --- 3fr
    x px  --- 1fr

    1fr = 195/3
    1fr = 65px
    ```

Logo, temos:

```text
30px 25% 1fr 2fr <===> 30px 75px 65px 130px
```

<iframe width="100%" height="300" src="//jsfiddle.net/raulfdm/cpy1gvwo/7/embedded/result,html,css/dark/" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>

Então, nunca se esqueça que:

!>Fractions são SEMPRE baseadas no valor **RESTANTE** disponível.

## minmax

A função `minmax` também foi introduzida com o CSS Grid layouts e tem como objetivo definir um tamanho minimo e/ou máximo para a coluna ou linha.

Ela aceita dois parâmetros:
1. tamanho minimo, que pode ser qualquer valor mensurável;
2. tamanho máximo, que também segue essa regra.

Um plus é que além de aceitar `px`, `rem`, `%`, etc, ambos aceitam o valor `auto`, na qual aumenta/diminui de acordo com o tamanho do conteúdo do `grid-item`.

```css
.container{
  display: grid;
  grid-template-rows: minmax(100px, auto);
}
```

No caso acima, temos um grid que define um tamanho tamanho mínimo é `100px` e pode se expandir para o máximo que o conteúdo permitir APENAS para primeira linha, sendo as outras, definidas pelo tamanho do seu conteúdo:

<iframe width="100%" height="300" src="//jsfiddle.net/raulfdm/cpy1gvwo/10/embedded/result,css,html/dark/" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>


```css
.grid-container {
  display: grid;
  grid-template-rows: minmax(100px, auto);
  grid-template-columns: minmax(auto, 50%) 1fr 3em;
}
```

No caso acima, temos a mesma regra anterior para as linhas, porém agora, na coluna, definimos que a primeira vai ter o valor mínimo relativo ao seu conteúdo mas vai ter NO MÁXIMO 50% do tamanho total, ou seja, em um grid de 300px, pode a primeira coluna pode ter entre 1 e 150px:


<iframe width="100%" height="300" src="//jsfiddle.net/raulfdm/cpy1gvwo/15/embedded/result,css,html/dark/" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>
