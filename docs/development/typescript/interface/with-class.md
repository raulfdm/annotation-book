# with Class

No exemplo básico vimos a implementação como objeto. Porém, também podemos fazer com classes:

```ts
interface IPerson {
  name: string;
  greetings: () => void;
}

class Person implements Person {}
```

!> O sufixo `I` antes do nome da inteface também é uma convenção para ambos os casos onde queremos deixar CLARO que se trata de uma interface ou quando queremos dar o mesmo nome (`Person` no caso) tanto para a classe quanto para a interface.

No caso acima, teremos o seguinte erro:

```
Class 'Person' incorrectly implements interface 'IPerson'.
  Type 'Person' is missing the following properties from type 'IPerson': name, greetings(2420)
```

Isso porque ao implementar (`implements`) uma interface, devemos seguir exatamente o que ela nos pede para ter.

Uma analogia bem comum que é usada para explicar interfaces é a de um contrato.

Pense como se a interface `IPerson` falasse para a classe `Person`:

```
IPerson diz:

- Ao assinar o meu contrato, você concorda em:
  1. ter um field `name` do tipo string;
  2. ter um método chamado `greetings` que não vai receber nenhum parâmetro e não vai retornar nada.
- Você concorda?

Person diz:
- Aceito
```

Agora, `Person` é obrigado a cumprir:

```ts
interface IPerson {
  name: string;
  greetings: () => void;
}

class Person implements IPerson {
  constructor(public name: string, private age: number) {}

  greetings() {
    console.log("Hello =)");
  }
}
```

Perceba que ao usarmos o short-hand initialization, precisamos deixar CLARO que `name` tem acesso `public`, pois nossa interface define desta maneira (por de baixo dos panos).

Isso porque a interface define SOMENTE o que deve ser publico. Tanto isto é verdade que também implementamos `age` como atributo privado e não temos nenhum tipo de erro.

> "Interfaces describe the public side of the class, rather than both the public and private side. This prohibits you from using them to check that a class also has particular types for the private side of the class instance."
>
> https://www.typescriptlang.org/docs/handbook/interfaces.html

O único modificador que uma interface aceita é `readonly`:

```ts
interface IPerson {
  readonly name: string;
  greetings: () => void;
}

class Person implements IPerson {
  constructor(public name: string, private age: number) {}

  greetings() {
    console.log("Hello =)");
  }
}

Person.name = "raul"; // Cannot assign to 'name' because it is a read-only property.(2540)
```

## Multiple implements

Além disso, podemos também implementar multiplas interfaces:

```ts
interface IPerson {
  readonly name: string;
  greetings: () => void;
}

interface Human {
  motherName: string;
}

class Person implements IPerson, Human {
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

Como visto no exemplo anterior, basta passarmos quantas interfaces quisermos seguidas de virgula.
