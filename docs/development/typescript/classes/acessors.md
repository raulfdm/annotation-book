# Accessors

## Private

Em TS, temos o conceito de `public` (pode ser acessado fora da classe), `protected` (pode ser acessado dentro da classe e por outras classes que estendem dela) e `private` (somente acessado dentro da classe no qual é definido) fields. Por padrão, todo field criado é publico. Caso queremos deixar ele "escondido" do mundo exterior, podemos defini-lo como private:

```ts
class Person {
  private kind = "human";

  constructor(name: string) {
    this.name = name;
  }
}

const person = new Person("Raul");

person.kind; // <- Error
```

## Protected

## Public

## readonly
