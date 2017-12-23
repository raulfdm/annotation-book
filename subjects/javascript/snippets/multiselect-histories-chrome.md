# Multiseleção nos históricos do Google Chrome

```javascript
function getAllHistories() {
  return new Promise((resolve, reject) => {
    try {
      var listOfHistories = Array.from(
        document
          .querySelector("history-app")
          .shadowRoot.querySelector("#main-container")
          .querySelector("iron-pages")
          .querySelector("history-list")
          .shadowRoot.querySelector("iron-list")
          .querySelectorAll("history-item")
      );
      console.log('listOfHistories',listOfHistories)
      resolve(listOfHistories);
    } catch (error) {
      reject(error);
    }
  });
}

function selectAllHistory(historyList = []) {
  return new Promise((resolve, reject) => {
    try {
      historyList.forEach(historyElement =>
        historyElement.shadowRoot.querySelector("#checkbox").click()
      );
      resolve(true);
    } catch (error) {
      reject(error);
    }
  });
}

function activeButtonDelete() {
  return new Promise((resolve, reject) => {
    try {
      var button = document.body
        .querySelector("history-app")
        .shadowRoot.querySelector("history-toolbar")
        .shadowRoot.querySelector("cr-toolbar-selection-overlay")
        .shadowRoot.querySelector("#delete");

      button.click();
      resolve(true);
    } catch (error) {
      reject(error);
    }
  });
}

function confirmExclusion() {
  return new Promise((resolve, reject) => {
    try {
      var deleteButton = document.body
        .querySelector("history-app")
        .shadowRoot.querySelector("#main-container")
        .querySelector("iron-pages")
        .querySelector("history-list")
        .shadowRoot.querySelector('dialog [slot="button-container"]')
        .children[1];

      deleteButton.click();
      resolve(true);
    } catch (error) {
      reject(error);
    }
  });
}

function start() {
  getAllHistories()
    .then(selectAllHistory)
    .then(activeButtonDelete)
    .then(confirmExclusion)
    .then(() => console.log("SUCCESS"))
    .catch(err => console.error(err));
}
```
