# Remove notifição anti-adblock na EXAME
> https://exame.abril.com.br/

```javascript
MutationObserver = window.MutationObserver || window.WebKitMutationObserver;

const ANTI_AD_CLASSES = [/tp-backdrop/gi, /tp-active/gi];
let timeoutID = 0;

const cleanAd = () => {
  clearTimeout(timeoutID);
  timeoutID = setTimeout(() => {
    document.querySelector("body").classList.remove("tp-modal-open");
    document.querySelector("body > div.tp-modal").remove();
    document.querySelector(".tp-backdrop.tp-active").remove();
  }, 3000);
};

const observer = new MutationObserver((mutations, observer) => {
  mutations.forEach(mutation => {
    const arrayOfClass = mutation.target.className.split(" ");

    arrayOfClass.forEach(foundClass => {
      ANTI_AD_CLASSES.forEach(addClass => {
        if (addClass.test(foundClass)) {
          cleanAd();
        }
      });
    });
  });
});


observer.observe(document, {
  subtree: true,
  attributes: true
});
```
