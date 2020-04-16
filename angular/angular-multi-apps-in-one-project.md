# 在一个项目中维护多个 Angular 应用

## 单个项目和多个项目

**单项目中维护多个 Angular 应用**
好处：
- node_modules 是公用的，不用为每个应用都维护一份 packages.json, 也不需要为每个应用都去安装一遍依赖
  - 减少因为依赖包锁包不一致引起的问题
- 只需要一个 git repo，方便版本控制，提高开发效率
  - 不用在多个代码仓库之间来回切换
  - 上线时不再需要维护多个代码仓库的版本
  - 当多个应用依赖于相同的 share module 时，不再需要用 submodule 来管理，不会出现 submodule 版本不匹配的问题
  - 不会出现因为多个代码仓库依赖相同的 submodule，重构时只照应到了当前应用而忽略了其他应用的情况
- 方便一起进行 Angular 的升级

**每个项目一个 Angular 应用**

## 步骤
### 创建一个新的项目
`ng new angular-multi-application-project-demo --createApplication=false`
此时除了 `node_modules`，只有一些基础的配置。`angular.json` 中的配置也什么都没有

### 在项目下创建一个新的应用
创建一个名为 first 的应用
`ng g application first --style=scss --routing=true`
- 在 projects 目录下多了一个名为 first 的文件夹，其中为该生成应用的命令生成的所有文件
- 在 first 文件夹下，first 应用拥有自己的 tslint，tsconfig，karmaconfig， browserslist 的配置
- 在根目录的 `angular.json` 文件中多了 `projects.first` 的相关配置。且 `defaultProject` 为 `first`。
- 此时运行 `ng serve`，会启动 first 应用（默认应用）。

使用相同的命令，创建名为 second 的应用
`ng g application second --style=scss --routing=true`
- **因为创建 first 应用时已经安装过相应的依赖，所以创建 second 应用的时候不再需要去更新 package.json 并安装，所以时间会非常快。此处可以体验到共享依赖包的好处。**
- 在根目录的 `angular.json` 文件中多了 `projects.second` 的相关配置。
- 此时运行 `ng serve second`，会启动 second 应用。

### 在项目下创建一个新的库
创建名为 dependences 的库：
`ng g library dependences`

### 在库中新增一个 service 并分别在 first 和 second 应用中使用
`ng generate service hello-world --project=dependences`

### 创建一个子应用并在另外一个应用中以路由的方式引入
- 创建一个新的应用 child
- 给 child 创建两个页面，并创建对应的路由
- 在 first 应用中创建一个页面，并创建对应的路由
- 在 first 应用的一个子路由中引入 child 应用
- 移除 child 中的 BrowserModule
- 将 child 中 RouterModule.forRoot 改为 RouterModule.forChild
- 能够成功嵌入，但是不再能够独立启动

### 改造
- 将child抽成一个单独的lib，再在两个 app 中引入。在 app 中独立引入 BrowerModule 和配置路由
