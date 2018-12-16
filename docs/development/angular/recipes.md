# Receitas

## Dependencias Globais

Em certos momentos queremos adicionar dependencias que serão usadas globalmente no projeto como por exemplo um framework CSS, uma biblioteca Javascript e etc.

Para isso, precisamos definir o caminho desse arquivo dentro do arquivo `angular.json`, que é o "centro nervoso" do projeto, ou seja, é o lugar que está definido TODAS as informações necessárias para o build acontecer.

Dentro da chave `build`, temos `options` e dentro de `options` temos algumas chaves como `polyfills`, `assets`, `styles`, `scripts`. É aqui que adicionamos os nossos arquivos globais.

```json
{
  "build": {
    "builder": "@angular-devkit/build-angular:browser",
    "options": {
      "outputPath": "dist/test-angular",
      "index": "src/index.html",
      "main": "src/main.ts",
      "polyfills": "src/polyfills.ts",
      "tsConfig": "src/tsconfig.app.json",
      "assets": ["src/favicon.ico", "src/assets"],
      "styles": ["src/styles.css"],
      "scripts": []
    },
    "configurations": {
      "production": {
        "fileReplacements": [
          {
            "replace": "src/environments/environment.ts",
            "with": "src/environments/environment.prod.ts"
          }
        ],
        "optimization": true,
        "outputHashing": "all",
        "sourceMap": false,
        "extractCss": true,
        "namedChunks": false,
        "aot": true,
        "extractLicenses": true,
        "vendorChunk": false,
        "buildOptimizer": true
      }
    }
  }
}
```

No caso de dependencias dentro do `node_modules`, precisamos especificar o caminho absoluto para chegar lá, ou seja, `./node_modules/fo/bar/fo.js`

## Forçando implementação

Por padrão, o typescript/Angular não te obriga a implementar nenhum lifecycle method, porém, é uma boa prática implementar a interface para nos forçar a usar:

```ts
import { Component, OnInit } from '@angular/core';

//implementando a interface OnInit
@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent implements OnInit {
  constructor() {}

  //Agora somos forçados a fazer essa implementação, se não queb ra
  ngOnInit() {
    throw new Error('onInit not implemented');
  }
}
```
