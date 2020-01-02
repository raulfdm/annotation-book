# Short-hand initialization

TS nos prove uma syntax onde podemos evitar esse escopo do constructor:

```ts
class Person {
  private kind = "human";

  constructor(public name: string, private age: number) {}
}

const person = new Person("Raul", 88);

person.name; //> Raul
person.age; //> Property 'age' is private and only accessible within class 'Person'.
```

Passando um dos accessors `public`, `protected` ou `private`, você pede gentilmente para o TS receber a variável `name` e logo em seguida atribuir o valor recebido a um novo field (de mesmo nome), com o valor recebido
