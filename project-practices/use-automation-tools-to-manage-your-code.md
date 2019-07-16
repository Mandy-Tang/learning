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
```

## 使用 TSLint 或者 ESLint 做语法检查
接下来我们会基于 TSLint 做讨论。


## 使用 [Prettier](https://prettier.io/) 进行代码格式化
通常，我们希望不管有多少人工作在同一个代码仓库中，我们写的代码都有统一的格式和规范，prettier 就是这样一个工具，可以帮助我们做代码格式化。
TSLint 中其实也有一部分的代码格式化的校验，但其只能对 js/ts 文件进行校验，且规则没有 prettier 全面；而 perttier 不但支持 js/ts，也支持对 css、HTML 等文件进行代码格式化，同时，对三大前端框架的特定的代码结构都提供了支持，例如 React 中的 styled-components。
所以，我们可以使用 lint 做检查，把格式化的工作都交给 prettier。
当 tslint 和 prettier 一起使用的时候，可能会有格式化的冲突，我们可以使用[tslint-config-prettier](https://github.com/prettier/tslint-config-prettier)
