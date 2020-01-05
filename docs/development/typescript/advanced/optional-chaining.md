# Optional Chaining

Imagine que recebemos a seguinte api response:

```json
{
  "data": {
    "user": {
      "_id": "1234",
      "name": "Raul",
      "favorites": {
        "articles": ["how to study"],
        "songs": ["pesadão.mp3"]
      }
    }
  }
}
```

E o nosso backend nos diz que:

1. Pode ser que `data` seja `null`, o que significa que não encontrou o usuário;
1. Caso o usuário exista, `id` e `name` sempre estarão disponíveis;
1. `favorites` poderá ou não existir;

Nessa perspectiva, queremos criar nosso próprio modelo de dados extraindo dados da API response:

```js
function createUser(apiResponse) {
  if (!apiResponse.data) {
    return;
  }

  const { user: userFromData } = apiResponse.data;

  const user = {
    id: userFromData._id,
    name: userFromData.name,
    favoritesArticles: [],
    favoriteSongs: []
  };

  if (userFromData.favorites) {
    const { articles, songs } = userFromData.favorites;

    if (articles) {
      user.favoritesArticles = articles;
    }

    if (songs) {
      user.favoriteSongs = songs;
    }
  }

  return user;
}

const user = createUser(apiResponse);

console.log(user);
/*
{
  id: '1234',
  name: 'Raul',
  favoritesArticles: [ 'how to study' ],
  favoriteSongs: [ 'pesadão.mp3' ]
}
*/
```

Perceba quantas validações precisamos fazer pra lidar com o caso de não existir alguns dados. Com optional chaining, isso tudo fica muito mais fácil de ser validado:

```ts
function createUser(apiResponse) {
  if (!apiResponse.data) {
    return;
  }

  const { user: userFromData } = apiResponse.data;

  const user = {
    id: userFromData._id,
    name: userFromData.name,
    favoritesArticles: userFromData?.favorites?.articles || [],
    favoriteSongs: userFromData?.favorites?.songs || []
  };

  return user;
}
```

O operator `?`, indica ao typescript que existe a possibilidade daquele valor ser null ou undefined.

Logo, deixamos essa validação para a propria ferramenta e dizemos que:

> Para favoriteArticles, se `favorites` existir e for um objeto e ele tiver a propriedade `articles`, use ela. Caso contrário, use um array vazio como valor default.
> (o mesmo para songs)

Se você estiver usando `lodash`, resolveria fazendo:

```ts
function createUser(apiResponse) {
  if (!apiResponse.data) {
    return;
  }

  const { user: userFromData } = apiResponse.data;

  const user = {
    id: userFromData._id,
    name: userFromData.name,
    favoritesArticles: _.get(userFromData, "favorites.articles"), [],
    favoriteSongs: _.get(userFromData, "favorites.songs") || []
  };

  return user;
}
```

Ou no caso de `ramda`:

```ts
function createUser(apiResponse) {
  if (!apiResponse.data) {
    return;
  }

  const { user: userFromData } = apiResponse.data;

  const user = {
    id: userFromData._id,
    name: userFromData.name,
    favoritesArticles: R.pathOr([], ["favorites", "articles"], userFromData),
    favoriteSongs: R.pathOr([], ["favorites", "songs"], userFromData)
  };

  return user;
}
```
