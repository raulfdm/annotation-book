# Conceitos

## Pastas

Ao setar um projeto com a AngularCLI, a esturura da projeto é a seguinte:

```
.
├── README.md
├── angular.json
├── e2e
│   ├── protractor.conf.js
│   ├── src
│   │   ├── app.e2e-spec.ts
│   │   └── app.po.ts
│   └── tsconfig.e2e.json
├── package-lock.json
├── package.json
├── src
│   ├── app
│   │   ├── app-routing.module.ts
│   │   ├── app.component.html
│   │   ├── app.component.scss
│   │   ├── app.component.spec.ts
│   │   ├── app.component.ts
│   │   └── app.module.ts
│   ├── assets
│   ├── browserslist
│   ├── environments
│   │   ├── environment.prod.ts
│   │   └── environment.ts
│   ├── favicon.ico
│   ├── index.html
│   ├── karma.conf.js
│   ├── main.ts
│   ├── polyfills.ts
│   ├── styles.scss
│   ├── test.ts
│   ├── tsconfig.app.json
│   ├── tsconfig.spec.json
│   └── tslint.json
├── tsconfig.json
└── tslint.json
```

Assim, é fácil ver que tudo que fomos criar será (quase sempre) da pasta `src/app`.

## Components

Tudo no Angular é um component. Assim, quando falamos em `<app-todo></app-todo>` por exemplo, isso significa que existe um component com esse nome dentro de `app`.

O Angular segue uma estrutura onde o nome do componente tem o nome de: `<nome>.component.ts`.

### .component.ts

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

## One way Data-binding

Para fazer data-binding no Angular, no template, você usa uma AE (Angular Expression) definida por `{{ <minha-variável> }}`:

```html
<h1>Welcome to {{ title }}!</h1>
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

## Módulos

Para o angular, módulo é um conjunto de components que fazem parte do mesmo grupo. Vamos imaginar uma tabela, onde possuimos o componente de Header, Body, Footer, Linhas e Colunas, totalizando 5 components. Como eles estão relacionados, podemos criar um Módulo chamado Table, que importa todos esses componentes e quando alguém quiser usar a tabela, ao invés de importar cada componente separado, importa o módulo Tabela.

## Feature Module

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

## Lifecyle

> [https://angular.io/guide/lifecycle-hooks](https://angular.io/guide/lifecycle-hooks)

![Angular Lifecycle](https://i.stack.imgur.com/yzaYJ.png)
Assim como no React, o Angular também possui um Lifecycle para implementarmos no momento certo os métodos.

## Tipagem

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

## Providers

Providers são métodos já configurados que implementam uma lógica/configuração pra você não precisar esquentar a cabeça com isso. Um exemplo é o `HttpClient`.

Se formos criar um `new HttpClient`, precisamos saber uma série de informações e implementações. Para evitar isso, usamos o `HttpClientModule` (provider) que abstrai essa configuração toda.

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
