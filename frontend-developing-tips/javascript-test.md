# JavaScript Test

## 测试类型
- 单元测试
- 集成测试
- e2e 测试：功能测试

## 跑测试的方式
- 运行在浏览器中：使用测试工具生成一个HTML，并将测试文件以JS脚本的方式引入并在浏览器中运行。最真实的环境，测试结果比较可靠。
- 运行在 headless 浏览器中：没有 GUI（图形用户界面）的浏览器。使用 headless 浏览器的方式通常会比依赖浏览器的测试来的快，且可以在一个命令行的环境中进行测试。
- 通过 NodeJS 运行：只需要测试文件以及相关依赖包，比如 jsdom (仅用 js 模拟浏览器环境)。相对于前两者来说非常快。

## 测试工具
- 测试启动工具：在浏览器或者 NodeJS 中按照用户配置启动测试，(Karma, Jasmine, Jest, TestCafe, Cypress, webdriverio)
- 提供测试结构：组织测试案例，可读，(Mocha, Jasmine, Jest, Cucumber, TestCafe, Cypress)
- 断言：(Chai, Jasmine, Jest, Unexpected, TestCafe, Cypress)
- 生成、展示测试过程和结果：(Mocha, Jasmine, Jest, Karma, TestCafe, Cypress)
- 提供 Mocks、Spies 和 Stubs：模拟测试场景、隔离测试、插入运行过程，(Sinon, Jasmine, enzyme, Jest, testdouble)
- 生成并对比快照：通过对比生成的组件和数据结构的快照，确保变更和代码变更预期一致，(Jest, Ava)
- 生成代码覆盖报告：(Istanbul, Jest, Blanket)
- 浏览器控制器：在功能测试中模拟用户行为，(Nightwatch, Nightmare, Phantom, Puppeteer, TestCafe, Cypress)
- 界面回归工具：(Applitools, Percy, Wraith, WebdriverCSS)

### 浏览器控制器

有多种控制浏览器的方式来模拟用户的行为：

#### 通过 WebDriver
WebDriver 是浏览器远程控制接口，通过这些接口可以操作浏览器。它本身是一个垮平台、垮语言的协议，

WebDriver is a remote control interface that enables introspection and control of user agents. It provides a platform- and language-neutral wire protocol as a way for out-of-process programs to remotely instruct the behavior of web browsers.

Provided is a set of interfaces to discover and manipulate DOM elements in web documents and to control the behavior of a user agent. It is primarily intended to allow web authors to write tests that automate a user agent from a separate controlling process, but may also be used in such a way as to allow in-browser scripts to control a — possibly separate — browser.

## 选择合适的工具
测试结构+断言工具+如何跑测试



## Cypress


------------------
**参考**
- [An Overview of JavaScript Testing in 2020](https://medium.com/welldone-software/an-overview-of-javascript-testing-7ce7298b9870)
