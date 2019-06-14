# 1.MVVM理解
MVVM 由以下三个内容组成
View：视图
Model：数据模型，也可以在Model中定义数据修改和操作的业务逻辑
ViewModel：作为桥梁负责沟通 View 和 Model，当视图变化时，触发数据更新，当数据变化时，触发视图更新
Vue.js就是一个MVVM框架，Vue 内部使用了 Object.defineProperty() 来实现双向绑定，通过这个函数可以监听到 set 和 get的事件。get方法用于收集依赖项，具体是视图Dom，set方法用于数据更新时，通知依赖项，具体是执行render方法来改变视图
# 2.vue双向绑定理解
双向绑定：当视图变化，数据会修改，当数据变化，视图会更新；当为一个input添加v-model指令时，这个值在Vue 内部使用了 Object.defineProperty() 对这个属性进行了重新定义，特别是重新定义了存取描述符，即set和get方法，当触发渲染方法时，get方法会收集依赖项（观察者），set方法用于数据更新时，通知依赖项，即执行render方法来改变视图，而v-model是:value和@input的语法糖，当用户输入时会触发input方法，会调用set方法，然后会触发视图更新，从而达到双向绑定的效果。总的来说，Vue实现双向绑定的核心就是Object.defineProperty
但是Object.defineProperty还是有缺陷的
只能对属性进行数据劫持，所以需要深度遍历整个对象
对于数组不能监听到数据的变化
所在Vue 3.0使用了Proxy替代了这个方法
# 3.vue react区别
有道搜索【Vue React对比】

# 4.koa中间件实现原理（洋葱模型）
洋葱模型，从外到内，再从内向外
https://juejin.im/post/5b9a23a45188255c9c751b07#heading-4

# 5.node异步处理
异步编程包含以下几种形式：
callback function
promise
generator function (co)
async await function

# 6.co 与 generator 关系
co是generator的执行迭代器，在ES2017的async替代了co+generator
# 7.async 与 generator 区别
都用于异步编程，但async相当于co+generator，它可以自执行
