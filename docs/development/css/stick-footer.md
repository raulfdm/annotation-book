# Sticky Footer
>Técnica para deixar o footer da página colado

Hoje é possível fazer essa técnica utilizando o flexbox. Primeiro, precisamos definir que todos os elementos estejam em um wrapper, ou seja, um container que engloba tudo isso. No caso, será o body:

```html
<body>
    <header> </header>
    <main></main>
    <footer></footer>
</body>
```

É importante entender que o html e o body precisam estar com altura de 100% da página:

```css
html, body {
    height: 100%;
}
```

Agora, definimos que o body será flex e mudamos sua orientação para colunas:

```css
body {
    display: flex;
    flex-direction: column;
}
```

Em seguida, definimos que o main ocupará todo o espaço disponível, empurrando o footer para baixo:

```css
main {
    flex: 1;
}
```

Com isso, o footer sempre estará no Rodapé! =D
