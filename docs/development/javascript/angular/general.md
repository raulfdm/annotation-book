# Angular

## Basics

### Instalação

A melhor forma de criar um projeto em Angular é usando o [AngularCLI](https://cli.angular.io/).

```bash
npm install -g @angular/cli
```

### Criando um projeto

Para criar um projeto, basta digitar:

```bash
ng new <project-name>
```

### Subindo o Servidor

Para startar o projeto:

```bash
ng serve --open
```

A flag `--open`, abre o browser pra você.

## Concepts

### Pastas

Tudo que formos criar dentro do projeto, a grande maioria é dentro da pasta `app`.

### Components

Tudo no Angular é um component. Assim, quando falamos em `<app-todo></app-todo>` por exemplo, isso significa que existe um component com esse nome dentro de `app`.

O Angular segue uma estrutura onde o nome do componente tem o nome de: `<nome>.component.ts`.

#### .component.ts

A estrutura básica de um component em angular é:

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent {
  title = 'app';
}
```

Onde:

- @Component: é um decorator, ou seja, é uma forma de injetar na classe meta informações sobre o component. Para saber mais [clique aqui](https://www.typescriptlang.org/docs/handbook/decorators.html). Obs: **OBRIGATÓRIO**
- selector: é reference à tag que criaremos. Nesse caso, a usaremos como `<app-root></app-root>`
- templateUrl: é a URl para o arquivo HTML que representa a marcação do component
- styleUrls: são os arquivos de estilos references ao component

### One way Data-binding

Para fazer data-binding no Angular, no template, você usa uma AE (Angular Expression) definida por `{{ <minha-variável> }}`:

```html
<h1>
  Welcome to {{ title }}!
</h1>
```

e na classe teremos:

```ts
export class AppComponent {
  title = 'app';
}
```

Ou seja, a mensagem do `<h1>` será `Welcome to app`.

Entretanto, essa abordagem é boa somente para os casos onde queremos interpolar um conteúdo dentro da tag. Quando queremos fazer data-binding de atributos, usamos da seguinte maneira:

```html
<a [href]="link">{{ linkName }}</a>
```

e na classe teremos:

```ts
export class AppComponent {
  link = "http://google.com";,
  linkName = "Google"
}
```

Perceba que ao invés da AE, usamos `[]` no atributo e no seu valor, passamos o nome da variável definido na classe. Dessa forma, o Angular sabe que aquilo é um data-bind e que ele precisa pregar o valor de uma variável na classe e aplicar no template.

## Convenções

Quero criar o componente "menu":

- nome da pasta: `menu`
- nome do component: `menu.component.ts`
- nome da classe dentro do arquivo component: `MenuComponent`
- nome do template: `menu.component.html`
- nome do css: `menu.component.css`
- nome do selector: `<prefixo-do-projeto>-menu`. Esse é um caso especial, onde precisamos definir um prefixo para evitar conflitos de nome. A boa prática é definir um prefixo com o nome do projeto, por exemplo:
  Projeto my-fintness-pall. Componente menu: `<mfp-menu></mfp-menu>`

## Dependencias Globais

Em certos momentos queremos adicionar dependencias que serão usadas globalmente no projeto como por exemplo um framework CSS, uma biblioteca Javascript e etc.

Para isso, precisamos definir o caminho desse arquivo dentro do arquivo `angular.json`, que é o "centro nervoso" do projeto, ou seja, é o lugar que está definido TODAS as informações necessárias para o build acontecer.

Dentro da chave `build`, temos `options` e dentro de `options` temos algumas chaves como `polyfills`, `assets`, `styles`, `scripts`. É aqui que adicionamos os nossos arquivos globais.

```json
{
  "build": {
    "builder": "@angular-devkit/build-angular:browser",
    "options": {
      "outputPath": "dist/test-angular",
      "index": "src/index.html",
      "main": "src/main.ts",
      "polyfills": "src/polyfills.ts",
      "tsConfig": "src/tsconfig.app.json",
      "assets": ["src/favicon.ico", "src/assets"],
      "styles": ["src/styles.css"],
      "scripts": []
    },
    "configurations": {
      "production": {
        "fileReplacements": [
          {
            "replace": "src/environments/environment.ts",
            "with": "src/environments/environment.prod.ts"
          }
        ],
        "optimization": true,
        "outputHashing": "all",
        "sourceMap": false,
        "extractCss": true,
        "namedChunks": false,
        "aot": true,
        "extractLicenses": true,
        "vendorChunk": false,
        "buildOptimizer": true
      }
    }
  }
}
```

No caso de dependencias dentro do `node_modules`, precisamos especificar o caminho absoluto para chegar lá, ou seja, `./node_modules/fo/bar/fo.js`

## Modulos

Para o angular, módulo é um conjunto de components que fazem parte do mesmo grupo. Vamos imaginar uma tabela, onde possuimos o componente de Header, Body, Footer, Linhas e Colunas, totalizando 5 components. Como eles estão relacionados, podemos criar um Módulo chamado Table, que importa todos esses componentes e quando alguém quiser usar a tabela, ao invés de importar cada componente separado, importa o módulo Tabela.

### Feature Module

O que vimos acima é conhecido como FeatureModule, ou seja, modulo que contém os componentes relacionados a uma feature específica.

Ainda usando o exemplo anterior, a estrutura de pastas ficaria mais ou menos assim:

```plain
app
 |__table/
      |__table.module.ts
      |__header/
      |__body/
      |__footer/
```

onde o `table.module.ts` exportaria todos os componentes relativos:

```ts
import { NgModule } from '@angular/core';
import Header from './header/header.component.ts';
import Body from './body/body.component.ts';
import Footer from './footer/footer.component.ts';

@NgModule({
  declarations: [Header, Body, Footer],
  exports: [Header, Body, Footer]
})
export class TableModule {}
```

Perceba que temos `declarations` e `exports`. A diferença é que tudo que ta em `declarations` seria similar a atributos privados de uma classe, ou seja, só ela mesma possui acesso. Já o `exports` seriam os atributos publicos, ou seja, os méotodos que tudo mundo que o importar terá acesso.

> Não é obrigatório que tudo que seja declarado seja exportado. Você pode ter 30 declarações e exportar apenas 3 métodos.

## Passando Props pros components (Inbound Props)

Diferentemente do React, quando queremos passar props para um componente Angular, precisamos em sua classe, explicitar que a propriedade X será aceita, por exemplo:

```ts
import { Input } from '@angular/core';

export class TitleComponent {
  @Input() text = '';
}
```

```html
<title text="Raul"></title>
```

Assim, será renderizado a marcação do componente `Title` com o texto passado como props "Raul".

## Diretivas

### Structural Directive

> [Para saber mais](https://angular.io/guide/structural-directives)

Diretivas estruturais são diretivas que alteram o comportamento dos elementos do DOM, baseado em sua função. Por exemplo, `ngIf`. Quando usamos ela, estamos falando que aquele component deverá ser renderizado mediante a uma condicional, ou seja, se o valor X for `false`, não renderiza, se for `true`, renderiza.

```html
<div *ngIf="hero" class="name">{{hero.name}}</div>
```

No exemplo acima, se o valor "hero" existir, ou seja, !== false, a `div` será renderizada.

Lembrando que para os casos de passar propriedade, precisamos fazer o data-binding:

```html
<img *ngIf="photo" [url]="photo.url" [alt]="photo.description"/>
```

#### NgFor

Ainda sobre diretivas estruturais, temos o `*ngFor` que tem a função de criar um loop através de um array e criar elementos DOM para cada objeto.

```ts
export class PhotoListComponent {
  photos = [
    {
      id: 1,
      url: 'http://blabla.com/1',
      description: 'A photo'
    },
    {
      id: 2,
      url: 'http://blabla.com/2',
      description: 'A photo 2'
    }
  ];
}
```

```html
<img *ngFor="let photo of photos" [url]="photo.url" [alt]="photo.description"/>
```

Perceba que neste exemplo, temos um array de photos e na marcação, diremos para o angular criar um elemento do tipo `img` para cada objeto dentro do array de `photos`.

---

## Providers

Providers são métodos já configurados que implementam uma lógica/configuração pra você não precisar esquentar a cabeça com isso. Um exemplo é o `HttpClient`.

Se formos criar um `new HttpClient`, precisamos saber uma série de informações e implementações. Para evitar isso, usamos o `HttpClientModule` (provider) que abstrai essa configuração toda.

---

## Requisições HTTP

Para fazer requisições HTTP, usamos o modulo `HttpClient` do próprio Angular. Porém, precisamos fazer algumas configurações:

1.  Importar o `HttpClientModule` no módulo principal da aplicação:

    ```ts
    //.. Código omitido

    import { HttpClientModule } from '@angular/common/http';

    @NgModule({
      declarations: [AppComponent],
      imports: [BrowserModule, HttpClientModule],
      providers: [],
      bootstrap: [AppComponent]
    })
    export class AppModule {}
    ```

1.  No modulo/component que a gente que usar o http agora, precisamos fazer uma injeção de dependencia do `HttpClient`:

    ```ts
    //.. Código omitido

    export class AppComponent {
      constructor(http: HttpClient) {
        //disponível no contexto
      }
    }
    ```

### Observable

O Angular em seus módulos optou por trabalhar com observable ao invés de trabalhar com promises. Isso significa que é um pouco diferente a maneira de lidar.

Comparando o fetch (promise) com o httpClient (observable), quando chamamos o `fetch('link')`, a requisição é disparada imediatamente. Já no httpClient, ela só é executada quando alguém se inscreve nela, ou seja, `httpClient.get('link').subscribe()`

#### Resposta

Enquanto na promise temos o `then` para pegar as respostas de sucesso e o `catch` para os erros, nos observables, a função de subscribe espera receber dois parametros. O primeiro é uma função de sucesso e o segundo é uma função para tratar o erro.

## Services

Para isolarmos nosso código de requisição, podemos criar uma classe chamada `<component>.service.ts` e lá, fazer coisas relacionadas ao Http:

```ts
//userInfo.service.ts

import { HttpClient } from '@angular/common/http';

export class UserInfoService {
  constructor(private http: HttpClient) {}

  public getUserData(username: string) {
    return this.http.get<User>(`http://my-api.com/user/${username}`);
  }
}
```

Aqui vale uma nota especial onde não faz sentido implementarmos o `subscribe` do generator, uma vez que é responsabilidade de quem quer usaer o método.

E onde queremos usar, ao invés de importar o Http, importaremos o service:

```ts
import { Component, Input } from '@angular/core';
import { UserInfoService } from './user/userInfo/userInfo.service';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent {
  user: User;

  constructor(userInfo: UserInfoService) {
    userInfo //Usamos o userInfoService para pegar os dados
      .getUserData('raulfdm')
      .subscribe(
        ({
          avatar_url,
          followers,
          following,
          name,
          public_repos,
          location
        }) => {
          this.user = {
            avatar_url,
            followers,
            following,
            name,
            location,
            public_repos
          };
        }
      );
  }
}
```

Porém, com esse código teremos erro. Precisamos de explicitar para o Angular que o nosso `Service` é do tipo `Injectable`.

### Injectable

Injectable em teste funciona da mesma forma que o `@NgModule` ou `@Component`, ou seja, precisamos decorar a classe e passarmos como meta informação se esse serviço terá uma única instância ou multiplas. Em casos como esse do Http, não faz muitos sentido criarmos uma instância para cada vez que formos usar esse serviço.

Assim, alteramos nosso código para:

```ts
//userInfo.service.ts

import { HttpClient } from '@angular/common/http';

export class UserInfoService {
  constructor(private http: HttpClient) {}

  public getUserData(username: string) {
    return this.http.get<User>(`http://my-api.com/user/${username}`);
  }
}
```

## Typing

Para criarmos tipos, criamos e exportamos uma interface em um arquivo dentro da pasta do component:

```ts
// user.ts
export interface User {
  name: string;
}
```

Assim, para tipar parâmetro, retorno, etc., basta importar essa interface e usa-la.

```ts
import { User } from './user.ts';

class MyUsers {
  user: User;
}
```

## Lifecyle

> [https://angular.io/guide/lifecycle-hooks](https://angular.io/guide/lifecycle-hooks)

![Angular Lifecycle](https://i.stack.imgur.com/yzaYJ.png)
Assim como no React, o Angular também possui um Lifecycle para implementarmos no momento certo os métodos.

## Forçando implementação

Por padrão, o typescript/Angular não te obriga a implementar nenhum lifecycle method, porém, é uma boa prática implementar a interface para nos forçar a usar:

```ts
import { Component, OnInit } from '@angular/core';

//implementando a interface OnInit
@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent implements OnInit {
  constructor() {}

  //Agora somos forçados a fazer essa implementação, se não queb ra
  ngOnInit() {
    throw new Error('onInit not implemented');
  }
}
```

### ngOnInit

Executa algum código assim que o Angular inicializar os primeiros data-bound, propriedades e definir as diretivas.

> Diquinha: fazemos requisição http aqui
