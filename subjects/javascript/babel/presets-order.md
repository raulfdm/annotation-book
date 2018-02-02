# Ordem dos presets

A ordem de declaração dos `presets` no babel conta muito, assim como no `webpack`, a ordem dos loaders vai definir se o fluxo funcionará ou não.

## Problema
Estava tendo probelam de transpilação do código usando Babel + React:

```json
{
  "presets": ["react-app","stage-0",[
    "env",
    {
      "targets": {
        "browsers": ["last 2 versions", "not ie <= 10"]
      }
    }
  ]],
  "plugins": [
    ["transform-runtime", {
      "helpers": false,
      "polyfill": false,
      "regenerator": true,
      "moduleName": "babel-runtime"
    }],
    [
      "module-resolver",
      {
        "alias": {
          "Declarations": "./src/scenes/Declarations/",
          "DeclarationLines": "./src/scenes/DeclarationLines/",
          "Candidates": "./src/scenes/Candidates/",
          "components": "./src/components/",
          "globals": "./src/globals",
          "services": "./src/services/"
        }
      }
    ]
  ]
}
```

E nessa configuração, tive o seguinte erro:

```bash
Failed to compile.

./src/components/Loader/Loader.js
Syntax error: Missing class properties transform.

   8 |
   9 | export default class Loader extends PureComponent {
> 10 |   state = {
     |   ^
  11 |     showLoader: false,
  12 |   };
  13 |
```

Procurando no repositório do `BabelJS`, descobri que a ordem correta de importação dos presets é: `stage-0>env>react`

resultando em:

```diff
{
-  "presets": ["react-app","stage-0",[
+  "presets": ["stage-0",[
    "env",
    {
      "targets": {
        "browsers": ["last 2 versions", "not ie <= 10"]
      }
    }
-  ]],  
+  ],"react-app"],
  "plugins": [
    ["transform-runtime", {
      "helpers": false,
      "polyfill": false,
      "regenerator": true,
      "moduleName": "babel-runtime"
    }],
    [
      "module-resolver",
      {
        "alias": {
          "Declarations": "./src/scenes/Declarations/",
          "DeclarationLines": "./src/scenes/DeclarationLines/",
          "Candidates": "./src/scenes/Candidates/",
          "components": "./src/components/",
          "globals": "./src/globals",
          "services": "./src/services/"
        }
      }
    ]
  ]
}

```

Resolvendo assim o problema.
