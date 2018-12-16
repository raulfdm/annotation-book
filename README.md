# Personal Notebook Annotation

> Personal online notebook to write down my studies, ideas, bug solutions and what else I want to :notebook:

- [Github Project](https://github.com/raulfdm/annotation-book)
- [Online Notebook](https://raulfdm-gitbook.surge.sh/)

---

> ⚠️ Attention ️️️️⚠️
> All my notes were wrote in PT-BR because it's my mother language But you can use it to create your own.

## How to Use

The first version of this project was based on Gitbook. However, after read [this issue](https://github.com/GitbookIO/gitbook/issues/1808) on Gitbook's repository it seems the team will not keep Gitbook V2 open-source. Also there's no reply and answers on the issues there so I've just decided to find another open-source and well maintained solution which solves my problem.

### Docsify

[Docsify](https://docsify.js.org) is a really nice tool to build web documentation writing markdown. They use VueJS, which makes the lib way lighter and also fast.

I really like this tool because:

- it's been maintained by the community;
- run fast on dev mode and don't have to build;
- Easy configurable and customizable;
- Documentation clear and neat with some really good examples and showcases;

### Running

1. Clone this project;
1. Install the dependencies:

```bash
yarn install
# or
npm install
```

1. Run it locally:

```bash
yarn dev
# or
npm dev
```

## Folder Structure

Here's the folder structure of this project:

```
annotation-book/
├── docs/
│   ├── development/*
│   └── ...
├── _sidebar.md
├── index.html
└── package.json
```

However, it's also possible to customize as you want, like add all those files inside a `docs` folder. [See more about it here](https://docsify.js.org/#/quickstart).

### \_sidebar.md

Here's the main sidebar structure. If you navigate through folders inside `docs`, you'll more `_sidebar.md` files. Fortunately Docsify allow us to have nested Sidebars as you can see on [their documentation](https://docsify.js.org/#/more-pages?id=nested-sidebars).

### index.html

Here's the entry point of the project. It's the place where we init `Docisfy` and also import `themes`, `plugins` and customize things.

Also the this is the file to be hosted (together with the docs of course) by the http server (e.g. Netilify, Github Pages, Gitlab Pages, etc.).
