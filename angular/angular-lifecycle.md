# Angular 生命周期

## When a component is created
```
constructor(); // 在构造函数完成之前，被绑定的输入属性都还没有值；在构造函数中除了使用简单的值对局部变量进行赋值外，什么都不应该做。
ngOnChanges(); // 访问被绑定的输入属性的第一次机会。
ngOnInit(); // 在整个生命周期中只执行一次，可以在这里进行复杂的初始化逻辑
ngDoCheck();
ngAfterContentInit(); // 在创建了组件的外来投影之后调用；AfterContent在这里无须担心单向数据流规则；
ngAfterContentChecked();
ngAfterViewInit(); // 在创建了组件的子视图之后调用；在这里需要遵循单向数据流原则，即禁止在一个视图已经被组合好之后再更新视图；AfterView都是在组件的视图已经组好好之后触发的，如果在该方法中更新组件中被绑定属性，会报错，所以应该延迟更新
ngAftreViewChecked();
```

## When a component is destroyed
```
ngOnDestroy(); // 应该在这里释放那些不会被垃圾收集器自动回收的资源。
```

## When input change
```
ngOnchanges(); // 检测到组件或指令的输入属性发生变化时执行，这里判断变化进行的是浅比较
ngDoCheck(); // 使用其用来检测Angular无法识别的更改，调用非常频繁
ngAfterContentChecked();
ngAfterViewChecked();
```