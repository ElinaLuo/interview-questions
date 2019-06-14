# 1.js 实现异步的方式
function(cb)、promise、generator、async、setTimeout

# 2.vue中的emit是异步吗？
不是，同步的

# 3.promise理解
Promise 是异步编程的一种解决方案，采用链式调用的方式组织代码，比传统的回调函数层层嵌套的方式，代码上更加直观清晰。
两个特点：
a.对象的状态不受外界影响，有3种状态：pending（执行中）、Resolved（成功，又称Fulfilled）、rejected（拒绝）
b.一旦状态改变，就不会再变，任何时候都可以得到这个结果。Promise对象的状态改变，只有两种可能：Pending ==> Resolved 和 Pending ==> Rejected
缺点：
仍然不解决层层嵌套问题
当发生错误的时候，无法定位是哪个promise执行出错了

# 4.解释深拷贝和浅拷贝？深拷贝的方法？
浅拷贝：浅复制是对对象引用地址的复制
深拷贝：开辟新的栈，两个对象对应两个不同的地址，修改一个对象的属性，不会改变另一个对象的属性
浅拷贝的方法：Object.assign()
深拷贝的方法：$.extend()、lodash.cloneDeep()、JSON.parse(JSON.stringify(obj))

# 5.JSON.parse(JSON.stringify(obj))深拷贝的缺点？
undefined、function、正则表达式无法复制
```
var target = {
    a: 1,
    b: 2,
    c: null,
    d: undefined,
    e: {
      f: "f"
    },
    g: [1,2,3],
    h: /\d*/,
    hello: function() {
      console.log("Hello, world!");
    }
};
var copy = cloneObject(target);
console.log(copy);
// 深拷贝
function deepCopy(obj) {
  var clone = {};
  for(var i in obj) {
      if(obj[i] != null &&  typeof(obj[i]) == "object")
          clone[i] = cloneObject(obj[i]);
      else
          clone[i] = obj[i];
  }
  return clone;
}
```


# 6.webpack内部实现
webpack是一个模块打包工具
entry：入口文件
loader：针对不同文件经过对应的loader处理，比如style-loader, babel-loader等
plugin：执行的不同生命周期会调用hook执行plugin

# 7.Vue-SSR理解
一套同构代码，利用webpack两份打包配置，webpack-client-config生成的client bundle用于entry-client.js供浏览器渲染，服务端生成server bundle用于entry-server.js供服务端渲染调用


# 8.vue优点
1.数据驱动框架相比手动更新DOM的框架，对开发者更友好，开发效率更高
2.入门门槛低，上手快
3.轻量，包体积小

# 9.如何实现按需加载
require.ensure、import().then

# 10.ES6 模块与 CommonJS 模块的差异
CommonJS 模块输出的是一个值的拷贝，ES6 模块输出的是值的引用
CommonJS 模块是运行时加载，ES6 模块是编译时输出接口（esm不支持dynamic import）

# 11.AMD如何定义和引用模块？
define([], () => {})，require([], () => {})