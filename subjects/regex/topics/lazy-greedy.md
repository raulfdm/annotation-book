# Expressões gananciosas ou pregriçosas

Os **quantifiers** por padrão são `greedy` (gananciosos), ou seja, quando você define um deles, ele não para no primeiro caso que encontra, ou seja, ele vai até não encontrar mais evidências. 

Um exemplo é o `+`, ele vai selecionar TUDO até a ultima ocorrência, segue um exemplo prático:

```
Frase: Nico Steppat|14/05/1977|Rua Buarque de Macedo|50|22222-222|Rio de Janeiro
Expressão: .+\| // Selecione qualquer caracter (.) que pode se repetir uma ou mais vezes (+) até encontrar o pipe(|)

Resultado (1 match): Nico Steppat|14/05/1977|Rua Buarque de Macedo|50|22222-222|
```

Porém, vamos supor que queremos só a primeira parte, ou seja, só o nome, até se deparar com o PRIMEIRO pipe. Assim, podemos pedir para ela através do `?`, tornando-a **"preguiçosa"**, ficando:

```
Frase: Nico Steppat|14/05/1977|Rua Buarque de Macedo|50|22222-222|Rio de Janeiro
Expressão: .+?\| // Selecione qualquer caracter (.) que pode se repetir uma ou mais vezes (+) até encontrar o pipe(|)

Resultado (5 matches): Nico Steppat| | 14/05/1977| | Rua Buarque de Macedo| | 50| | 22222-222|
```

# Backreferences

Podemos ter um caso onde temos a seguinte condição:
```
Target: <h1>Meu Titulo</h1>
Regex: <h1>[\w\s]+</h1>
```

Porém, suponhamos que eu quero pegar elementos de titulo, mas eles possam ser `h1` ou `h2`.
Assim, a nossa regex não funciona mais. Corrigindo-a, fica:

```
Target: <h1>Meu Titulo</h1>
Regex: <(h1|h2)>[\w\s]+</(h1|h2)>
```

Só que existe um problema. Vamos supor que o elemento esteja inválido e comece com `<h1>` e termine com `</h2>`. A nossa expressão pegaria também, pois, foi definido:
> Pegue quando for h1 ou h2 (no ínicio e fim)

Podemos definir a seguinte condição: 
> Quando pegar h1 na primeira ocorrência, a segunda ocorrência TAMBÉM DEVERÁ SER h1.

Para tal, podemos fazer uma refência (backreference) ao primeiro grupo, ou seja, dizer para a nossa expressão aplicar o MESMO resultado de um determinado grupo:
```
Target: <h1>Meu Titulo</h1>
Regex: <(h1|h2)>[\w\s]+</\1>
```

Com isso, referenciamos que o resultado do primeiro grupo (`(h1|h2)`)), deverá ser aplicado também em `</\1>`, ou seja, se for for `h1`, coloca `h1` na referência, se for `h2`, coloque `h2`.
