# 依赖注入（DI，Dependency Injector）

**依赖注入是一种设计模式**
在面向对象编程中，如果我们需要在 Class A 中使用 Class B，一般情况下，我们需要在 Class A 中显示地 new 一个 Class B。
依赖注入的思想是，我们只需要在 Class A 中定义一个 Class B 的对象，而不是重新 new 一个 B 对象；Class A 会从外部请求获取 B 对象。
在 Angular 中，DI 框架会在实例化某个类时向其提供这个类所声明的依赖项。

**术语**
- **服务**
- **依赖**
- **服务提供商**
- **注入器**
- **依赖注入令牌（DI Token）**
注入器内部维护了一个**令牌-提供商**的映射表，令牌相当于这个映射表的键值。比如`constructor(heroService: HeroService)`中，类`HeroService`类型就是令牌，我们通过这个令牌，在注入器中获取`HeroService`的实例。

## 注入器

### 多级依赖注入器
Angular 有一个与组件树平行的注入器树（结构完全相同且一一对应）。
- **平台注入器**：在启动期间内部使用，用于配置与平台相关的配置项。
- **根注入器**：根模块 AppModule 的注入器，可以在根模块的 providers 中配置，或者在装饰器元数据中使用`providedIn:'root'`。
    - 根注入器创建于启动过程中。
    - 如果你在 AppModule 的 @NgModule() 元数据中配置了全应用级的提供商，它就会覆盖通过 @Injectable() 配置的那一个。 
- **NgModel级注入器**：可以在 NgModule 的 providers 中配置，也可以在 @Injectable() 的 providedIn 选项中指定模块。
    - 在 NgModule 的 providers 中配置不能摇树优化。
    - 在 @Injectable() 中的 providedIn 选项中指定模块这种方式可以被摇树优化。
- **组件级注入器**：每个组件**实例**的注入器，与组件的生命周期一样。
    - 组件上的注入器实际上并不属于组件，而属于组件实例所附着的元素，所以更应该叫做元素注入器。
    - 同一个元素上的组件和指令共享一个注入器。

### 注入器冒泡
当一个组件申请获得一个依赖时，会首先在组件注入器上查找是否有对应的提供商；如果没有找到，它就把这个申请转给它的父组件的注入器来处理；同理，如果父组件的注入器也无法满足，父组件就继续把这个请求转给更上一层的注入器，直到找到一个能处理这个申请的注入器。如果最后超过了祖先也没有找到，Angular 就会抛出错误。
如果在不同层级上为同一个 DI 令牌提供了服务商，Angular 会使用它遇到的第一个服务提供商来提供依赖。
可以使用 @Host() 来阻止冒泡，这样，对提供商的查找就只会停留在该组件的宿主元素的注入器上。

- 在某个注入器的范围内，服务是单例的
- @Optional() 表示依赖是可选的，当找不到对应的服务提供商时，Angular 会返回 null 然后继续执行。此时需要程序能够正确处理服务依赖为空的情况。
- @Host() 会禁止在宿主组件以上的搜索。宿主组件通常就是请求该依赖的那个组件。但当该组件投影进某个父组件时，那个父组件就会变成宿主。
- 使用 @Inject() 指定自定义提供商。
- 使用 @Self 限定只在该组件的注入器中查找提供商。使用 @SkipSelf 装饰器让你跳过局部注入器，并在注入器树中向上查找，以发现哪个提供商满足该依赖。

> **@Injectable()** 当 Angular 创建一个带有参数的类的实例时，会去查找有关这些参数的类型以及供注入使用的元数据，以便找到正确的服务。如果 Angular 无法找到参数信息，它就会抛出一个错误。
> 而当把 TypeScript 编译成 JavaScript 的时候，一般会丢弃参数的类型信息。只有当类具有装饰器，并且 `tsconfig.json` 中的编译器选项 `emitDecoratorMetadata` 为 `true` 时，TypeScript 才会保留这些信息。CLI 所配置的 `tsconfig.json` 就带有 `emitDecoratorMetadata: true`。
> 所以我们需要给所有的服务加上 @Injectable()的装饰器。

## 服务提供商
