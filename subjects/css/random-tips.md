# Dicas aleatórias

- Manipular a posição do elemento no grid: usar o valor **auto** nas propriedades `margin-left` ou `margin-right`.
- A **Ordem de precedência** no CSS segue a estrutura:
```
Inline Style > ID > Class > Element Style
```

  Ou então, data uma div comum `div`, a ordem de prescendencia segue a seguinte ordem:

  ```html
  <div style="background-color: red" class="regular-div" id="regular-div"></div>
  ```

  ```css
  .regular-div {
    background-color: red;
  }
  ```

  ```css
  #regular-div {
    background-color: red;
  }
  ```

  ```css
  div {
    background-color: red;
  }
  ```
