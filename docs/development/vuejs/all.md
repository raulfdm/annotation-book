# VueJS

## CLI
para nos ajudar a criar um projeto utilizando vue, podemos utilizar a VUE CLI. Com ela, a geraçao de arquivos e configurações é toda facilitada.

Para insta-la, basta rodar o comando abaixo:

```bash
$ npm i -g vue-clie 
```

## Iniciando um projeto
Com a CLI instalada, rodamos o comando:

```bash
$ vue init webpack-simple <nome-do-projeto>
```

---

# Global Vue Object

O Global vue Object (`import Vue from 'vue'`) é o objeto que dará os super poderes do vue para a nós e possibilitará seu uso. É necessário importar o objeto principal do módulo e instacia-lo para que isso seja possível.

## Vue Instance
A Vue Instance é criada utilizando o Global Vue Object. Ele é o MERGE dos meus componentes com o componente pai (vue)

## Estrutura e configurações

A estrutura basica do vue instance é a seguinte:
```js
new Vue({
  el: '#app',
  render: h => h(App
})
```

- **el**: Element
  - Essa tag se refere ao elemento do meu index.html que receberá todo o conteúdo renderizado. Recebe um seletor de CSS
- **render**: Funçao de renderiação
  - É a função chamada no momento da renderização do componente que receberá um parâmetro "h" (padrão do vue) e receberá o componente que será renderizado no lugar de #App

--- 

# Entendendo o arqivo .vue

Um módulo Vue (arquivo .vue) possui **3 tags** principais: 
- **template:** (`<template>`)
- **script:** (`<script>`)
- **style:** (`<style>`)

## Template
Nessa parte é onde fica o nosso código HTML e também as **interpolações**.

Uma regra muito importante do template é: **Todo o conteúdo deverá estar envolto de apenas 1 tag**.

Isso na prática significa que caso você tenha dois componentes, é necessário envolve-los em um outro componente, que no caso seria como um envelopador (wrapper).

```html
<template>
  <h1>Hello {{ name }}</h1>
</template>
```

No exemplo acima, como temos apenas **um** elemento no template, ele é o seu próprio **wrapper**.


## Script
Nessa tag, definiremos a lógica do nosso componente. Por default, ele retorna um objeto com o nome do componente e uma função de data.

```html
<script>
export default {
  name: 'app',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  }
}
</script>
```
A Função **data** tem a única função de passar os dados para a parte do template conseguir fazer a interpolação dos dados.

## Style
Na tag style, como o próprio nome já diz, é para gente estilizar estilos do nosso componente.
```vue
<style>
  h1 {
    text-align: center;
  }
</style>
```

Ainda nela, é possível definir se queremos que o escopo do nosso CSS seja global ou seja local através da *tag* `scoped`:
```vue
<style scoped>
  h1 {
    text-align: center;
  }
</style>
```

Isso significa que no build, será criado um **hash-id** para a classe do elemento e esse estilo não "vazará" para os outros elementos. No caso do exemplo acima, temos um estilo no `h1`. Caso ele seja aplicado desta maneira, de acordo com a ordem de declaração, todos os elementos `h1` receberiam este estilo. Porém, como está em `scoped`, será gerado um hash-id como mostra o exemplo abaixo:

```html
<div data-v-a0905cb8="" id="app"></div>
```



