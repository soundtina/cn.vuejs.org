---
title: 列表渲染
type: guide
order: 8
---

## `v-for`

<<<<<<< HEAD
可以使用 `v-for` 指令基于一个数组渲染一个列表。这个指令使用特殊的语法，形式为 `item in items`，`items` 是数据数组，`item` 是当前数组元素的**别名**：

**示例：**
=======
We can use the `v-for` directive to render a list of items based on an array. The `v-for` directive requires a special syntax in the form of `item in items`, where `items` is the source data array and `item` is an **alias** for the array element being iterated on:

### Basic Usage
>>>>>>> 4960c14f24457b6dff5547c06bac85709005e4b7

``` html
<ul id="example-1">
  <li v-for="item in items">
    {{ item.message }}
  </li>
</ul>
```

``` js
var example1 = new Vue({
  el: '#example-1',
  data: {
    items: [
      { message: 'Foo' },
      { message: 'Bar' }
    ]
  }
})
```

<<<<<<< HEAD
**结果：**
=======
Result:
>>>>>>> 4960c14f24457b6dff5547c06bac85709005e4b7

{% raw %}
<ul id="example-1" class="demo">
  <li v-for="item in items">
    {{item.message}}
  </li>
</ul>
<script>
var example1 = new Vue({
  el: '#example-1',
  data: {
    items: [
      { message: 'Foo' },
      { message: 'Bar' }
    ]
  },
  watch: {
    items: function () {
      smoothScroll.animateScroll(null, '#example-1')
    }
  }
})
</script>
{% endraw %}

<<<<<<< HEAD
在 `v-for` 块内我们能完全访问父组件作用域内的属性，另有一个特殊变量 `$index`，正如你猜到的，它是当前数组元素的索引：
=======
Inside `v-for` blocks we have full access to parent scope properties. `v-for` also supports an optional second argument for the index of the current item.
>>>>>>> 4960c14f24457b6dff5547c06bac85709005e4b7

``` html
<ul id="example-2">
  <li v-for="(item, index) in items">
    {{ parentMessage }} - {{ index }} - {{ item.message }}
  </li>
</ul>
```

``` js
var example2 = new Vue({
  el: '#example-2',
  data: {
    parentMessage: 'Parent',
    items: [
      { message: 'Foo' },
      { message: 'Bar' }
    ]
  }
})
```

<<<<<<< HEAD
**结果：**
=======
Result:
>>>>>>> 4960c14f24457b6dff5547c06bac85709005e4b7

{% raw%}
<ul id="example-2" class="demo">
  <li v-for="(item, index) in items">
    {{ parentMessage }} - {{ index }} - {{ item.message }}
  </li>
</ul>
<script>
var example2 = new Vue({
  el: '#example-2',
  data: {
    parentMessage: 'Parent',
    items: [
      { message: 'Foo' },
      { message: 'Bar' }
    ]
  },
  watch: {
    items: function () {
      smoothScroll.animateScroll(null, '#example-2')
    }
  }
})
</script>
{% endraw %}

<<<<<<< HEAD
另外，你可以为索引指定一个别名（如果 `v-for` 用于一个对象，则可以为对象的键指定一个别名）：

``` html
<div v-for="(index, item) in items">
  {{ index }} {{ item.message }}
</div>
```

从 1.0.17 开始可以使用 `of` 分隔符，更接近 JavaScript 遍历器语法：
=======
You can also use `of` as the delimiter instead of `in`, so that it is closer to JavaScript's syntax for iterators:
>>>>>>> 4960c14f24457b6dff5547c06bac85709005e4b7

``` html
<div v-for="item of items"></div>
```

<<<<<<< HEAD
## template v-for
=======
### Template v-for
>>>>>>> 4960c14f24457b6dff5547c06bac85709005e4b7

类似于 template `v-if`，也可以将 `v-for` 用在 `<template>` 标签上，以渲染一个包含多个元素的块。例如：

``` html
<ul>
  <template v-for="item in items">
    <li>{{ item.msg }}</li>
    <li class="divider"></li>
  </template>
</ul>
```

<<<<<<< HEAD
## 数组变动检测

### 变异方法

Vue.js 包装了被观察数组的变异方法，故它们能触发视图更新。被包装的方法有：

- `push()`
- `pop()`
- `shift()`
- `unshift()`
- `splice()`
- `sort()`
- `reverse()`

