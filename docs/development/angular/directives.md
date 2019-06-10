# Directives

Directives are instructions in the DOM. In other words, they're instructions we have to do something with the elements we attach to do something based in a condition or something like that.

It's possible to create our own directive of course but it's also some very useful built-in one and they're dived in two types: `Structural` and `Attributes`.

## Structural Directive

Basically they're responsible to affect somehow the DOM tree based on their function.

They are marked by `*` and then the directive name (e.g. `*ngIf`). Bellow you can check some of them.

### ngIf

Render or not something based a condition. Lets see the follow example:

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-server',
  templateUrl: './server.component.html'
})
export class ServerComponent {
  showsParagraph = false;
}
```

```html
<p *ngIf="showsParagraph">My Awesome Paragraph</p>
```

So at the first moment this paragraph won't be render by angular, because `showsParagraph` is `false`. If we change this value to `true`, then it'll automatically be rendered.

### \*ngFor

This directive is used to loop through some array and then render elements with them. Let's see the follow example:

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-server',
  templateUrl: './server.component.html'
})
export class ServerComponent {
  people = ['Raul', 'José'];
}
```

```html
<p *ngFor="let person of people">{{ person }}</p>
```

It'll be rendered 2 paragraphs, one with `Raul` text inside and other with `José` text.

!> It's really necessary define a temporary variable with `let` to Angular be able to set as the current value during the loop.

#### getting index

Sometimes is useful do something with the index. To know that, you can extend `ngFor` direct and do:

```html
<p *ngFor="let person of people; let index = index">
  {{ person }} - {{ index }}
</p>
```

In that case will be render:

```
Raul - 0
José - 1
```

!> Array length starts at 0 position.

## Property Directive

Those are directives we use to change element properties. To use them we have to wrap within `[]`.

### ngStyle

Apply certain style based in a condition. Let's see the example bellow:

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-server',
  templateUrl: './server.component.html'
})
export class ServerComponent {
  user = 'Raul';
  isActive = false;
}
```

```html
<p [ngStyle]="{ backgroundColor: isActive ? 'green' : 'red' }">{{ user }}</p>
```

As you can see, inside the directive we can pass an simple JS object with the styles we want to apply conditionally.

In that case, we're gonna apply `green` if `isActive === true` or `red` if `isActive === false`.

### ngClass

Similar of `ngStyle`, we can add/remove CSS class conditionally:

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-server',
  templateUrl: './server.component.html',
  styles: [
    `
      .is-active {
        background-color: green;
      }
    `
  ]
})
export class ServerComponent {
  isActive = true;
  user = 'Raul';
}
```

```html
<p [ngClass]="{ 'is-active': isActive }">{{ user }}</p>
```

In that case, if `isActive` is true, the class `is-active` will be applied to the element.
