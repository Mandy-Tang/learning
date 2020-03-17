# OpenShift 简介

## 什么是 OpenShift
- 红帽
- 开源的容器应用 Paas 平台
- Kubernetes 和 docker
- 帮助开发人员快速在云端开发、托管、扩展、交付应用。

> 云计算的三种服务模式
> - Iaas 基础设施即服务
> - Paas 平台即服务
> - Saas 软件即服务

## OpenShift Online
- 分层系统
  - docker
  - k8s
  - 源代码管理、构建、部署
  - 大规模管理和发布镜像
  - 大规模管理应用
  - 用户管理
  - 网络基础设施
- 系统架构
  - 微服务架构
  - 使用restful API暴露核心对象
  - 使用Controller获取核心对象的状态，执行相关的操作，并修改对应的状态

### 核心概念

#### Container
#### Image
#### Container Image Registries
#### Pods
   - 沿用 k8s 中 pod 的概念，是部署在一个 host 上的一个或者多个 container 的集合。是定义、部署、管理的最小计算单元。
   - pod 类似于一个 container 的机器实例（Pods are the rough equivalent of a machine instance (physical or virtual) to a container. ），分配了内部 IP，拥有完整的端口信息，一个 pod 中的容器可以共享这个 pod 的网络和存储资源。
   - 具有生命周期：定义 - 在 node 上跑起来 - 因为 containers 都移除等原因删除
   - 不可变，修改配置、镜像等都是删除原有 pod 再新建
#### Services
  - k8s 中的概念，作为一个内部的负载均衡器服务。一个 service 背后维护了几个复制的 pod，当 service 收到一个请求时，会转发到某一个 pod 上。
  - 如果不需要负载均衡或者单一IP地址，可配置 headless service
#### Labels
  - k8s 中的概念
#### Endpoints:
The servers that back a service are called its endpoints, and are specified by an object of type Endpoints with the same name as the service.
#### Users
#### Namespaces
- K8s 中的概念，提供了一种机制去确定一个集群中资源的范围（A Kubernetes namespace provides a mechanism to scope resources in a cluster.）
- 避免命名冲突、分配用户管理权限、限制共同资源的消耗（The ability to limit community resource consumption.）
#### Projects
- k8s namespace + 一些附加说明
- project 是普通用户访问资源的渠道，且需要管理员提供访问项目的权限。
- 项目为一个群体提供了一个独立的环境去组织和管理内容，并与另外一个群体完全隔离。
#### Builds
构建是一个过程，给定一些输入参数，按照构建的配置，得到一个期望的结果。在这里，构建通常是指利用一些入参或者源码生成一个镜像的过程。
- Source to Image Build
- pipeline build
  - Jenkins
#### Image Streams


### 架构组件
- k8s 架构
  -
