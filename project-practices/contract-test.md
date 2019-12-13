# 基于 GraphQL 的契约测试

## What is Contract Test
- 老马提出

## Why We Need Contract Test
在前后端分离开发，或者微服务架构的场景下，或者有第三方
- 保证接口的一致性
- 前后端测试解耦
  消费者和提供者的测试不需要相互依赖，可以独立进行测试
- 测试前移
  集成测试只有在前后端都开发好之后才能进行，如果这个时候发现接口错误，那就得再回过头去改接口。而契约测试可以发生在开发阶段

## HOW

### 步骤
以消费者驱动的契约测试
1.消费者根据业务需求编写好契约文件，契约文件中包含返回的数据
2.消费者向契约文件发起请求，契约文件返回对应的数据，消费者通过得到的数据判断是否为预期的结果
3.契约文件向生产者发起请求，得到生产者真实的返回结果并且与契约文件中的数据进行校验，判断生产者返回的数据是否满足契约的要求。如果无法通过校验，说明生产者提供的服务发生了改变，或者不满足消费者的需求。


### 工具
- Pact
  基于 restful 接口
- Pact + GraphQL

## GraphQL 的契约测试

------
参考资料：

- [聊一聊契约测试](https://insights.thoughtworks.cn/about-contract-test/)
- [A Comprehensive Guide to Contract Testing APIs in a Service Oriented Architecture](https://medium.com/@liran.tal/a-comprehensive-guide-to-contract-testing-apis-in-a-service-oriented-architecture-5695ccf9ac5a)
- [契约测试](https://www.jianshu.com/p/e318fadf8553)
- [契约测试之核心解惑](https://www.jianshu.com/p/ca82cde5b125)
- [契约测试之Pact By Example](https://www.jianshu.com/p/681047496728)
- [Start testing your GraphQL Schema, Queries and, Mutations!](https://hackernoon.com/start-testing-your-graphql-schema-queries-and-mutations-b514911b1368)
- [Implementing a Consumer-Driven Contract for a React App with Pact and Jest](https://reflectoring.io/pact-react-consumer)
- [Implementing a Consumer-Driven Contract for a GraphQL Consumer with Node and Apollo](https://reflectoring.io/pact-node-graphql-consumer/)
