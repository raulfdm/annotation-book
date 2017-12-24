# Boas práticas

## 1. Versionamento

Após criar a pasta do projeto, já rodar o comando `git init` e fazer a configuração do servidor onde será versionado o projeto.

---

## 2. NPM INIT
Rodar o comando `npm init` ou `yarn init` e preencher todas as configurações do projeto, bem como: 
- Autor name/email
- License
- Repositório do Git
- Versão
- arquivo de entreda (entry point)
- Nome do Projeto

---

## 3. Criar o GitIgnore
Criar o gitignore é importante para não versionamos arquivos desnecessários. Atualmente, existe um pacote chamado gitignore que fica responsável de criar a lista de arquivos e pastas ignoradas para gente de forma automatizada.

Como usaremos apenas uma vez em cada projeto, essa dependencia pode ser instalada globalmente: 
```
npm i -g gitignore
```

Então, podemos checar quais os tipos de projetos que já possui o gitignore com o comando `gitignore --types`

Como o projeto geralmente se baseia na estrutura do Node (node modules,lockes etc) podemos escolher o tipo `gitignore node` que o arquivo será gerado corretamente.

Mais informações em: [gitignore project](https://www.npmjs.com/package/gitignore)

---

## 4. Criar o README.md
Criar um README (letras maisculas para arquivos só de texto) baseado em algum estilo do projeto [Awesome Readme](https://github.com/matiassingers/awesome-readme).

---

## 5. Criar um Arquivo de Contributing
Criar o arquivo de Contributing baseado no template criado aqui.

---

## 6. Definir ESLINT Style
Padrões de código são extremamente importantes. Para garanti-los, devemos usar um linter, que fará a checagem do nosso código.

Adicionar como dependencia de desenvolvimento o ESLINT (caso seja javascript puro) utilizando o comando:
```
npm install eslint --save-dev

# ou

yarn add -D eslint
```

Em seguida, rodar o comando: `node_modules/.bin/eslint --init`

Escolha um estilo popular (AIRBNB) e em seguida selecione para gerar o estilo em JSON e o arquivo `.eslintrc.json` será criado.

Vale lembrar que podemos alterar as regras quando for conveniente.

  ### 6.1 Extensão
  Para facilitar no Lint, podemos utilizar uma extensão para nosso editor de texto. No caso do VSCODE, podemos baixar a ESLint do Dirk Baeumer.

  ### 6.2 Rodar LINT
  Para executar o lint, basta passarmos o comando: `node_modules/.bin/eslint <pasta>/*.js`, por exemplo:
  ```
  node_modules/.bin/eslint src/*.js
  ```

---

## 7. Definir um .editorconfig
O editorConfig é uma série de configurações de estilo que a maioria dos editores de texto usam para fazer a identação e definir algumas propriedades importantes (tipo charset).

Pode usar o arquivo criado aqui como padrão.

---

## 8. NPM Scripts
Configurar inicialmente o script do lint na parte dos scripts do package.json:
```json
{
  "scripts": {
    "lint": "node_modules/.bin/eslint src/*.js"
  }
} 
```

Para rodar o comando, podemos:
```
npm run lint

# ou

yarn lint
```

---

## 9. Adicionar Hooks
Hooks no git são como ganchos. Ele possibilita que seja executada determinada tarefa antes de alguma ação via GIT. Ou seja, imagina que antes de cada `push` para o branch, eu queira executar alguma tarefa e, caso ela não seja feita com sucesso, me barre de fazer esse `push`. É para isso que serve hooks.

Uma das maneiras mais fáceis, é utilizando o pacote [HUSKY](https://github.com/typicode/husky). Para instala-lo, basta digitar `npm i --save-dev husky`.

Agora, definimos quais os ganchos que queremos utilizar. Por exemplo, gostariamos de executar um link antes de fazer o push. Logo, segundo a documentação do Husky, adicionamos no Script do Package.json a script `prepush` com o script que gostariamos de executar:

```json
{
  "scripts": {
    "lint" : "lint": "node_modules/.bin/eslint src/*.js",
    "prepush" : "npm run lint"
  }
}
```

Dessa forma, quando fizermos um `git push origin master`, o comando `lint` será executado. Caso falhe, o push não será feito e teremos que revisar quais os erros.

Evita muito código errado para versionamento.
