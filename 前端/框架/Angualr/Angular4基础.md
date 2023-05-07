### Angular 应用中的 8 个主要构造块：

- [模块 (module)](https://v2.angular.cn/docs/ts/latest/guide/architecture.html#modules)
- [组件 (component)](https://v2.angular.cn/docs/ts/latest/guide/architecture.html#components)
- [模板 (template)](https://v2.angular.cn/docs/ts/latest/guide/architecture.html#templates)
- [元数据 (metadata)](https://v2.angular.cn/docs/ts/latest/guide/architecture.html#metadata)
- [数据绑定 (data binding)](https://v2.angular.cn/docs/ts/latest/guide/architecture.html#data-binding)
- [指令 (directive)](https://v2.angular.cn/docs/ts/latest/guide/architecture.html#directives)
- [服务 (service)](https://v2.angular.cn/docs/ts/latest/guide/architecture.html#services)
- [依赖注入 (dependency injection)](https://v2.angular.cn/docs/ts/latest/guide/architecture.html#dependency-injection)



#### 模块

`NgModule`是一个装饰器函数，它接收一个用来描述模块属性的元数据对象。其中最重要的属性是：

- `declarations` - 声明本模块中拥有的*视图类*。Angular 有三种视图类：[组件](https://v2.angular.cn/docs/ts/latest/guide/architecture.html#components)、[指令](https://v2.angular.cn/docs/ts/latest/guide/architecture.html#directives)和[管道](https://v2.angular.cn/docs/ts/latest/guide/pipes.html)。
- `exports` - declarations 的子集，可用于其它模块的组件[模板](https://v2.angular.cn/docs/ts/latest/guide/architecture.html#templates)。
- `imports` - *本*模块声明的组件模板需要的类所在的其它模块。
- `providers` - [服务](https://v2.angular.cn/docs/ts/latest/guide/architecture.html#services)的创建者，并加入到全局服务列表中，可用于应用任何部分。、
- `bootstrap` - 指定应用的主视图（称为*根组件*），它是所有其它视图的宿主。只有*根模块*才能设置`bootstrap`属性。

```typescript
import { NgModule }      from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
@NgModule({
  imports:      [ BrowserModule ],
  providers:    [ Logger ],
  declarations: [ AppComponent ],
  exports:      [ AppComponent ],
  bootstrap:    [ AppComponent ]
})
export class AppModule { }
```

##### **注意：模板绑定是通过 \*property\* 和\*事件\*来工作的，而不是 \*attribute\*。**



### 组件

每个组件都以`@Component`[装饰器](https://v2.angular.cn/docs/ts/latest/glossary.html#decorator)函数开始，它接受一个*元数据*对象参数。

`@Component`的配置项包括：

- `selector`： CSS 选择器，它告诉 Angular 在*父级* HTML 中查找`<hero-list>`标签，创建并插入该组件。 例如，如果应用的 HTML 包含`<hero-list></hero-list>`， Angular 就会把`HeroListComponent`的一个实例插入到这个标签中。
- `templateUrl`：组件 HTML 模板的模块相对地址

- `providers` - 组件所需服务的*依赖注入提供商*数组。 这是在告诉 Angular：该组件的构造函数需要一个`HeroService`服务，这样组件就可以从服务中获得英雄数据。

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'my-app',
  template: `<h1>Hello {{name}}</h1>`
})
export class AppComponent { name = 'Angular'; }
```



#### 依赖注入

当 Angular 创建组件时，会首先为组件所需的服务请求一个**注入器 (injector)**。

注入器维护了一个服务实例的容器，存放着以前创建的实例。 如果所请求的服务实例不在容器中，注入器就会创建一个服务实例，并且添加到容器中，然后把这个服务返回给 Angular。 当所有请求的服务都被解析完并返回时，Angular 会以这些服务为参数去调用组件的构造函数。 这就是*依赖注入* 

如果注入器还没有`HeroService`，它怎么知道该如何创建一个呢？

简单点说，我们必须先用注入器（injector）为`HeroService`注册一个**提供商（provider）**。 提供商用来创建或返回服务，通常就是这个服务类本身（相当于`new HeroService()`）

我们可以在模块中或组件中注册提供商。

但通常会把提供商添加到[根模块](https://v2.angular.cn/docs/ts/latest/guide/architecture.html#module)上，以便在任何地方都使用服务的同一个实例，或者在组件上使用

##### 主要流程：**[@Injectable()](https://v2.angular.cn/docs/ts/latest/api/core/index/Injectable-decorator.html)** 标识一个类可以被注入器实例化

- 依赖注入渗透在整个 Angular 框架中，被到处使用。
- **注入器 (injector)** 是本机制的核心。
  - 注入器负责维护一个*容器*，用于存放它创建过的服务实例。
  - 注入器能使用*提供商*创建一个新的服务实例。
- *提供商*是一个用于创建服务的配方。
- 把*提供商*注册到注入器。



1. ng generate component example 生成组件带有模版

2. ng generate component example -it 生成内联模版（不会单独生成html文件）

3. ng generate directive my-directive - 生成一个新指令

4. ng generate pipe my-pipe - 生成一个新管道

5. ng generate service my-service - 生成一个新服务

6. ng generate route my-route - 生成一个新路由

7. ng generate class my-class - 生成一个简易的模型类
   