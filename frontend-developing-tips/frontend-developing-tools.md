# 前端开发工具小知识

------------------------------------------

##### npx 和 npm 的区别
npx 主要解决了两个问题：
- 调用项目内的模块：npx 运行时会到 `node_modules/.bin` 路径和环境变量 `$PATH` 下查找命令是否存在，所以可以直接运行项目内部安装的模块
- 避免全局安装模块：`npx create-react-app my-react-app` 命令会将 `create-react-app` 下载到一个临时目录，使用以后再删除。所以可以避免 `npm install --global` 全局安装之后再运行相关命令。