你可以打开浏览器的控制台，用这些方法修改上例的 `items` 数组。例如：`example1.items.push({ message: 'Baz' })`。

### 替换数组

变异方法，如名字所示，修改了原始数组。相比之下，也有非变异方法，如 `filter()`, `concat()` 和 `slice()`，不会修改原始数组而是返回一个新数组。在使用非变异方法时，可以直接用新数组替换旧数组：

``` js
example1.items = example1.items.filter(function (item) {
  return item.message.match(/Foo/)
})
```

可能你觉得这将导致 Vue.js 弃用已有 DOM 并重新渲染整个列表——幸运的是并非如此。 Vue.js 实现了一些启发算法，以最大化复用 DOM 元素，因而用另一个数组替换数组是一个非常高效的操作。

### track-by

有时需要用全新对象（例如通过 API 调用创建的对象）替换数组。因为 `v-for` 默认通过数据对象的特征来决定对已有作用域和 DOM 元素的复用程度，这可能导致重新渲染整个列表。但是，如果每个对象都有一个唯一 ID 的属性，便可以使用 `track-by` 特性给 Vue.js 一个提示，Vue.js 因而能尽可能地复用已有实例。

例如，假定数据为：

``` js
{
  items: [
    { _uid: '88f869d', ... },
    { _uid: '7496c10', ... }
  ]
}
```

然后可以这样给出提示：

``` html
<div v-for="item in items" track-by="_uid">
  <!-- content -->
</div>
```

然后在替换数组 `items` 时，如果 Vue.js 遇到一个包含 `_uid: '88f869d'` 的新对象，它知道它可以复用这个已有对象的作用域与 DOM 元素。

### track-by $index

如果没有唯一的键供追踪，可以使用 `track-by="$index"`，它强制让 `v-for` 进入原位更新模式：片断不会被移动，而是简单地以对应索引的新值刷新。这种模式也能处理数据数组中重复的值。

这让数据替换非常高效，但是也会付出一定的代价。因为这时 DOM 节点不再映射数组元素顺序的改变，不能同步临时状态（比如 `<input>` 元素的值）以及组件的私有状态。因此，如果 `v-for` 块包含 `<input>` 元素或子组件，要小心使用 `track-by="$index"`

### 问题

因为 JavaScript 的限制，Vue.js **不能**检测到下面数组变化：

1. 直接用索引设置元素，如 `vm.items[0] = {}`；
2. 修改数据的长度，如 `vm.items.length = 0`。

为了解决问题 (1)，Vue.js 扩展了观察数组，为它添加了一个 `$set()` 方法：

``` js
// 与 `example1.items[0] = ...` 相同，但是能触发视图更新
example1.items.$set(0, { childMsg: 'Changed!'})
```

至于问题 (2)，只需用一个空数组替换 `items`。

除了 `$set()`， Vue.js 也为观察数组添加了 `$remove()` 方法，用于从目标数组中查找并删除元素，在内部它调用 `splice()` 。因此，不必这样：

``` js
var index = this.items.indexOf(item)
if (index !== -1) {
  this.items.splice(index, 1)
}
```

只用这样：

``` js
this.items.$remove(item)
```

#### 使用 `Object.freeze()`

在遍历一个数组时，如果数组元素是对象并且对象用 `Object.freeze()` 冻结，你需要明确指定 `track-by`。在这种情况下如果 Vue.js 不能自动追踪对象，将给出一条警告。

## 对象 v-for

也可以使用 `v-for` 遍历对象。除了 `$index` 之外，作用域内还可以访问另外一个特殊变量 `$key`。
=======
### Object v-for

You can also use `v-for` to iterate through the properties of an object.
>>>>>>> 4960c14f24457b6dff5547c06bac85709005e4b7

``` html
<ul id="repeat-object" class="demo">
  <li v-for="value in object">
    {{ value }}
  </li>
</ul>
```

``` js
new Vue({
  el: '#repeat-object',
  data: {
    object: {
      FirstName: 'John',
      LastName: 'Doe',
      Age: 30
    }
  }
})
```

<<<<<<< HEAD
**结果：**
=======
Result:
>>>>>>> 4960c14f24457b6dff5547c06bac85709005e4b7

{% raw %}
<ul id="repeat-object" class="demo">
  <li v-for="value in object">
    {{ value }}
  </li>
