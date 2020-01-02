# Inheritance

**Herança** não é um conceito de TS, mas é bom saber um pouco sobre. Sabe quando tu cria um class component em React e tu precisa `extends` de React.Component? Isso é herança.

Com ela, podemos herdar métodos e variáveis de outra classe:

```ts
class Animal {
  constructor(private kind: string) {}

  getKind() {
    return this.kind;
  }

  walk() {
    console.log("do some walking movement");
  }
}

class Human extends Animal {
  constructor() {
    super("Human");
  }

  walk() {
    console.log("Do some biped walking");
  }
}

class Horse extends Animal {
  constructor() {
    super("Horse");
  }
}

const animal = new Animal("Insect");
animal.getKind(); //> Insect
animal.walk(); //> do some walking movement

const human = new Human();
human.getKind(); //> Human
human.walk(); //> Do some biped walking

const horse = new Horse();
horse.getKind(); //> Horse
horse.walk(); //> do some walking movement
```

Perceba que quando estendemos de outra classe, se o construtor dela exigir parâmetros, precisamos passa-los através da palavra `super`, que é a PRIMEIRA coisa que precisa se declarada.

Para além disso, tanto `Human`, quanto `Horse`, herdam de `Animal` o método `getKind` e `walk`. No caso de `Horse`, nós não sobrescrevemos o método `walk`, logo, ele usa deu seu pai (`Animal`).

!> Uma coisa importante a se notar é que `kind` em `Animal`, está marcado como acesso `private`, OU SEJA, não está acessível para nenhuma outra classe. Caso desejarmos acessar `this.kind` dentro de `Human` ou `Horse`, precisamos trocar de `private` para `protected`.
