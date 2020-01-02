# Singletons + Private Constructor

Singleton é um design pattern bem comum no mundo do desenvolvimento. A ideia por trás é usarmos A MESMA instância de um objeto através da aplicação inteira. Em JS, seria algo como:

```js
class Person{
  constructor(private name: string) { }

  getName() {
    return this.name
  }
}

export const person = new Person("Raul");
```

E lá em outro arquivo:

```js
import { person } from "./person";

console.log(person.getName()); // Raul
```

Nesse caso, sempre que importarmos em algum outro lugar `person`, será SEMPRE o mesmo objeto.

Em TS, temos uma outra maneira de implementar isso, que é através do `private constructor`:

```ts
class Person {
  private constructor(private name: string) {}

  getName() {
    return this.name;
  }
}
```

Porém, se tentarmos criar uma nova usando `new`, teremos um erro:

```js
const person = new Person("raul"); // Constructor of class 'Person' is private and only accessible within the class declaration.(2673)
```

Ou seja, a partir deste momento, o constructor só pode ser usado por métodos de dentro da própria classe. Parece um pouco intuitivo, mas faz sentido pois ele tem accessor `private`.

Então, como construiremos nosso objeto?

O primeiro passo é criar uma propriedade que guardará a instância da classe e consequentemente, poderá ter como tipo, somente a classe em si:

```diff
class Person {
+ private static _instance: Person;
+ private name?: string;
+
+ private constructor() {}
- private constructor(private name: string) {}

  getName() {
    return this.name;
  }
}
```

Perceba que adicionamos uma propriedade `private` e `static` que guardará a instancia criada, porém, pelo fato de ser privada, somente será acessível por métodos internos da classe.

Também precisamos abrir mão de usar parametros no construtor e criarmos alguns outros métodos (ou setters) para adicionar informação na nossa instância.

Em seguida, precisamos adicionar um método para criarmos ou retornarmos a instancia criada:

```diff
class Person {
  private static _instance: Person;
  private name?: string;

  private constructor() {}

  getName() {
    return this.name;
  }

+ static get instance() {
+   if (!Person._instance) {
+     Person._instance = new Person();
+   }
+
+   return Person._instance
+ }
}
```

Criamos um getter estático que:

- se não tiver ainda uma instacia criada, cria uma;
- se já tiver, retorna a mesma

Para voltarmos com a nossa funcionalidade anterior, vamos adicionar uma função setar o nome:

```diff
class Person {
  private static _instance: Person;
  private name?: string;

  private constructor() {}

  getName() {
    return this.name;
  }

+ setName(name: string) {
+   this.name = name;
+ }

  static get instance() {
    if (!Person._instance) {
      Person._instance = new Person();
    }

    return Person._instance;
  }
}
```

> Obs.: poderiamos implementar um `get name` e um `set name`, mas precisariamos trocar o nome da variável `name`, caso contrário teremos um erro de identificador duplicado (`Duplicate identifier 'name'.(2300)`)

Utilizando nosso singleton, teriamos:

```ts
class Person {
  private static _instance: Person;
  private name?: string;

  private constructor() {}

  getName() {
    return this.name;
  }

  setName(name: string) {
    this.name = name;
  }

  static get instance() {
    if (!Person._instance) {
      Person._instance = new Person();
    }

    return Person._instance;
  }
}

const person = Person.instance; // Cria a instancia, pois ainda não temos
const anotherPerson = Person.instance; // Retorna a instancia criada anteriormente

console.log(person.getName()); // undefined
console.log(anotherPerson.getName()); //undefined

person.setName("Raul");
console.log(anotherPerson.getName()); // Raul
```

Perceba que usamos `person` para setar o nome e fazemos um `getName` em `anotherPerson`, evidenciando o uso da MESMA instance em ambos objetos criados.
