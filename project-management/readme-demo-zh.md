# XX项目
此项目为XX。
此项目通过 [Angular CLI](https://github.com/angular/angular-cli) version 7.2.1 生成，以 [Angular](https://angular.io/) 为框架进行开发。

## 开发环境
- Nodejs: v10.15.0

## 项目启动
- 安装依赖 `npm install`
- 启动开发环境 `npm start`
- 访问 `http://localhost:4200/`，你可以看到项目已经启动。
- liveReload 默认开启，如果修改代码并保存，你可以看到页面会同步更。关闭 liveReload 可以换为 `npm run start:once`

## 在开发时访问不同环境的后端服务
- 前端的请求统一转到 BFF，由 BFF 去请求不同的后端服务。
- 连接 DEV 环境的 BFF：`npm start` 或者 `npm run start:dev` 会通过 `proxy.conf.json` 的配置将请求转发到 DEV 环境的 BFF。
- 连接本地环境的 BFF：`npm run start:local` 会通过 `proxy.local.json` 将请求代理到本地环境的 BFF，但 BFF 实际还是访问的后端环境。通过这个命令可以在本地调试浏览器到 BFF 的请求。
- 如果需要在本地直接访问后端的某个服务，可以修改对应的 proxy 文件中的配置。

## 项目构建
- 运行 `npm run build`
- 对于不同环境的项目构建，请运行 `npm run build:环境`，具体配置请参考 `package.json` 中的脚本。
  - `angular.json` 中的 `projects.architect.build.configuration` 有对应的不同环境的配置。
  - 不同环境的 build 命令配置了不同的环境变量配置文件 `src/enviroments/environment.环境.ts`。如有需要，可以在对应的文件中添加环境变量。
  - 更多配置请参考 Angular 官方文档

## 测试
- 项目现阶段只有单元测试
- 测试框架已从默认的 karma 迁移到 Jest
- 运行一次测试 `npm run test`
- 检测代码改时自动运行测试 `npm run test-once`
- 项目抽取了一个公共的 mock 的模块 `TestingModule`，其中 mock 通用的一些 services，可以直接使用。

## 开发自动化工具
- **prettier**：代码格式化工具
- **lint**：语法检查
- **lint-staged**：对 git stage 的文件进行操作
- **husky**：git hook 工具
  - 已配置 commit 之前会运行 lint-stage，而后者会去运行 prettier 和 lint，具体请参考项目配置文件
  - 已配置 push 之前会运行测试

## 技术栈
- **Angular**：前端框架
- **RxJS**：响应式编程工具
- **TypeScript**：
- **NgRx**：用于状态管理
- **Jest**：测试框架
- **Lodash**：前端常用 util 库
- **GraphQL**：
- 组件库：**Material**
- UI库：无
- 业务相关第三方组件库
  - XXX
  - XXX

## 支持设备和环境
- 支持的设备（系统/分辨率）：支持XX系统，分辨率为XX
- 支持的环境和版本 (浏览器及其版本)：只支持XX浏览器，版本XX之上

## 代码结构
- 项目文件结构原则
  - 遵循 angular 官方推荐结构
  - TBC
- 当前代码结构
  - TBC

## 开发规范
- git commit 格式：XXXX
- 代码小步提交
- 命名规范
  - 遵循 angular 官方推荐命名规范，推荐用 cli 生成 `**Component`，`**Module`，`**Service`,`**Directive` 等
  - page 文件命名为 `**-page.ts`，组件命名为 `**PageComponent`
  - model 文件命名为 `**.model.ts`，类型命名为 `**Model`
  - enum 类型首字母大写，每个枚举值用全大写和下划线组合，例如 FRONT_APP
  - 通用 const 命名为 全大写和下划线组合
  - TBC
- 分支策略
  - XXX

## Icon Font
- 本项目使用 **icon-font-generator** 作为生成 icon font 的工具
- 如何将一个 svg 文件转成 icon font
  - 将 svg 文件 copy 到 `src/assets/icons` 目录下
  - 运行脚本 `npm run icon-font`，会生成新的 icon font 文件
  - 在 html 中 `<app-icon name="文件名称"></app-icon>` 就可以使用对应的 icon
- 开发规范
  - icon 命名请以“图形/含义-形状/样式”的命名方式，例如 “close.svg” “danger-circle” 等，具体请参考已有的 icon font

-----------------------------------

# 工作流程

## 敏捷实践
- 迭代周期：每 XX 周
- 迭代计划会议时间：每迭代 XX
- 站会时间：每天早上 XX 点
- 封版时间：每迭代 XX
- release 频率和时间：每迭代 XX 次上线
- retro 频率和时间：每迭代 XX
- showcase 频率和时间：每迭代 XX
- code reivew 频率和时间：每天下午XX点

## 部署上线
- 三个环境：DEV（XX 用），ST（XX 用），UAT（XX 用）
- 负责人：XX
- 步骤：XX
- 生产环境测试账号：XX
