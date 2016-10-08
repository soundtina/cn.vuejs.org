---
title: Vue 实例
type: guide
order: 3
---

## 构造器

<<<<<<< HEAD
每个 Vue.js 应用的起步都是通过构造函数 `Vue` 创建一个 **Vue 的根实例**：
=======
Every Vue vm is bootstrapped by creating a **root Vue instance** with the `Vue` constructor function:
>>>>>>> 4960c14f24457b6dff5547c06bac85709005e4b7

``` js
var vm = new Vue({
  // 选项
})
```

<<<<<<< HEAD
一个 Vue 实例其实正是一个 [MVVM 模式](https://en.wikipedia.org/wiki/Model_View_ViewModel)中所描述的 ViewModel - 因此在文档中经常会使用 `vm` 这个变量名。
=======
Although not strictly associated with the [MVVM pattern](https://en.wikipedia.org/wiki/Model_View_ViewModel), Vue's design was no doubt inspired by it. As a convention, we often use the variable `vm` (short for ViewModel) to refer to our Vue instances.
>>>>>>> 4960c14f24457b6dff5547c06bac85709005e4b7

在实例化 Vue 时，需要传入一个**选项对象**，它可以包含数据、模板、挂载元素、方法、生命周期钩子等选项。全部的选项可以在 [API 文档](/api)中查看。

可以扩展 `Vue` 构造器，从而用预定义选项创建可复用的**组件构造器**：

``` js
var MyComponent = Vue.extend({
  // 扩展选项
})

// 所有的 `MyComponent` 实例都将以预定义的扩展选项被创建
var myComponentInstance = new MyComponent()
```

<<<<<<< HEAD
尽管可以命令式地创建扩展实例，不过在多数情况下将组件构造器注册为一个自定义元素，然后声明式地用在模板中。我们将在后面详细说明组件系统。现在你只需知道所有的 Vue.js 组件其实都是被扩展的 Vue 实例。
=======
Although it is possible to create extended instances imperatively, most of the time it is recommended to compose them declaratively in templates as custom elements. We will talk about [the component system](components.html) in detail later. For now, you just need to know that all Vue components are essentially extended Vue instances.
>>>>>>> 4960c14f24457b6dff5547c06bac85709005e4b7

## 属性与方法

每个 Vue 实例都会**代理**其 `data` 对象里所有的属性：

``` js
var data = { a: 1 }
var vm = new Vue({
  data: data
})

vm.a === data.a // -> true

// 设置属性也会影响到原始数据
vm.a = 2
data.a // -> 2

// ... 反之亦然
data.a = 3
vm.a // -> 3
```

注意只有这些被代理的属性是**响应的**。如果在实例创建之后添加新的属性到实例上，它不会触发视图更新。我们将在后面详细讨论响应系统。

<<<<<<< HEAD
除了这些数据属性，Vue 实例暴露了一些有用的实例属性与方法。这些属性与方法都有前缀 `$`，以便与代理的数据属性区分。例如：
=======
In addition to data properties, Vue instances expose a number of useful instance properties and methods. These properties and methods are prefixed with `$` to differentiate them from proxied data properties. For example:
>>>>>>> 4960c14f24457b6dff5547c06bac85709005e4b7

``` js
var data = { a: 1 }
var vm = new Vue({
  el: '#example',
  data: data
})

vm.$data === data // -> true
vm.$el === document.getElementById('example') // -> true

// $watch 是一个实例方法
vm.$watch('a', function (newVal, oldVal) {
  // 这个回调将在 `vm.a`  改变后调用
})
```

<<<<<<< HEAD
参考 [API 文档](/api)查看全部的实例属性与方法。

## 实例生命周期

Vue 实例在创建时有一系列初始化步骤——例如，它需要建立数据观察，编译模板，创建必要的数据绑定。在此过程中，它也将调用一些**生命周期钩子**，给自定义逻辑提供运行机会。例如 `created`  钩子在实例创建后调用：
=======
<p class="tip">Note that __you should not use arrow functions on an instance property or callback__ (e.g. `vm.$watch('a', newVal => this.myMethod())`). The reason is arrow functions bind the parent context, so `this` will not be the Vue instance as you expect and `this.myMethod` will be undefined.</p>

Consult the [API reference](/api) for the full list of instance properties and methods.

## Instance Lifecycle Hooks

Each Vue instance goes through a series of initialization steps when it is created - for example, it needs to set up data observation, compile the template, mount the instance to the DOM, and update the DOM when data changes. Along the way, it will also invoke some **lifecycle hooks**, which give us the opportunity to execute custom logic. For example, the `created` hook is called after the instance is created:
>>>>>>> 4960c14f24457b6dff5547c06bac85709005e4b7

``` js
var vm = new Vue({
  data: {
    a: 1
  },
  created: function () {
    // `this` 指向 vm 实例
    console.log('a is: ' + this.a)
  }
})
// -> "a is: 1"
```

<<<<<<< HEAD
也有一些其它的钩子，在实例生命周期的不同阶段调用，如 `compiled`、 `ready` 、`destroyed`。钩子的 `this` 指向调用它的 Vue 实例。一些用户可能会问 Vue.js 是否有“控制器”的概念？答案是，没有。组件的自定义逻辑可以分割在这些钩子中。
=======
There are also other hooks which will be called at different stages of the instance's lifecycle, for example `mounted`, `updated`, and `destroyed`. All lifecycle hooks are called with their `this` context pointing to the Vue instance invoking it. Some users may have been wondering where the concept of "controllers" lives in the Vue world and the answer is: there are no controllers. Your custom logic for a component would be split among these lifecycle hooks.
>>>>>>> 4960c14f24457b6dff5547c06bac85709005e4b7

## 生命周期图示

下图说明了实例的生命周期。你不需要立马弄明白所有的东西，不过以后它会有帮助。

![Lifecycle](/images/lifecycle.png)