</ul>
<script>
new Vue({
  el: '#repeat-object',
  data: {
    object: {
      FirstName: 'John',
      LastName: 'Doe',
      Age: 30
    }
  }
})
</script>
{% endraw %}

<<<<<<< HEAD
也可以给对象的键提供一个别名：
=======
You can also provide a second argument for the key:

``` html
<div v-for="(value, key) in object">
  {{ key }} : {{ value }}
</div>
```

And another for the index:
>>>>>>> 4960c14f24457b6dff5547c06bac85709005e4b7

``` html
<div v-for="(value, key, index) in object">
  {{ index }}. {{ key }} : {{ value }}
</div>
```

<<<<<<< HEAD
<p class="tip">在遍历对象时，是按 `Object.keys()` 的结果遍历，但是不能保证它的结果在不同的 JavaScript 引擎下是一致的。</p>

## 值域 v-for

`v-for` 也可以接收一个整数，此时它将重复模板数次。
=======
<p class="tip">When iterating over an object, the order is based on the key enumeration order of `Object.keys()`, which is **not** guaranteed to be consistent across JavaScript engine implementations.</p>

### Range v-for

`v-for` can also take an integer. In this case it will repeat the template that many times.
>>>>>>> 4960c14f24457b6dff5547c06bac85709005e4b7

``` html
<div>
  <span v-for="n in 10">{{ n }}</span>
</div>
```

结果：

{% raw %}
<div id="range" class="demo">
  <span v-for="n in 10">{{ n }} </span>
</div>
<script>
new Vue({ el: '#range' })
</script>
{% endraw %}

<<<<<<< HEAD
## 显示过滤/排序的结果

有时我们想显示过滤/排序过的数组，同时不实际修改或重置原始数据。有两个办法：

1. 创建一个计算属性，返回过滤/排序过的数组；
2. 使用内置的过滤器 `filterBy` 和 `orderBy`。

