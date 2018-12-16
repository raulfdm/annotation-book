# Directory Tree

Sometimes we do want to show certain folder structure like this:

```
.
├── README.md
├── angular.json
├── package.json
├── src
│   ├── app
│   │   ├── app-routing.module.ts
│   │   ├── app.component.html
│   │   ├── app.component.scss
│   │   ├── app.component.spec.ts
│   │   ├── app.component.ts
│   │   └── app.module.ts
├── tsconfig.json
└── tslint.json
```

Instead write by yourself this tree, there's a package which does this exact service: [`tree`](http://mama.indstate.edu/users/ice/tree/)

## Installation

### MacOS

For macos, you have to install it by running:

```bash
brew install tree
```

([font](https://superuser.com/a/359727))

## Windows/Linux

If I'm not in a mistaken, for both linux and windows are already pre-installed via terminal/cmd

## Running

With the app ready, only thing you have to do is go inside the folder you want to print and run via terminal:

```bash
tree
```

## Ignoring

Sometimes we do want to ignore certain folder. For those cases, you just have to run:

```bash
tree -I 'node_modules|cache|test_*'
```
