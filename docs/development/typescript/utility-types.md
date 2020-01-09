# Utility Type

> https://www.typescriptlang.org/docs/handbook/utility-types.html

Tipos utilitários são ferramentas que nos ajudam a definir melhor os tipos que precisamos e com menos código. Todos eles são baseados em `Generics`, ou seja, um entendimento prévio de como tipos genericos funcionam é essencial para a compreensão de como utiliza-los.

## Partial<T>

Vamos olhar o seguinte exemplo:

```ts
type Person = {
  name: string;
  age: number;
  id: string;
  createDate: Date;
  isUnder18: boolean;
};

function createPerson(name: string, age: number): Person {
  const person: Person = {}; // Type '{}' is missing the following properties from type 'Person': name, age, id, createDate, isUnder18(2739)

  person.name = name;
  person.age = age;
  person.id = Math.random().toString();

  if (person.age > 18) {
    person.isUnder18 = false;
  } else {
    person.isUnder18 = true;
  }

  person.createDate = new Date();

  return person;
}

createPerson("Raul", 88);
```

Temos uma função que dado um nome e idade, retornará um objeto do tipo `Person` com uma estrutura bem mais robusta.

Dentro dela, precisamos fazer alguma validação, como por exemplo para `isUnder18` e baseado na condição atribuir um valor ou outro.

> Eu sei que daria pra fazer com ternary expression e bem mais clean do que isso, é só um exemplo! -.-

Porém como pode ser observado, já temos um erro de todas as propriedades faltando.

Uma das formas de resolver isso é utilizando o `Partial`, que diz que teremos um objeto com todas aquelas propriedades, mas com seus respectivos valores OU undefined:

```ts
type Person = {
  name: string;
  age: number;
  id: string;
  createDate: Date;
  isUnder18: boolean;
};

function createPerson(name: string, age: number): Person {
  const person: Partial<Person> = {};

  person.name = name;
  person.age = age;
  person.id = Math.random().toString();

  if (person.age > 18) {
    person.isUnder18 = false;
  } else {
    person.isUnder18 = true;
  }

  person.createDate = new Date();

  return person as Person;
}

createPerson("Raul", 88);
```

## Readonly<T>

<!-- TODO -->

## Record<K,T>

<!-- TODO -->

## Pick<T,K>

O utilitário Pick serve para casos onde temos um objeto, classe, interface ou tipo e queremos pegar somente ALGUMAS propriedades do mesmo.

Vamos imaginar que temos uma interface `Person` que define vários atributos:

```ts
type Person = {
  name: string;
  age: number;
  id: string;
  createDate: Date;
  isUnder18: boolean;
};
```

Porém, por algum motivo precisamos criar um objeto que seja do tipo `Person`, mas com menos fields. Se tentarmos:

```ts
const simpleData: Person = {
  // Type '{ name: string; age: number; }' is missing the following properties from type 'Person': id, createDate, isUnder18(2739)
  name: "Raul",
  age: 88
};
```

teremos um erro que faz muito sentido, pois estamos dizendo que `simpleData` é do tipo `Person` mas não satisfazemos a assinatura dos parâmetros.

Para contornar isso, podemos fazer:

```ts
type Person = {
  name: string;
  age: number;
  id: string;
  createDate: Date;
  isUnder18: boolean;
};

const simpleData: Pick<Person, "age" | "name"> = {
  name: "Raul",
  age: 88
};
```

Logo, se inspecionarmos o tipo de `simpleData`, ele será: `const simpleData: Pick<Person, "age" | "name">`.

Isso significa que quando tentamos usar `simpleData`, teremos acesso APENAS a `age` e `name`.

## Omit<T,K>

Omit é o oposto do Pick. É quando queremos pegar quase todas propriedades, exceto algumas bem específicas.

Ainda no exemplo de `Pick`, vamos imaginar que agora eu tenho um `simpleData` que vai ter quase tudo que `Person` pede, exceto `isUnder18`:

```ts
type Person = {
  name: string;
  age: number;
  id: string;
  createDate: Date;
  isUnder18: boolean;
};

const simpleData: Omit<Person, "isUnder18"> = {
  name: "Raul",
  age: 88,
  id: "1234",
  createDate: new Date()
};
```

## Exclude<T,U>

<!-- TODO -->

## Extract<T,U>

<!-- TODO -->

## NonNullable<T>

<!-- TODO -->

## Parameters<T>

<!-- TODO -->

## ConstructorParameters<T>

<!-- TODO -->

## ReturnType<T>

<!-- TODO -->

## InstanceType<T>

<!-- TODO -->

## Required<T>

<!-- TODO -->

## ThisParameterType

<!-- TODO -->

## OmitThisParameter

<!-- TODO -->

## ThisType<T>

<!-- TODO -->
