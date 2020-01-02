# Class fields

`class fields` está introduzido no JavaScript desde o ES6 (mesmo que de maneira rudimentar):

```js
class Person {
  constructor(name) {
    this.name = name;
    this.kind = "human";
  }
}
```

Em TypeScript, podemos declarar esses fields no escopo da própria classe:

```ts
class Person {
  kind = "human";
  constructor(name) {
    this.name = name;
  }
}
```

Assim, `kind` é uma variável que pertence a Person e possui escopo `public`.
