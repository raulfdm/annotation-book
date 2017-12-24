
# Medidas

## Relatividade e HTML
Quando falamos sobre relatividade no tamanho da font do browser, precisamos levar em consideração que serão sempre baseadas no tamanho da font do browser MESMO. Imagine o cenário:

```scss
//font-size browser: 20px
body {
  font-size: 200%; //20px * 200% = 40px
}

div {
  height: 30rem; //20px * 30 = 600px
}
```
Podemos ver que apesar de termos no body uma font que é o dobro de tamanho, foi calculado com base na fonte do elemento `html`. Caso queiramos mudar isso, podemos faze-lo:

```scss
//font-size browser: 20px
html {
  font-size: 200%; //20px * 200 = 40px
}

div {
  height: 30rem; //40px * 30 = 1200px
}
```

## %

### Box Model
Quando usamos porcentagem nas propriedades do box-model (width, height, padding, margin) se refere ao tamanho do elemento pai. Exemplo:

```html
<style>
.a {
  height: 100px;
  width: 100px;
  background-color: purple;
}

.b {
  height: 50%;
  width: 50%;
  padding: 10%;
  margin: 10%;
  background-color: navy;
}
</style>

<div class="a">
  <div class="b"></div>
</div>
```

Nesse caso, teremos que o `height` e o `width` valerão **50px (100px*50%)** e a `margin` e `padding` valerão **10px (100px*50%)**.

Usar porcentagem pode causar alguns efeitos colaterais, uma vez que ela sempre será baseada no tamanho do pai. Logo, ela é realmente útil quando queremos levar em consideração o tamanho do container para desenvolver algum elemento.

## REM
O `rem` é uma medida relativa na **ALTURA** da fonte do navegador. Vamos imaginar que você defina que a fonte do seu navegador será 20px. Caso você declare alguma tamanho dele elemento com `rem`, será feito o calculo `Xrem = 20px * X`. Em outras palavras, temos:

```scss
//font-size (browser): 20px

h1 {
  font-size: 1.8rem; //OR 36px (20*1.8)
}
```

Ela não é recomendada em casos onde queremos definir a largura de qualquer elemento. Isso pode dar uma bugada nos nossos elementos, pois, apesar das fontes terem a mesma altera, o estilo de cada uma define uma largura diferente. Para esses casos utilizamos o **CH**.

## CH
CH é parecido com REM, mas com a diferença que ele é relacionado a **LARGURA**, e não a altura. Essa largura será sempre baseada na largura do caracterer 0!

## EM
O EM é bem similar ao REM, entretanto, caso tenha um tamanho de fonte especial definido no elemento, ele assumirá esse valor, e não mais o tamanho padrão da fonte no navegador. Exemplo

```scss
//Font-size browser: 20px

div {
  font-size: 16px;
  height: 2em; //Isso será equivalente a 2*16 (32px) e não a 2*20
}

```
