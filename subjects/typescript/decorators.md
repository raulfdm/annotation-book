# Decorators

Um decorators é um meio de interpectar uma tarefa (metodo) e realizar alguma ação antes ou depois da sua executação. Para usa-lo em Typescript (04/08/2017) é necessário ativar nas opções do compilador (`tsconfig.json`) a opção `experimentalDecorators`:

```json
tsconfig.json
{
  "experimentalDecorators": true
}
```

## Anotação
Depois de ativado, para fazer uso é bem simples, basta passar a anotação `@<nome-do-decorator>` em cima do método/função que deseja interceptar: 

```typescript
@logarResultadoNoConsole()
function soma(a,b){
 return a+b
 }
 ```
 
 ## Criando um decorator
 O primeiro passo é criar um arquivo normal (.ts) e exportar uma função. Lembre-se:
 > O nome da função exportada, será o nome usado para usar o decorator!
 
 Voltando, essa função, deverá retornar outra função:
 
 ```typescript
 export function logarResultadoNoConsole(){
  return function(target: any, key: string, descriptor: PropertyDescriptor){
  
  }
 }
 ```
 
## Observação importante
Só é possível usar decorator para metodos que estejam dentro de classes, ou seja, caso você tenha uma função avulsa
```typescript
function myName(name){
    return name.toUpperCase()
}
```

E tentar decorar ela
```typescript
@consoleLog()
function myName(name){
    return name.toUpperCase()
}
```

Você receberá um erro: `Decorators are not valid here.`
