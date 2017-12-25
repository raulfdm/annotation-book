# Unknow Word Error + Storybook

Dada a configuração:

```js
//webpack.config
module.exports = {
  module: {
    rules: [
      {
        test: /\.css$/,
        use: [
          {
            loader: "style-loader"
          },
          {
            loader: "css-loader",
            options: {
              import: false,
              importLoaders: 1,
              root: "."
            }
          },
          {
            loader: "postcss-loader"
          }
        ]
      }
    ]
  }
};

```

Ao rodar o Storybooks, recebemos o seguinte erro:

```bash
ERROR in ./node_modules/css-loader?{"importLoaders":1}!./node_modules/postcss-loader/lib?{"ident":"postcss"}!./node_modules/style-loader!./node_modules/css-loader?{"import":false,"importLoaders":1,"root":"."}!./node_modules/postcss-loader/lib!./src/atoms/Button/Button.css
Module build failed: Syntax Error

(5:1) Unknown word

  3 | // load the styles
  4 | var content = require("!!../../../node_modules/css-loader/index.js?{\"import\":false,\"importLoaders\":1,\"root\":\".\"}!../../../node_modules/postcss-loader/lib/index.js!./Button.css");
> 5 | if(typeof content === 'string') content = [[module.id, content, '']];
    | ^
  6 | // Prepare cssTransformation
  7 | var transform;

 @ ./src/atoms/Button/Button.css 4:14-296 18:2-22:4 19:20-302
 @ ./src/atoms/Button/index.js
 @ ./src/atoms/Button/Button.story.js
 @ ./src \.story\.js$
 @ ./.storybook/config.js
 @ multi ./node_modules/@storybook/react/dist/server/config/polyfills.js ./node_modules/@storybook/react/dist/server/config/globals.js (webpack)-hot-middleware/client.js?reload=true ./.storybook/config.js
 ```

 Para corrigir, basta adicionar um `includes` com um `path` inexistente:

```diff
//webpack.config
module.exports = {
  module: {
    rules: [
      {
        test: /\.css$/,
+       include: [path.resolve(__dirname, "not_exist_path")], //Fix Unknow word Error
        use: [
          {
            loader: "style-loader"
          },
          {
            loader: "css-loader",
            options: {
              import: false,
              importLoaders: 1,
              root: "."
            }
          },
          {
            loader: "postcss-loader"
          }
        ]
      }
    ]
  }
};
```
