# 微信小程序学习笔记

## 从 JS-SDK 到微信小程序
- WeixinJSBridge
- JS-SDK
- JS-SDK 增强版：微信 Web 资源离线存储
- 微信小程序
  - 快速加载
  - 更强大的能力
  - 原生的体验
  - 易用且安全的微信数据开放
  - 高效和简单的开发

## 小程序与普通网页开发的区别
- 逻辑层和渲染层是分开的
- 逻辑层：CoreJS，渲染层：Chrome WebView
- 渲染层，逻辑层，外部通信三者之间通过微信客户端（Native）做中转

## 小程序的执行环境
小程序目前可以运行的三大平台：
- iOS，iOS9 及以上
- Android 平台
- 小程序 IDE
三种平台实现的 ECMAScript 标准不一样。在小程序中，IOS9 和 IOS10 所使用的运行环境没有完全支持 ECMAScript 6。小程序 IDE 提供了 ES6 转 ES5 的工具。
