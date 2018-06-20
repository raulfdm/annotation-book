# Personal Gitbook Annotation

> Personal online nootbook to write my studies, ideas, bug solutions and whatelse I wish :notebook:

* [Github Project](https://github.com/raulfdm/annotation-book)
* [Online Notebook](https://raulfdm-gitbook.surge.sh/)

---

## :warning: Atention :warning:

All my notes were wrote in PT-BR, because it's my main language, but, you can use this project to create your own notebook!

## How to Use

First of all you have to understand what is a Gitbook. For this, I really recommend to access [this website](https://toolchain.gitbook.com/).

If you already know it, following the steps bellow:

1. Clone this project;
1. Install all dependencies:


```bash
cd <folder-created>
yarn install
# or
npm install
```

1. Statt the server running:


```bash
yarn start
# or
npm start
```

## To Deploy

To deploy this book I'm using [Surge](https://surge.sh/). If you want to deploy you own, access their website, install the CLI and configure it.

Then, open `package.json` file and at `deploy` script, set the URL you want to display your book (for free deploy, keep `<my-custom-url>.surge.sh`).

## Notes

* Everytime you add a new plugin run:

  ```bash
  yarn gb:install
  # or
  npm run gb:install
  ```
