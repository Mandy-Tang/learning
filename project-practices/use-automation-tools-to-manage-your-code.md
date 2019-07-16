# 使用自动化工具管理你的代码

## 使用 [Husky](https://github.com/typicode/husky) 让 git hook 变得更容易
Git Hook，又称为 git 的钩子，利用 git hook，我们通常可以在 git push，git commit 等 git 命令之前进行一些额外的操作，以避免开发人员做一些无用的提交。比如，在 git commit 之前格式化代码，检查 lint；又或者，在 git push 之前跑测试等等。
使用 husky 可以非常方便得进行 git hook 的配置。
比如，在一个 angular 的项目中，我们进行了如下配置：
```
  "husky": {
    "hooks": {
      "pre-commit": "lint-staged",
      "pre-push": "npm run test:once"
    }
  }
```
在 git commit 之前，运行 lint-staged 命令。
在 git push 之前，运行测试。

## 使用 [lint-staged](https://github.com/okonet/lint-staged) 仅对 git 暂存区中的文件进行操作
我们在每次 git commit 之前，都对代码中的某些文件进行了修改，我们可能配置了一些脚本用于规范我们的代码，比如跑 lint 的脚本用于语法检查，或者跑 prettier 的脚本用于代码格式化。
由于我们每次都只是修改了部分文件，所以没有必要对整个代码仓库的文件都进行检查。此时，使用 lint-staged 就非常方便了，它只会对 git stage 中的文件进行操作。
在上节中，我们已经在 husky 中配置了 commit 之前运行 lint-staged 命令，那么相应的 lint-staged 的配置可以如下：
```
  "lint-staged": {
    "*.{js,ts,scss,html,json}": [
      "prettier --write",
      "git add"
    ]
  }
```
运行 lint-staged，会对 stage 中的文件做 prettier 的代码格式化，并将修改的文件再次加入 stage。

## 使用 TSLint 或者 ESLint 做语法检查
接下来我们会基于 TSLint 做讨论。


## 使用 [Prettier](https://prettier.io/) 进行代码格式化
通常，我们希望不管有多少人工作在同一个代码仓库中，我们写的代码都有统一的格式和规范，prettier 就是这样一个工具，可以帮助我们做代码格式化。
perttier 不但支持 ts 文件，也支持对 css、HTML 等文件进行代码格式化，同时，对三大前端框架的特定的代码结构都提供了支持，例如 React 中的 styled-components。
所以，我们可以使用 lint 做语法检查，把格式化的工作都交给 prettier。
当 tslint 和 prettier 一起使用的时候，可能会有格式化的冲突。我们可以使用 [tslint-config-prettier](https://github.com/prettier/tslint-config-prettier) 禁止 tslint 中与 prettier 冲突的规则。也可以使用 [tslint-plugin-prettier](https://github.com/prettier/tslint-plugin-prettier) 插件让 tslint 用 prettier 做代码格式检查。
所以我们在 tslint.json 中的配置可能是这样的：
```
{
  "extends": ["tslint-plugin-prettier", "tslint-config-prettier"],
  "rules": {
    "prettier": true
  }
}
```
上面的配置需要先安装开发依赖包 tslint-plugin-prettier 和 tslint-config-prettier。

## 实践：在 Angular 项目中的配置 Husky，lint-staged，prettier
首先安装依赖：`npm install husky lint-staged prettier tslint-plugin-prettier --save-dev`
在 `package.json` 中，配置 husky 和 lint-staged：
```
  "husky": {
    "hooks": {
      "pre-commit": "lint-staged",
      "pre-push": "npm run test:once"
    }
  },
  "lint-staged": {
    "src/**/!(*.spec).ts": [
      "tslint --project tsconfig.app.json --fix",
      "prettier --write",
      "git add"
    ],
    "src/**/*.spec.ts": [
      "tslint --project tsconfig.spec.json --fix",
      "prettier --write",
      "git add"
    ],
    "e2e/**/*.ts": [
      "tslint --project e2e/tsconfig.json --fix",
      "prettier --write",
      "git add"
    ],
    "*.{js,scss,html,json}": [
      "prettier --write",
      "git add"
    ]
  }
```
- 这里需要自己单独去配置 `test:once` 的脚本。
- 这里单独跑了 prettier, 而没有使用 `tslint-plugin-prettier` 插件，因为如果用 tslint 跑 prettier 无法使用直接修复的命令。
- 这里做了三种 ts 文件的配置，是因为 tslint 做 type check 时需要相关的 tsconfig 文件，且使用 `--project` 配置 tsconfig 文件时只能配置一个。因此这里分别配置了功能代码、测试代码、e2e 代码三种文件的配置。

在 `tslint.json` 的 `extends` 中加上 `tslint-plugin-prettier`，最后的配置可能是：
```
"extends": ["tslint:recommended", "tslint-plugin-prettier"],
```
你可能还需要配置 `.prettierignore` 文件用于配置不需要 prettier 的文件，和 `.prettierrc` 文件用于配置 prettier 的配置。
