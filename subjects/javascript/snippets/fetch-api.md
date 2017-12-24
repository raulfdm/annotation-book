# Usando Fetch API

## Caso de requisição GET/JSON
```javascript
let headers = new Headers({'Content-Type': 'application/json'});

let httpConfig = {
    method: 'GET',
    headers: headers,
    mode: 'cors'
}

let url = `https:...`;

fetch(url, httpConfig)
    .then(response => response.json())
    .then(obj => console.log(obj));
```
