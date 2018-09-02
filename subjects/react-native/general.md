# React native

## Tags

### Text

Melhor lugar para colocar um texto (equivalente ao `p`)

### Image

Componente de imagem (`img`)

### Dimensions

Component que prove informações sobre dimensões em geral. Nele, temos o método `get`. No `get`, podemos passar como parâmetro `screen` e assim, teremos todas as informações sobre a tela do usuário:

```jsx
const myWidth = Dimensions.get('screen').width;
const myHeight = Dimensions.get('screen').height;
```
