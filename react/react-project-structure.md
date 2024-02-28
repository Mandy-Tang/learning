# 搭建一个 react 项目

使用到的工具
- 包管理工具 yarn
- react脚手架工具 create-react-app
- webpack 配置修改工具 react-app-rewired
- git钩子 husky, lint-staged
- ts语法检查 eslint
- 样式语法检查 stylelint
- 代码格式化 prettier

## 使用 create-react-app 生成项目
```
$ npx create-react-app my-app --typescript
$ # 或者
$ yarn create react-app my-app --typescript
```

## 使用 react-app-rewired 使 webpack 可配置

1. 添加依赖包`react-app-rewired`
```
$ yarn add react-app-rewired --dev
```
2. 修改 `packages.scripts` 中的命令：
```
// package.json

-    "start": "react-scripts start",
-    "build": "react-scripts build",
-    "test": "react-scripts test",
// 将以上三个命令替换为：
+    "start": "react-app-rewired start",
+    "build": "react-app-rewired build",
+    "test": "react-app-rewired test",
```
3. 在根目录下增加文件 `config-overrides.js` 用于修改 webpack 配置，
```
// config.overrides.js

module.exports = function override(config, env) {
  //do stuff with the webpack config...
  return config;
}
```

## 工程配置
首先推荐一个 node 的工具包 [mrm](https://mrm.js.org/)，用这个工具可以快速初始化一些工程化配置，例如 `package.json`, `.gitignore`, `.eslintrc` 等等。
1. 增加 `.npmrc` 配置文件，固定项目的 npm 源
```
// .npmrc

registry=http://registry.npmjs.org
```
2. 增加 `.editorconfig` 配置文件
```
$ npx mrm editorconfig
```
3. 增加 `eslint` 配置
```
$ yarn add eslint --save && yarn eslint --init
```

## git test
test

