# Desafio

Precisamos ajudar os correios a entregar corretamente suas correspondências. Para tal, disponibilizaram-nos um arquivo com diversas linhas, nas quais são necessárias as informações: **Nome**, **Rua**, **Número** e **CEP**.
As outras informações também devem ser separadas para futuros serviços dos correios, porém não precisamos capturá-las neste momento.

```
Nico Steppat|14/05/1977|Rua Buarque de Macedo|50|22222-222|Rio de Janeiro

Romulo Henrique|14/06/1993|Rua do Lins|120|12345-322|Rio de Janeiro

Leonardo Cordeiro|01/01/1995|Rua de Campo Grande|01|00001-234|Rio de Janeiro
```
Tente montar uma regex que realize esse trabalho e ajude os correios!

Resposta:
```
nome:               ([\w\s]+)\|
Data de nascimento: (?:[1-3]?\d\/[01][0-9]\/[12]\d{3})\|
endereço:           ([\w\s]+)\|
numero:             (\d{1,4})\|
cep:                (\d{5}-?\d{3})\|
Cidade:             (?:[\w\s]+)

Resultado: ([\w\s]+)\|(?:[1-3]?\d\/[01][0-9]\/[12]\d{3})\|([\w\s]+)\|(\d{1,4})\|(\d{5}-?\d{3})\|(?:[\w\s]+)

```

