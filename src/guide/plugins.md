---
title: 插件
type: guide
order: 18
---

<<<<<<< HEAD
## 开发插件

插件通常会为 Vue 添加全局功能。插件的范围没有限制——通常是下面几种：

1. 添加全局方法或属性，如 [vue-element](https://github.com/vuejs/vue-element)
=======
## Writing a Plugin
>>>>>>> 4960c14f24457b6dff5547c06bac85709005e4b7

2. 添加全局资源：指令/过滤器/过渡等，如 [vue-touch](https://github.com/vuejs/vue-touch)

3. 添加 Vue 实例方法，通过把它们添加到 Vue.prototype 上实现。

4. 一个库，提供自己的 API，同时提供上面提到的一个或多个功能，如 [vue-router](https://github.com/vuejs/vue-router)

<<<<<<< HEAD
Vue.js 的插件应当有一个公开方法 `install`。这个方法的第一个参数是 `Vue` 构造器，第二个参数是一个可选的选项对象：

``` js
MyPlugin.install = function (Vue, options) {
  // 1. 添加全局方法或属性
  Vue.myGlobalMethod = ...
  // 2. 添加全局资源
  Vue.directive('my-directive', {})
  // 3. 添加实例方法
  Vue.prototype.$myMethod = ...
=======
3. Add some component options by global mixin. e.g. [vuex](https://github.com/vuejs/vuex)

4. Add some Vue instance methods by attaching them to Vue.prototype.

5. A library that provides an API of its own, while at the same time injecting some combination of the above. e.g. [vue-router](https://github.com/vuejs/vue-router)

A Vue.js plugin should expose an `install` method. The method will be called with the `Vue` constructor as the first argument, along with possible options:

``` js
MyPlugin.install = function (Vue, options) {
  // 1. add global method or property
  Vue.myGlobalMethod = function () {
    // something logic ...
  }

  // 2. add a global asset
  Vue.directive('my-directive', {
    bind (el, binding, vnode, oldVnode) {
      // something logic ...
    }
    ...
  })

  // 3. inject some component options
  Vue.mixin({
    created: function () {
      // something logic ...
    }
    ...
  })

  // 4. add an instance method
  Vue.prototype.$myMethod = function (options) {
    // something logic ...
  }
>>>>>>> 4960c14f24457b6dff5547c06bac85709005e4b7
}
```

## 使用插件

通过 `Vue.use()` 全局方法使用插件：

``` js
// 调用 `MyPlugin.install(Vue)`
Vue.use(MyPlugin)
```

也可以传入一个选项对象：

``` js
Vue.use(MyPlugin, { someOption: true })
```

<<<<<<< HEAD
一些插件，如 `vue-router`，如果 `Vue` 是全局变量则自动调用 `Vue.use()`。不过在模块环境中应当始终显式调用 `Vue.use()`：
=======
`Vue.use` automatically prevents you from using the same plugin more than once, so calling it multiple times on the same plugin will install the plugin only once.

Some plugins provided by Vue.js official plugins such as `vue-router` automatically calls `Vue.use()` if `Vue` is available as a global variable. However in a module environment such as CommonJS, you always need to call `Vue.use()` explicitly:
>>>>>>> 4960c14f24457b6dff5547c06bac85709005e4b7

``` js
// 通过 Browserify 或 Webpack 使用 CommonJS 兼容模块
var Vue = require('vue')
var VueRouter = require('vue-router')

// 不要忘了调用此方法
Vue.use(VueRouter)
```

<<<<<<< HEAD
## 已有插件 & 工具

- [vue-router](https://github.com/vuejs/vue-router)：Vue.js 官方路由。与 Vue.js 内核深度整合，让构建单页应用易如反掌。

- [vue-resource](https://github.com/vuejs/vue-resource)：通过 XMLHttpRequest 或 JSONP 发起请求并处理响应。

- [vue-async-data](https://github.com/vuejs/vue-async-data)：异步加载数据插件。

- [vue-validator](https://github.com/vuejs/vue-validator)：表单验证插件。

- [vue-devtools](https://github.com/vuejs/vue-devtools)：Chrome 开发者工具扩展，用于调试  Vue.js 应用。

- [vue-touch](https://github.com/vuejs/vue-touch)：使用 Hammer.js 添加触摸手势指令。

- [vue-element](https://github.com/vuejs/vue-element)：使用 Vue.js 注册自定义元素。

- [vue-animated-list](https://github.com/vuejs/vue-animated-list)： 方便的为 `v-for` 渲染的列表添加动画。

- [用户贡献的工具](https://github.com/vuejs/awesome-vue#libraries--plugins)
=======
Checkout [awesome-vue](https://github.com/vuejs/awesome-vue#libraries--plugins) for a huge collection of community-contributed plugins and libraries.
>>>>>>> 4960c14f24457b6dff5547c06bac85709005e4b7
