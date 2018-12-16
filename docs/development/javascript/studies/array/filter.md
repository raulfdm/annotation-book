# Filter
O filter é uma "higher order function". Mas afinal, o que isso significa?
Significa que ele é uma __função__ que recebe outra __função__ (callback) para realizar sua operação.

Muito usado na programação funcional, basicamente ele vai nos permitir escrever menos código, menos lógica e fazer a mesma coisa. EXAMPLESSSS:

```javascript
const exercicios = [
    {"nome": "Supino Reto", "grupo-muscular": "peitoral"},
    {"nome": "Supino Inclinado", "grupo-muscular": "peitoral"},
    {"nome": "Legpress 45", "grupo-muscular": "quadriceps"},
    {"nome": "Rosca Direta", "grupo-muscular": "Biceps"},
];


let exerciciosDePeito = [];

for(let index = 0; index <exercicios.length; index++){
    if(exercicios[index]["grupo-muscular"] === "peitoral" ){
        exerciciosDePeito.push(exercicios[index]);
    }
}

console.log(exerciciosDePeito);

//Resultado: [ { nome: 'Supino Reto', 'grupo-muscular': 'peitoral' }, { nome: 'Supino Inclinado', 'grupo-muscular': 'peitoral' } ]
```

O código acima funciona perfeitamente, entretanto, é fácil de perceber que nos preocupamos com um número grande de coisas:

1. Aplicar a iteração no array;
1. Aplicar a condicional;
1. Inserir os elementos filtrados no novo array.
  
Usando Filter, podemos fazer isso de forma muito mais simplificada, nos preocupando basicamente com a regra:

```javascript
const exercicios = [
    {"nome": "Supino Reto", "grupo-muscular": "peitoral"},
    {"nome": "Supino Inclinado", "grupo-muscular": "peitoral"},
    {"nome": "Legpress 45", "grupo-muscular": "quadriceps"},
    {"nome": "Rosca Direta", "grupo-muscular": "Biceps"},
];

//Filter: Higher Order Function
let exerciciosDePeito = exercicios.filter(function(exercicio){
    return exercicio['grupo-muscular'] === 'peitoral';
})

console.log(exerciciosDePeito);
//Resultado: [ { nome: 'Supino Reto', 'grupo-muscular': 'peitoral' }, { nome: 'Supino Inclinado', 'grupo-muscular': 'peitoral' } ]
```

O Filter, basicamente itera sobre um array e retorna um novo array para gente e esse novo array, já é atribuido a uma variável (`exerciciosDePeito`). Logo, precisamos apenas nos preocupar com a lógica condional.

Ainda é possível escrever o mesmo código, isolando a função e abstraindo ainda mais:

```javascript
const exercicios = [
    {"nome": "Supino Reto", "grupo-muscular": "peitoral"},
    {"nome": "Supino Inclinado", "grupo-muscular": "peitoral"},
    {"nome": "Legpress 45", "grupo-muscular": "quadriceps"},
    {"nome": "Rosca Direta", "grupo-muscular": "Biceps"},
];

function eHExercicioDePeito(exercicio){
    return exercicio['grupo-muscular'] === 'peitoral';
}

let exerciciosDePeito = exercicios.filter(eHExercicioDePeito);
    
console.log(exerciciosDePeito);
//Resultado: [ { nome: 'Supino Reto', 'grupo-muscular': 'peitoral' },{ nome: 'Supino Inclinado', 'grupo-muscular': 'peitoral' } ]
```

Como a função `Filter` recebe uma função de callback como argumento,é perfeitamente aceitável passarmos uma função como argumento para ela, mesmo que essa função esteja escrita em outro lugar.

## Recapitulando

A função `filter` itera sobre um array utilizando uma outra função que receberá como argumento cada item que está sendo iterado no array e executar alguma lógica, retornando um novo array.
