# Plugins úteis

Quando precisamos de tarefas muito específicas além de transpilar nosso código para ES2015, precisamos recorrer a alguns plugins, e, para nossa sorte, o Babel possui muitos plugins extremamente úteis.

## Transform React Constant Elements

> [https://babeljs.io/docs/plugins/transform-react-constant-elements/](https://babeljs.io/docs/plugins/transform-react-constant-elements/)

Sua finalidade é criar constantes (`const`) para os stateless components, afim de utilizar o `hoisting` natural do javascript e ter um ganho de perfomance em sua execução. Além disso, ele ainda da uma ofuscada ainda maior no código.

```js
// ENTRADA
const Hr = () => {
  return <hr className="hr" />;
};
```

```js
// RESULTADO
const _ref = <hr className="hr" />;

const Hr = () => {
  return _ref;
};
```

Vale lembrar que ele só deve ser utilizado em **produção**.

## Transform Runtime
> [https://babeljs.io/docs/plugins/transform-runtime/](https://babeljs.io/docs/plugins/transform-runtime/)

Esse plugin é tem a finalidade de ajudar a limpar o código duplicado pelo próprio babel quando ele está fazendo a compilação.

## Transform React Remove PropTypes
> [https://github.com/oliviertassinari/babel-plugin-transform-react-remove-prop-types](https://github.com/oliviertassinari/babel-plugin-transform-react-remove-prop-types)

Esse plugin é excelente, pois remove todos os `prop-types` dos components. `Prop-types` são muito úteis no desenvolvimento, porém, no build de produção não fazem muito sentido.

```js
// ENTRADA
const Baz = (props) => (
  <div {...props} />
);

Baz.propTypes = {
  className: PropTypes.string
};
```

```js
// RESULTADO
const Baz = (props) => (
  <div {...props} />
);
```

Dependendo da quantidade de components que você tem, pode-se alcançar uma redução de código significativa!
