
# Ordem de precedência

Os estilos em CSS respeitam a seguite ordem:

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
