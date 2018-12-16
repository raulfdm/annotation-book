## Snippet Task

```json
{
  // See https://go.microsoft.com/fwlink/?LinkId=733558
  // for the documentation about the tasks.json format
  "version": "2.0.0",
  "tasks": [
    {
      "label": "bootstrap",
      "dependsOn": ["webpack", "rails", "blokkendoos"]
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
    {
      "label": "blokkendoos",
      "type": "shell",
      "isBackground": true,
      "command": "cd /Users/raulmelo/projects/youngcapital/blokkendoos && bundle exec rails s",
      "problemMatcher": []
    }
  ]
}
```
