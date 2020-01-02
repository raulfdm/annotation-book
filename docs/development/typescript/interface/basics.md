# Interface

Interfaces são formas de definir assinaturas para nossas classes e objetos. Com ela, é possível quais as propriedades e métodos que determinado objeto deve ou não possuir.

Para criação de uma interface, fazemos:

```ts
interface Person {
  name: string;
}
```

Por convenção, o nome da interface segue PascalCase (primeira letra de cada palavra em maiúsculo), em seguida, separado por ponto-e-virgula, cada atributo do objeto.

```ts
interface Person {
  name: string;
}

function printName(person: Person) {
  console.log(`Hello ${person.name}`);
}

const person: Person = {
  name: "raul"
};

printName(person); // Hello raul
```

No exemplo acima, criamos nossa interface `Person` (linhas 16-18) que define que o objeto **deverá** conter APENAS o atributo `name` do tipo `string`.

Em seguida, criamos uma função (linhas 20-22) que espera receber um parâmetro do tipo `Person`.

Logo após, criamos um objeto `person` (linhas 24-26) que defini explicitamente que ele deverá ter exatamente o que `Person` requer.

Por fim, chamamos a função `printName` passando como parametro o nosso objeto `person`.
