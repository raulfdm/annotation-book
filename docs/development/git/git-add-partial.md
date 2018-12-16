# git add -p

Às vezes temos a necessidade de commitar apenas uma parte específica do nosso código, ou criar um commit especialmente para a alteração X. Para esses casos, podemos adicionar (`git add`) ao staging nosso código parcialmente com a flag (`-p`).

Observe o caso abaixo:

```diff
function doCrazyThings(strA, strB){
-  const arrayOfStrings = strA.split('');
+  const arrayOfLetters = strA.split('');

-  arrayOfStrings.push(strB);
+  arrayOfLetters.push(strB);

  const nextLetters = arrayOfStrings.map(letter => letter+".");

-  let convertedString = ""

-  nextLetters.forEach(letter => {
-    convertedString += letter;
-  })

+  const convertedString = nextLetters.reduce((result, actualValue) => {
+    return result += actualValue;
+  },"")

  return convertedString;
}
```

Fizemos duas alterações. A primeira, renomeamos a variável `arrayOfStrings` para `arrayOfLetters`. Na segunda, refatoramos a maneira com que geramos o resultado final da função. Poderiamos commitar tudo junto? 

Sim, poderiamos!

Mas queremos? Não, queremos ser organizados.

Para tal dividir as mudanças em dois commits, vamos rodar o seguinte comando:

```bash
git add -p general-functions.js
```

Um menu iterativo irá se abrir, mostrando qual a diferença e o que desejamos fazer com elas. Há uma série de opções, mas, as mais úteis são:

* y => Yes, adiciona o pedaço de código em questão;
* n => No, não adiciona o pedaço do código em questão;
* q => quite, não adicione esse pedaço, matenha os selecionados e saia do menu;
* a => all, adicione todos as próximas alterações;
* d => undo, não adicione nenhum trecho   e saia do menu;
* s => split, quebre o trecho atual em um trecho menor;

Assim, se caso aparecer o trecho todo de código para selecionar, escolha a opção `s` e quebre em uma menor parte. Em seguida, selecione apenas o trecho referente à mudança de nome da variável por exemplo e em seguida saia do menu (`q`).

Você perceberá que em staging terá somente a mudança que você selecionou
