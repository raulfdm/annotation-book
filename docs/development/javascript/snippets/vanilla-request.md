# Vanilla Request Ajax

1. Criar uma instância de `XMLHttpRequest:
  ```javascript
  const xhr = new XMLHttpRequest()
  ```
1. Definir um objeto que contém as informações sobre para a requisição
  ```javascript
  const httpInformations = {
    method: 'GET',
    url: 'https://api.github.com/users/raulfdm',
  }
  ```

1. Adicionar uma função de callback no evento `loader` da requisição
  ```javascript
  xhr.addEventListener('load', () =>{
    const status = xhr.status
    const bodyResponse = JSON.parse(xhr.responseText)
  })
  ```

1. Abre a chamada, passando as informações `method` e a `url`
  ```javascript
  xhr.open(httpInformations.method,httpInformations.url)
  ```

1. Dispara a chamada efetivamente
  ```javascript
  xhr.send()
  ```

## Rodando
<iframe width="100%" height="300" src="//jsfiddle.net/raulfdm/pa64d88p/embedded/js,html,css,result/dark/" allowpaymentrequest allowfullscreen="allowfullscreen" frameborder="0"></iframe>
