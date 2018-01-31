# Border Radius

A propriedade `border-radius` é uma propriedade que foi implementada no CSS3.

Seu objetivo, é facilitar a criação de diferentes formas nos boxes, ao invés de apenas quadrados ou retangulos.

Assim como várias outras propriedades, ela aceita diferentes quantidades de parâmetros, por exemplo:

## Eixos
Uma coisa interessante e pouco divulgada, é que podemos passar valores para o raio no eixo X e valores para o raio no eixo Y da seguinte maneira: `border-radius: <raio na horizontal (eixo x)> / <raio na vertial (eixo y)`

Quando passamos apenas um valor, sem a barra `/`, os mesmos valores serão aplicados para ambos eixos, exemplo:

```
border-radius: 50%;
```

Será transformado em:

```
border-radius: 50% / 50%;
```

Ou mais precisamente em:

```
border-radius: 50% 50% 50% 50% / 50% 50% 50% 50%
```

No útlimo caso, o valor passado, será aplicado em todas as direções. 

Agora, vamos ver como funciona quando passamos de um a quatro valores:

## Passando valores para ambos eixos
### Passando 1 valor (border-radius: x)
Quando passamos apenas um valor, indicamos que ele seja usado nas quatro pontas do nosso box:

Exemplo `border-radius: 10px`:
[source code](https://jsfiddle.net/raulfdm/8a21e24h/3/)

### Passando 2 valores (border-radius: x y)
Passando 4 valores, temos:
* x: **Superior Direito** e **Inferior Esquerdo**
* y: **Inferior Direito** e **Superior Esquerdo**:

Dois exemplos. O primeiro `border-radius: 10px 0` e o segundo `border-radius: 0 10px`: 
[border radius](https://jsfiddle.net/raulfdm/8a21e24h/8/)

### Passando 3 valores (border-radius: x y z)

No caso de 3 valores, temos:
 * x: **Superior Esquerdo**. 
 * y: **Superior direito** E **Inferior Esquerdo**. 
 * z: **Inferior Direito**

Exemplo `border-radius: 10px 5px 20px`:

[border 3 values](https://jsfiddle.net/raulfdm/8a21e24h/6/)

### Passando 4 valores (border-radius: x y z w)
Neste caso, cada valor será correspondente a um canto da nossa caixa. Sendo:
* x: Superior Esquerdo
* y: Superior Direito
* z: Inferior Direito
* w: Inferior Esquerdo

Exemplo utilizando `border-radius: 15px 50px 30px 5px`:
[Border radius 4 values](https://jsfiddle.net/raulfdm/8a21e24h/7/)

## Passando valores para ambos eixos
### Passando 1 valor (border-radius: x / x)
Quando passamos apenas um valor, indicamos que ele seja usado nas quatro pontas do nosso box:

Exemplo `border-radius: 10px / 30px`:
[source code](https://jsfiddle.net/raulfdm/8a21e24h/9/)

### Passando 2 valores (border-radius: x y / x y)
Passando 4 valores, temos:
* x: **Superior Direito** e **Inferior Esquerdo**
* y: **Inferior Direito** e **Superior Esquerdo**:

Dois exemplos. O primeiro `border-radius: 50% 15% / 60% 30% e o segundo `border-radius: 80% 10% / 22% 90%`: 
[border radius](https://jsfiddle.net/raulfdm/8a21e24h/10/)
