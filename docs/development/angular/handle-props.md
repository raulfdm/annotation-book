# Props

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
<img *ngIf="photo" [url]="photo.url" [alt]="photo.description" />
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
<img *ngFor="let photo of photos" [url]="photo.url" [alt]="photo.description" />
```

Perceba que neste exemplo, temos um array de photos e na marcação, diremos para o angular criar um elemento do tipo `img` para cada objeto dentro do array de `photos`.

## Observable

O Angular em seus módulos optou por trabalhar com observable ao invés de trabalhar com promises. Isso significa que é um pouco diferente a maneira de lidar.

Comparando o fetch (promise) com o httpClient (observable), quando chamamos o `fetch('link')`, a requisição é disparada imediatamente. Já no httpClient, ela só é executada quando alguém se inscreve nela, ou seja, `httpClient.get('link').subscribe()`

### Resposta

Enquanto na promise temos o `then` para pegar as respostas de sucesso e o `catch` para os erros, nos observables, a função de subscribe espera receber dois parametros. O primeiro é uma função de sucesso e o segundo é uma função para tratar o erro.
