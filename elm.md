# vue渲染过程

<img src="https://p0.meituan.net/education/f41a481d7b68d0729fa6ac07151f8492144477.png">
<img src="https://p0.meituan.net/education/ecb1b75142d7040ccccbca6092ec9a8260975.jpg">

- new Vue，执行初始化
- 挂载$mount方法，通过自定义Render方法、template、el等生成Render函数
- 通过Watcher监听数据的变化
- 当数据发生变化时，Render函数执行生成VNode对象
- 通过patch方法，对比新旧VNode对象，通过DOM Diff算法，添加、修改、删除真正的DOM元素

# vue diff算法原理实现
创建 dom 树
树的diff，同层对比，输出patchs(listDiff/diffChildren/diffProps)
没有新的节点，返回
新的节点tagName与key不变， 对比props，继续递归遍历子树
对比属性(对比新旧属性列表):
旧属性是否存在与新属性列表中
都存在的是否有变化
是否出现旧列表中没有的新属性
tagName和key值变化了，则直接替换成新节点
渲染差异
遍历patchs， 把需要更改的节点取出来
局部更新dom


# mixin优缺点
优点：组件代码复用
缺点：Mixin是一种很灵活的代码复用方式，但把功能属性和方法导入，如果文件过多，会导致属性方法来源方面的不确定性

# 高阶组件
vue中没有高阶组件，在vue中是通过mixin来实现代码复用

# vue3.0有没有其它的新功能？
proxy替代Object.defineProperty

# webpack 工作原理、依赖关系图
初始化参数：从配置文件和 Shell 语句中读取与合并参数，得出最终的参数；
开始编译：用上一步得到的参数初始化 Compiler 对象，加载所有配置的插件，执行对象的 run 方法开始执行编译；
确定入口：根据配置中的 entry 找出所有的入口文件
编译模块：从入口文件出发，调用所有配置的 Loader 对模块进行翻译，再找出该模块依赖的模块，再递归本步骤直到所有入口依赖的文件都经过了本步骤的处理；
完成模块编译：在经过第4步使用 Loader 翻译完所有模块后，得到了每个模块被翻译后的最终内容以及它们之间的依赖关系；
输出资源：根据入口和模块之间的依赖关系，组装成一个个包含多个模块的 Chunk，再把每个 Chunk 转换成一个单独的文件加入到输出列表，这步是可以修改输出内容的最后机会；
输出完成：在确定好输出内容后，根据配置确定输出的路径和文件名，把文件内容写入到文件系统。 在以上过程中，webpack 会在特定的时间点广播出特定的事件，插件在监听到感兴趣的事件后会执行特定的逻辑，并且插件可以调用 webpack 提供的 API 改变 webpack 的运行结果。

# 性能优化
有道笔记搜索【性能优化】

# node事件循环
6个阶段：
1. timers：执行满足条件的setTimeout、setInterval回调。
1. I/O callbacks：是否有已完成的I/O操作的回调函数，来自上一轮的poll残留。
1. idle，prepare：可忽略
1. poll：等待还没完成的I/O事件，会因timers和超时时间等结束等待。
1. check：执行setImmediate的回调。
1. close callbacks：关闭所有的closing handles，一些onclose事件。

循环执行的过程：
1. 执行当前循环内的Timers Queue，执行并清空NextTick Queue，执行并清空Microtask Queue。
1. 执行当前循环内的I/O Queue，执行并清空NextTick Queue，执行并清空Microtask Queue。
1. 执行当前循环内的Check Queue，执行并清空NextTick Queue，执行并清空Microtask Queue。
1. 执行当前循环内的Close Queue，执行并清空NextTick Queue，执行并清空Microtask Queue。
1. 进入下轮循环。
process.nexTtick比promise 优先级高

# 用户输入url到页面展示的过程
有道笔记搜索【用户输入url到页面展示的过程】

# https加密过程
https://juejin.im/post/5a4f4884518825732b19a3ce

# 浏览器命中缓存的过程？
https://segmentfault.com/a/1190000017004307

# CDN缓存原理？
一般情况下，都会遵循http标准协议，缓存节点缓存的具体时间由 HTTP 响应头里面的 Cache-Control 和 Expires 响应头控制
https://juejin.im/post/5be3f486e51d45053d5c38ca#heading-6

# React与vue对比
有道搜索【Vue React对比】

# 了解的新技术
flutter、微服务