计算属性有更好的控制力，也更灵活，因为它是全功能 JavaScript。但是通常过滤器更方便，详细见 [API](/api/#filterBy)。
=======
### Components and v-for

> This section assumes knowledge of [Components](/guide/components.html). Feel free to skip it and come back later.

You can directly use `v-for` on a custom component, like any normal element:

``` html
<my-component v-for="item in items"></my-component>
```

However, this won't automatically pass any data to the component, because components have isolated scopes of their own. In order to pass the iterated data into the component, we should also use props:

``` html
<my-component
  v-for="(item, index) in items"
  v-bind:item="item"
  v-bind:index="index">
</my-component>
```

The reason for not automatically injecting `item` into the component is because that makes the component tightly coupled to how `v-for` works. Being explicit about where its data comes from makes the component reusable in other situations.

Here's a complete example of a simple todo list:

``` html
<div id="todo-list-example">
  <input
    v-model="newTodoText"
    v-on:keyup.enter="addNewTodo"
    placeholder="Add a todo"
  >
  <ul>
    <li
      is="todo-item"
      v-for="(todo, index) in todos"
      v-bind:title="todo"
      v-on:remove="todos.splice(index, 1)"
    ></li>
  </ul>
</div>
```

``` js
Vue.component('todo-item', {
  template: '\
    <li>\
      {{ title }}\
      <button v-on:click="$emit(\'remove\')">X</button>\
    </li>\
  ',
  props: ['title']
})

new Vue({
  el: '#todo-list-example',
  data: {
    newTodoText: '',
    todos: [
      'Do the dishes',
      'Take out the trash',
      'Mow the lawn'
    ]
  },
  methods: {
    addNewTodo: function () {
      this.todos.push(this.newTodoText)
      this.newTodoText = ''
    }
  }
})
```

{% raw %}
<div id="todo-list-example" class="demo">
  <input
    v-model="newTodoText" v
    v-on:keyup.enter="addNewTodo"
    placeholder="Add a todo"
  >
  <ul>
    <li
      is="todo-item"
      v-for="(todo, index) in todos"
      v-bind:title="todo"
      v-on:remove="todos.splice(index, 1)"
    ></li>
  </ul>
</div>
<script>
Vue.component('todo-item', {
  template: '\
    <li>\
      {{ title }}\
      <button v-on:click="$emit(\'remove\')">X</button>\
    </li>\
  ',
  props: ['title']
})
new Vue({
  el: '#todo-list-example',
  data: {
    newTodoText: '',
    todos: [
      'Do the dishes',
      'Take out the trash',
      'Mow the lawn'
    ]
  },
  methods: {
    addNewTodo: function () {
      this.todos.push(this.newTodoText)
      this.newTodoText = ''
    }
  }
})
</script>
{% endraw %}

## key

When Vue.js is updating a list of elements rendered with `v-for`, it by default uses an "in-place patch" strategy. If the order of the data items has changed, instead of moving the DOM elements to match the order of the items, Vue will simply patch each element in-place and make sure it reflects what should be rendered at that particular index. This is similar to the behavior of `track-by="$index"` in Vue 1.x.

This default mode is efficient, but only suitable **when your list render output does not rely on child component state or temporary DOM state (e.g. form input values)**.

To give Vue a hint so that it can track each node's identity, and thus reuse and reorder existing elements, you need to provide a unique `key` attribute for each item. An ideal value for `key` would be the unique id of each item. This special attribute is a rough equivalent to `track-by` in 1.x, but it works like an attribute, so you need to use `v-bind` to bind it to dynamic values (using shorthand here):

``` html
<div v-for="item in items" :key="item.id">
  <!-- content -->
</div>
```

It is recommended to provide a `key` with `v-for` whenever possible, unless the iterated DOM content is simple, or you are intentionally relying on the default behavior for performance gains.

Since it's a generic mechanism for Vue to identify nodes, the `key` also has other uses that are not specifically tied to `v-for`, as we will see later in the guide.

## Array Change Detection

### Mutation Methods

Vue wraps an observed array's mutation methods so they will also trigger view updates. The wrapped methods are:

- `push()`
- `pop()`
- `shift()`
- `unshift()`
- `splice()`
- `sort()`
- `reverse()`

You can open the console and play with the previous examples' `items` array by calling their mutation methods. For example: `example1.items.push({ message: 'Baz' })`.

### Replacing an Array

Mutation methods, as the name suggests, mutate the original array they are called on. In comparison, there are also non-mutating methods, e.g. `filter()`, `concat()` and `slice()`, which do not mutate the original Array but **always return a new array**. When working with non-mutating methods, you can just replace the old array with the new one:

``` js
example1.items = example1.items.filter(function (item) {
  return item.message.match(/Foo/)
})
```

You might think this will cause Vue to throw away the existing DOM and re-render the entire list - luckily, that is not the case. Vue implements some smart heuristics to maximize DOM element reuse, so replacing an array with another array containing overlapping objects is a very efficient operation.

### Caveats

Due to limitations in JavaScript, Vue **cannot** detect the following changes to an array:

1. When you directly set an item with the index, e.g. `vm.items[indexOfItem] = newValue`
2. When you modify the length of the array, e.g. `vm.items.length = newLength`

To overcome caveat 1, both of the following will accomplish the same as `vm.items[indexOfItem] = newValue`, but will also trigger state updates in the reactivity system:

``` js
// Vue.set
Vue.set(example1.items, indexOfItem, newValue)
```
``` js
// Array.prototype.splice`
example1.items.splice(indexOfItem, 1, newValue)
```

To deal with caveat 2, you can also use `splice`:

``` js
example1.items.splice(newLength)
```

## Displaying Filtered/Sorted Results

Sometimes we want to display a filtered or sorted version of an array without actually mutating or resetting the original data. In this case, you can create a computed property that returns the filtered or sorted array.

For example:

``` html
<li v-for="n in evenNumbers">{{ n }}</li>
```

``` js
data: {
  numbers: [ 1, 2, 3, 4, 5 ]
},
computed: {
  evenNumbers: function () {
    return this.numbers.filter(function (number) {
      return number % 2 === 0
    })
  }
}
```

Alternatively, you can also just use a method where computed properties are not feasible (e.g. inside nested `v-for` loops):

``` html
<li v-for="n in even(numbers)">{{ n }}</li>
```

``` js
data: {
  numbers: [ 1, 2, 3, 4, 5 ]
},
methods: {
  even: function (numbers) {
    return numbers.filter(function (number) {
      return number % 2 === 0
    })
  }
}
```
>>>>>>> 4960c14f24457b6dff5547c06bac85709005e4b7
