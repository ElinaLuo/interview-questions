# 1.性能优化
## 一.加载优化（资源下载、资源体积）
### 1.DNS优化
- 使用dns-prefetch域名预解析来减少DNS解析时间
- refetch加载未来可能需要的资源

### 2.资源使用CDN
- 访问加速（多节点）
- 负载均衡

### 3.升级到HTTP2
- 头部压缩
- 二进制分帧
- 多路复用，同个域名只需要占用一个 TCP 连接
- 支持服务器推送
### 4.Gzip
Nginx开启Gzip压缩
### 5.HTTP缓存
- 强缓存，Cache-Control、Expires
- 协商缓存，Etag(If-None-atch)、last-modified(If-Modified-Since)
### 6.减少文件体积
- webpack
- tree-shaking移除未使用的代码
- UglifyJs压缩
- code-splitting，分离出vendor充分利用浏览器缓存/按需加载
- css去重
### 7.图片优化
- 雪碧图
- webpack url-loader，小图片使用base64
- webp
- 懒加载
## 二.渲染优化
- 内联首屏渲染所需的css, js
- SSR，html可直接渲染出首屏
- 非核心模块，异步加载
- preload调整资源加载顺序
## 三.用户体验优化
- 利用一些动画过渡效果，能有效减少用户对卡顿的感知
- 骨架屏，减少用户对白屏的感知

参考：
1.页面资源加载过程分析：
评估关键渲染路径：
https://developers.google.com/web/fundamentals/performance/critical-rendering-path/measure-crp?hl=zh-cn

分析关键渲染路径性能：
https://developers.google.com/web/fundamentals/performance/critical-rendering-path/analyzing-crp?hl=zh-cn

# 2.vue diff算法原理实现
1. 创建 dom 树
1. 树的diff，同层对比，输出patchs(listDiff/diffChildren/diffProps)
    - 没有新的节点，返回
    - 新的节点tagName与key不变， 对比props，继续递归遍历子树
        对比属性(对比新旧属性列表):
        - 旧属性是否存在与新属性列表中
        - 都存在的是否有变化
        - 是否出现旧列表中没有的新属性
    - tagName和key值变化了，则直接替换成新节点
1. 渲染差异
- 遍历patchs， 把需要更改的节点取出来
- 局部更新dom

# 3.koa中间件实现原理
洋葱模型，从外到内，再从内向外
https://juejin.im/post/5b9a23a45188255c9c751b07#heading-4

# 4.MVVM
MVVM 由以下三个内容组成
View：视图
Model：数据模型，也可以在Model中定义数据修改和操作的业务逻辑
ViewModel：作为桥梁负责沟通 View 和 Model，当视图变化时，触发数据更新，当数据变化时，触发视图更新
Vue.js就是一个MVVM框架，Vue 内部使用了 Object.defineProperty() 来实现双向绑定，通过这个函数可以监听到 set 和 get的事件。get方法用于收集依赖项，具体是视图Dom，set方法用于数据更新时，通知依赖项，具体是执行render方法来改变视图

# 5.双向绑定原理
双向绑定：当视图变化，数据会修改，当数据变化，视图会更新；当为一个input添加v-model指令时，这个值在Vue 内部使用了 Object.defineProperty() 对这个属性进行了重新定义，特别是重新定义了存取描述符，即set和get方法，当触发渲染方法时，get方法会收集依赖项（观察者），set方法用于数据更新时，通知依赖项，即执行render方法来改变视图，而v-model是:value和@input的语法糖，当用户输入时会触发input方法，会调用set方法，然后会触发视图更新，从而达到双向绑定的效果。总的来说，Vue实现双向绑定的核心就是Object.defineProperty
但是Object.defineProperty还是有缺陷的
只能对属性进行数据劫持，所以需要深度遍历整个对象
对于数组不能监听到数据的变化
所在Vue 3.0使用了Proxy替代了这个方法

# 6.Vue React对比

# 7.用户输入url到页面展示的过程

1. DNS 解析
1. TCP 三次握手
1. 发送请求，分析 url，设置请求报文(头，主体)
1. 服务器返回请求的文件 (html)
1. 浏览器渲染
    - HTML parser --> DOM Tree
        - 标记化算法，进行元素状态的标记
        - dom 树构建
    - CSS parser --> Style Tree
        - 解析 css 代码，生成样式树
    - attachment --> Render Tree
        - 结合 dom树 与 style树，生成渲染树
    - layout: 布局
    - GPU painting: 像素绘制页面