## Lang
Vale frisar um ponto curioso é que você pode determinar qual a linguagem que você quer utilizar para fazer o **template** ou o **style**. No primeiro, podemos utilizar o [Pug](pugjs.org) e no segundo, podemos usar [Sass](sass-lang.com), [Stylus](http://stylus-lang.com/), [PostCSS](http://postcss.org/) e outros.

Para tal, basta configurar o loader dos mesmos nas tasks do webpack e definir a tag `lang`, passando qual a linguagem a ser utilizada:

```vue
<template lang="pug">
</template>

<script>
</script>

<style lang="postcss">
</style>

```

--- 

# Começando

## Interpolação e Data-binding
O conceito de interpolação é bastante difundido atualmente nos frameworks. Basicamente ele diz que, em determinado espaço na view entrará um dado vindo do script.

Uma interpolação em vueJS, é feita de duas formas. A primeira consiste em usar duas chaves e colocar o conteúdo no meio:
```vue
<template>
  <h1>{{ titulo }}</h1>
</template>

<script>
  export default {
    data() {
      titulo: 'Minha página'
    }
  }
</script>
```

Quando a interpolação é feita em um atributo, ou propriedade, não é possível realizar a interpolação desta maneira. Assim, somos obrigados a utilizar uma `diretiva` chamada **v-bind**:

```vue
<template>
  <img v-bind:href="imagem.url" v-bind:alt="imagem.titulo">
</template>

<script>
  export default {
    data() {
      imagem: {
      	url: 'http://.....com.br/img/jpg',
	titulo: 'foto de perfil'
      }
    }
  }
</script>
```

Entretanto, um **shorthand** para realizar o mesmo bind, pode ser apenas dois pontos (`:`):

```diff
-<img v-bind:href="imagem.url" v-bind:alt="imagem.titulo">
+<img :href="imagem.url" :alt="imagem.titulo">
```

O data-binding nada mais é do que o ligamento entre a variável do script e a sua referência na view. Da maneira que com que declaramos (dois pontos), dizemos que o data-binding é unidirecional do model(script) para a view(template).


## Diretivas

### v-for
No mundo da programação, temos sempre a necessidade de consumir uma API ou uma lista de dados e iterar sobre ela para gerar algo. No caso, para gerarmos elementos dinamicamente, basta definirmos a *diretiva* `v-for` dentro do elemento que será criado dinamicamente e dizemos quais os dados que serão usados:

```html
<ul>
  <li v-for="foto in fotos">
     <img :src="foto.url" :alt="foto.title">
  </li>
</ul>
	
```

---

# Lifecile Hooks 
O Vue e seus componentes possuem um ciclo de vida, ou seja, a cada final de um estado (criação, renderização, etc.), é disparado um evento que nós podemos interceptar e realizar alguma ação.

Todo o Lifecicle pode ser consultado em [https://vuejs.org/v2/api/#Options-Lifecycle-Hooks](https://vuejs.org/v2/api/#Options-Lifecycle-Hooks)

## created
Essa função é executada sempre que o componente é criado e antes do mesmo ser renderizado na tela. Ideal para inserir dados antes da renderização.

---

# Requisições HTTP

No core do Vue JS não há um módulo que execute requisições HTTP. Dessa maneira, precisamos baixar uma LIB que se integra muito bem com o vue que é a `vue-resource`:
```bash
npm i --save vue-resource
```

## Disponibilizando na aplicação
Para disponibilizar o modulo para nossa aplicação, depois de fazer o download, vamos no `main.js` e fazemos o *import* dele. Em seguida, pegamos o **Global vue object** e dizemos para ele **usar** o módulo:

```javascript
import Vue from 'vue'
import App from './App.vue'

import VueResource from 'vue-resource'

Vue.use(VueResource)
```

## Usando a o vue-resource
Dentro do nosso módulo, depois de inscrito corretamente no objeto global vue, podemos chamar dentro de algum lifecicle hook o comando `this.$http`. Essa função disponibiliza para nós todos os métodos HTTP de forma facilitada, devolvendo o resultado em formato de `promise` ([documentação](https://github.com/pagekit/vue-resource))


---

## Vue Router
Para criar rotas, precisamos sempre determinar um componente que será o wrapper, ou seja, onde o componente de cada rota será enxertado (inserido). Assim, uma prática comum é usar o App (modulo principal da nossa aplicação) como esse wrapper.

### Instalação
Antes de mais nada é preciso saber que o router do vue não faz parte do core dele, logo, se faz necessário a instalação.

```
npm i -g vue-router --save-dev
```

Em seguida, é necessário aplicar no módulo principal Vue, assim como fizemos com o resource:

```javascript
...
import VueRouter from 'vue-router'

Vue.use(VueRouter)
...
```

