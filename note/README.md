# Vue3.2源码分析
[Vue3.x](https://v3.cn.vuejs.org)文档地址 https://v3.cn.vuejs.org/
``` bash
git clone https://github.com/coddingus/vue-next.git
pnpm install
```
## Vue3.x的优化
### 源码优化
目的是为了让代码更容易维护
#### 采用monorepo
采用monorepo，这样做的好处是每个组件可以单独打包，可以按需引入，模块拆分更细化，更易维护和阅读

另外一些 package（比如 reactivity 响应式库）是可以独立于 Vue.js 使用的，按需引入，减小了引用包的体积大小
#### 采用Typescript
使用类型语言非常有利于代码的维护,ts相对于Flow有更好的类型检查功能，支持复杂类型推导
### 性能优化
#### 源码体积
* 移除一些冷门的 feature（比如 filter、inline-template 等
* 引入 tree-shaking 的技术，减少打包体积
#### 数据劫持优化
采用Proxy劫持数据,相对于`Object.defineProperty`
* `Proxy`可以劫持数据的增加、删除
* `Object.defineProperty`如果要劫持嵌套层级比较深的对象属性，就必须把每一层的数据都变成响应式的
**注意**，Proxy并不能监听到内部嵌套层级对象的变化，Vue是在getter中递归处理响应式对象，这样做的好处是，只有真正访问到的对象才会变成响应式的，而不是无脑递归

Proxy不支持ise
### 编译优化
* 标记动态节点
* slot的编译优化、时间监听函数的缓存优化，并在运行时重写了diff算法

### Composition Api
* Composition API可以将某个逻辑的关注点相关代码集中放到一个函数中，而不是分散的
* 优化逻辑复用

### 单文件组件`<script setup>`
[<script setup>](https://v3.cn.vuejs.org/api/sfc-script-setup.html)可以减少样板代码是使用
* 更少的样板内容，更简洁的代码。
* 能够使用纯 Typescript 声明 props 和抛出事件。
* 更好的运行时性能 (其模板会被编译成与其同一作用域的渲染函数，没有任何的中间代理)。
* 更好的 IDE 类型推断性能 (减少语言服务器从代码中抽离类型的工作)。

## 目录
* [Vue.js核心组件实现](./Component.md)
* [CompositionAPI]()