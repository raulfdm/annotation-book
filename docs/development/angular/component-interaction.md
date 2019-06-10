# Component Interaction

## Pass props to children

Some times we do want to pass props to a children and then use there do show/do something really. Let's see the follow template:

```html
<div class="test">
  <my-child-component *ngFor="let test of tests"></my-child-component>
</div>
```

Doing that, there's no such way to `my-child-component` now the information from `test`.

You can maybe think about do a bind property like this:

```html
<!-- parent.component.html -->
<div class="test">
  <my-child-component
    *ngFor="let test of tests"
    [test]="test"
  ></my-child-component>
</div>
```

But it'll throw error because `my-child-component` doesn't know `test` property.

The only way to allow it is explicitly make it to recognize this property doing:

```ts
import { Component, Input } from '@angular/core';

@Component({
  selector: 'app-my-child-component',
  templateUrl: './my-child-component.component.html',
  styleUrls: ['./my-child-component.component.scss']
})
export class MyChildComponent {
  // The declaration needed
  @Input() test: { name: string };
}
```

So the steps are:

1. Import `Input` from angular core;
1. Add the decorator on your class property (`@Input()`)

so in that case, we're gonna to access what we receive on externally `test` property.

```html
<!-- my-child.component.html -->
<p>{{test.name}}</p>
```

# Alias

It's also possible to create an alias to external call and then avoid expose the name, like this:

```ts
export class MyChildComponent {
  // The declaration needed
  @Input('myAwesomeProperty') test: { name: string };
}
```

and then do:

```html
<!-- parent.component.html -->
<div class="test">
  <my-child-component
    *ngFor="let test of tests"
    [myAwesomeProperty]="test"
  ></my-child-component>
</div>
```

## The opposite direction

Ok, we can pass props by using `@Input`, what what about the opposite?

For those cases we have `@Output`. But of course, the use is different.

Let's imagine the same example and on click event we want to emit to the parent we've changed.

```ts
/* parent.component.ts */
export class ParentComponent {
  onClickedItem(counter: number) {
    console.log(counter);
  }
}

/* my-child.component.ts */
export class MyChildComponent {
  @Input('myAwesomeProperty') test: { name: string };
  changeData = new EventEmitter({});
  counter = 0;

  onClickMe() {
    this.counter += 1;
    this.changeData(this.counter);
  }
}
```

```html
<!-- parent.component.html -->
<div class="test">
  <my-child-component
    *ngFor="let test of tests"
    [myAwesomeProperty]="test"
    changeData="onClickedItem($event)"
  ></my-child-component>
</div>

<!-- my-child.component.html -->
<p (click)="changeData()">{{test.name}}</p>
```
