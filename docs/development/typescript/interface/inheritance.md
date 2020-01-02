# Interface Inheritance

Apesar de termos a possibilidade de implementarmos várias interfaces em classes, as vezes é mais conveniente que herdamos de outras intefaces.

No exemplo seguinte, temos:

```ts
interface IHuman {
  motherName: string;
}

interface IPerson {
  readonly name: string;
  greetings: () => void;
}

class Person implements IPerson, IHuman {
  constructor(
    public name: string,
    public motherName: string,
    private age: number
  ) {}

  greetings() {
    console.log("Hello =)");
  }
}
```

Se todo `IPerson` precisa também ser `IHuman`, logo, podemos dizer que:

```ts
interface IHuman {
  motherName: string;
}

interface IPerson extends IHuman {
  readonly name: string;
  greetings: () => void;
}

class Person implements IPerson {
  constructor(
    public name: string,
    public motherName: string,
    private age: number
  ) {}

  greetings() {
    console.log("Hello =)");
  }
}
```

Ou seja, jogamos a responsabilidade de definir tudo que `Person` precisa ter para `IPerson`.

## Multiple extends

Diferente de herança em classe, nas interfaces podemos herdar de outras multiplas interfaces:

```js

interface IAnimal {
  breath: () => void
}

interface IHuman {
  motherName: string;
}

interface IPerson extends IHuman, IAnimal {
  readonly name: string;
  greetings: () => void;
}
```
