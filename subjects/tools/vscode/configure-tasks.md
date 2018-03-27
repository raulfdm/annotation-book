# Configurar Tasks

> https://code.visualstudio.com/docs/editor/tasks

Muitas vezes precisamos configurar tarefas (tasks) que precisam serem executadas toda vez, da mesma forma, e toda vez lembrar de qual pasta acessar, qual comando rodar, pode ser uma tarefa que apesar de não exigir muito esforço, ao longo de meses pode consumir bastante tempo perdido.

Para solucionar isso, o VSCode traz pra gente uma ferramenta chamada `Tasks`, no qual você pode definir comandos específicos que serão executados quando você rodar alguma task em específico.

## Exemplo

Abaixo, podemos ver um exemplo simples de uma tarefa configurada:

```json
{
  // See https://go.microsoft.com/fwlink/?LinkId=733558
  // for the documentation about the tasks.json format
  "version": "2.0.0",
  "tasks": [
    {
      "label": "webpack",
      "type": "shell",
      "isBackground": true,
      "command":
        "bundle exec /Users/raulmelo/projects/youngcapital/candidate-proposal-frontend-bff/bin/webpack-dev-server",
      "presentation": {
        "echo": true,
        "reveal": "always",
        "panel": "new"
      },
      "problemMatcher": []
    }
  ]
}
```

No caso, essa tarefa é do tipo `shell`, ou seja, vai rodar no terminal integrado e vai seguir o comando `bundle exec /Users/raulmelo/projects/youngcapital/candidate-proposal-frontend-bff/bin/webpack-dev-server`.

Na parte de `presentations` são algumas informações sobre como será exibida (output) essa tarefa.

* `echo` significa se ela vai ou não ser exibida no terminal (de forma escrita);
* `reveal` define se o terminal será "trazido para frente", ou seja, se o seu terminal integrado estiver fechado, ele vai abrir a sessão e mostrar a tarefa em questão;
* `panel`: define configurações do terminal onde diz como queremos trata-lo, ou seja, se usaremos um terminal que já esteja rodando algo, se vai ser um terminal dedicado para a tarefa, ou se vai abrir uma nova aba para tal.


## Tarefas linkadas
Além de definir tarefas, podemos definir uma tarefa para rodar todas as outras. O que precisamos, é configurar uma "Tarefa global" que seja dependente de outras, por exemplo:

```json
{
  // See https://go.microsoft.com/fwlink/?LinkId=733558
  // for the documentation about the tasks.json format
  "version": "2.0.0",
  "tasks": [
    {
      "label": "bootstrap",
      "dependsOn": ["webpack", "rails"]
    },
    {
      "label": "webpack",
      "type": "shell",
      "isBackground": true,
      "command":
        "bundle exec /Users/raulmelo/projects/youngcapital/candidate-proposal-frontend-bff/bin/webpack-dev-server",
      "presentation": {
        "echo": true,
        "reveal": "always",
        "panel": "new"
      },
      "problemMatcher": []
    },
    {
      "label": "rails",
      "type": "shell",
      "isBackground": true,
      "command": "cd /Users/raulmelo/projects/youngcapital/candidate-proposal-frontend-bff && bundle exec rails s",
      "problemMatcher": []
    },
  ]
}
```

No exemplo acima, temos duas 2 tarefas que de fato executam alguma coisa (`rails` e `webpack`) e uma tarefa (`boostrap`) que tem a única responsabilidade de chamá-las.

Esse mecanismo evita que precisamos rodar manualmente multiplas tarefas.

## Configurações extras

Para entender melhor como configurar, entre na [documentação oficial do VSCode](https://code.visualstudio.com/docs/editor/tasks).
