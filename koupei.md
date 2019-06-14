# 1.es6如何兼容低版本浏览器
@babel/preset-env + useBuiltIns: usage
@babel/polyfill（污染全局变量，会导入实际不需要的包，且不适合library，不推荐）

# 2.let var 区别 
let是块级作用域
var作用域提升
全局声明的var会被挂载到window下，而let不会
```
function f(){
console.log(a)// undefined
var a = 2
console.log(a)// 2
}
f()
```


# 3.如何用原生js方法给Dom添加class
```
const el = document.getElementById('.myDom')
el.classList.add('xxx')
el.classList.remove('xxx')
```


# 4.正则表达式在js下有哪些方法
```
str.match(regexp)
str.replace(regexp|substr, newSubStr|function)
str.search(regexp)
str.split([separator[, limit]])
regexObj.test(str)
regexObj.exec(str)
```
实践：用正则表达式，将"2019-05-01"转成"2019年05月01日"
console.log("2019-05-01".replace(/(\d*)-(\d*)-(\d*)/, '$1年$2月$3日'))


# 5判断数组
```
const arr = [1,2]
console.log(Object.prototype.toString.call(arr) == '[object Array]')// true
console.log(Array.isArray(arr))// true
// 不可靠，原型链有可能被修改
console.log(arr instanceof Array)// true
// 不可靠，constructor有可能被修改
console.log(arr.constructor == Array)// true
```

# 6.数组去重
Array.from(new Set([1,2,3,2,3]))// [1, 2, 3]
indexOf + 一层for循环
Map + 一层for循环

# 7.跨域
页面间跨域：postmessage、window.name
请求跨域：jsonp、cors、img
# 8.vue
# 9.mvvm理解
有道笔记搜索MVVM
# 10.双向绑定原理
有道笔记搜索 双向绑定原理
# 11.单向数据流原理

# 12.箭头函数中this能不能改
不能改

# 13.怎么改变 this 的指向
使用 ES6 的箭头函数
在函数内部使用 _this = this
使用 apply、call、bind
new 实例化一个对象

# 14.bind与apply call区别
bind内部可以通过apply、call来实现，不同的是bind返回一个函数，而apply、call会立即执行

