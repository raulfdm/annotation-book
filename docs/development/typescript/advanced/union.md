# Union

É bem próximo de [intersection](docs/development/typescript/advanced/intersection.md), porém, tem a função de **OU**:

```ts
type AccessCode = string | number;
```

No exemplo acima, `AccessCode` pode ser uma `string` OU um `number`.

Pode também ser usado para muitos e mais complexos tipos:

```ts
type Car = {
  wheels: number;
  openTrunk: () => void;
};

type Bike = {
  wheels: number;
};

type Vehicle = Car | Bike;
```

No exemplo acima, `Vehicle` pode ser tanto um carro (`Car`) quanto uma moto (`Bike`). Assim, se criarmos uma função genérica e não funcional para chamar as funções dos veículos:

```ts
type Car = {
  wheels: number;
  openTrunk: () => void;
};

type Bike = {
  wheels: number;
};

type Vehicle = Car | Bike;

function printFunctions(vehicle: Vehicle) {
  console.log("Number of Wheels", vehicle.wheels);
  vehicle.openTrunk(); // Property 'openTrunk' does not exist on type 'Vehicle'. Property 'openTrunk' does not exist on type 'Bike' (2339)
}
```

E é claro, pois veículo pode ser um OU o outro. Mas mesmo se tentarmos usar o bom e velho `if`, TS ainda não deixará de dar o mesmo erro:

```ts
function printFunctions(vehicle: Vehicle) {
  console.log("Number of Wheels", vehicle.wheels);
  if (vehicle.openTrunk) {
    // Property 'openTrunk' does not exist on type 'Vehicle'. Property 'openTrunk' does not exist on type 'Bike' (2339)
    vehicle.openTrunk();
  }
}
```

Nessa perspectiva, `Type Guards` nada mais é do que uma maneira de ter CERTEZA de que aquela properidade estará disponível. Usando `in` de JS, podemos contornar esse problema:

```ts
function printFunctions(vehicle: Vehicle) {
  console.log("Number of Wheels", vehicle.wheels);
  if ("openTrunk" in vehicle) {
    vehicle.openTrunk();
  }
}
```

> https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/in

## Class

Seguindo o mesmo exemplo anterior, se tanto `Car` e `Bike` fossem uma classe, poderíamos checar através do `instanceof` (também JS):

```ts
class Car {
  wheels = 4;

  openTrunk() {
    console.log("Opening trunk...");
  }
}

class Bike {
  wheels = 2;

  openTrunk() {
    console.log("Opening trunk...");
  }
}

/* Vehicle pode ser tanto ambos Car e Bike classe. */
type Vehicle = Car | Bike;

function printFunctions(vehicle: Vehicle) {
  console.log("Number of Wheels", vehicle.wheels);
  if (vehicle instanceof Car) {
    vehicle.openTrunk();
  }
}

const vehicle: Vehicle = new Car();
printFunctions(vehicle);
// Number of Wheels 4
// Opening trunk...

const vehicle2: Vehicle = new Bike();
printFunctions(vehicle2);
// Number of wheels 2
```

## Discriminated Union

O nome `Union` é auto explicativo, ou seja, a união de dois ou mais tipos. Isso significa que dado os tipos:

```ts
type Admin = {
  name: string;
  privileges: string[];
};

type Regular = {
  name: string;
};
```

e uma união entre eles:

```ts
type User = Admin | Regular;
```

Significa que user `User` SEMPRE terá um atributo chamado `name`, pois é o ponto em comum entre `Admin` e `Regular`.

Podemos utilizar esta feature para criar um ponto em comum e ajudar no [`type guard`](docs/development/typescript/advanced/type-guard):

```ts
type Admin = {
  type: "admin";
  name: string;
  privileges: string[];
};

type Regular = {
  type: "regular";
  name: string;
};

type User = Regular | Admin;
```

O ponto em comum entre os dois será o field `type`. Assim, em qualquer função onde precisamos chamar uma função específica de um tipo, podemos fazer um `if` ou um `switch`:

```ts
function executeDangerousCommand(user: User) {
  switch (user.type) {
    case "admin": {
      console.log("Doing something dangerous");
      break;
    }
    case "regular": {
      console.log("You do not have privileges");
      break;
    }
  }
}

const user: User = {
  type: "admin",
  name: "Raul",
  privileges: ["Root"]
};
executeDangerousCommand(user); // Doing something dangerous

const user2: User = {
  type: "regular",
  name: "John Do"
};
executeDangerousCommand(user2); // You do not have privileges
```
