# 1.盒模型
w3c 盒模型
IE 盒模型
box-sizing
# 2.垂直居中的实现方法？
absolute + transform
flex align-item
height = line-height
# 3.flex
# 4.如何用flex实现三列，中间等宽，两边自适应
``` html
<div class="container">
  <div class="left"></div>
  <div class="center"></div>
  <div class="right"></div>
</div>

// css
.container {
  display: flex;
  width: 500px;
}
.container div {
  height: 100px;
  border: 1px solid #000;
}
.left, .right {
  flex: 1;// 相当于flex-grow: 1(自动拉伸)
}
.center {
  width: 100px;
}
```

# 5.如何阻止form默认提交事件？
方法1：在button的onclick function最后执行的函数最后加上e.preventDefault
方法2：在form的onsubmit上指定return false
```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <script>
        // 方法1
        function func1(event){
            event.preventDefault();
        }
    </script>
</head>
<body>
    <form action="test.html" onsubmit="return false;">
        <input type="submit" value="button" onclick="func1(event)" />
    </form>
</body>
</html>
```


# 6.事件触发经历哪些阶段？
捕获->目标->冒泡
实例：a, b, c三个div如何设计点击事件，使得输出a c b？
```html
<div id="a">
    <div id="b">
        <div id="c">
        </div>
    </div>
</div>
<script>
document.getElementById('a').addEventListener('click', function() {
    console.log('a')
}, true)// 捕获
document.getElementById('b').addEventListener('click', function() {
    console.log('b')
}, false)// 冒泡
document.getElementById('c').addEventListener('click', function() {
    console.log('c')
})// 捕获/冒泡都可以
</script>
```

# 7.考察原型链
a.__proto__ = A.prototype
let a = {
  x: 'a'
}
let b = {
  x: 'b'
}

b.__proto__ = a
console.log(b.x)// b
delete b.x
console.log(b.x)// a
delete b.x
console.log(b.x)// a delete只能删除自身对象上的属性，而不能删除原型链上的属性



# 8.手机端点击延迟300ms如何解决？
直接使用@touchend替换@click
使用fastclick.js（具体实现：在检测到touchend事件的时候，会通过 DOM 自定义事件立即触发一个模拟click事件，并把浏览器在 300 毫秒之后真正触发的click事件阻止掉）
# 9.实现订阅发布
```
// 发布订阅模式
class Publisher {
  constructor() {
    this.quene = []
  }
  add(d) {
    this.quene.push(d)
  }
  update() {
    this.quene.forEach(d => {
      d.notify()
    })
  }
}
class Subscribe {
  constructor(cb) {
    this.cb = cb
  }
  notify() {
    this.cb()
  }
}

const p = new Publisher()
const s1 = new Subscribe(() => {
  console.log('s1 被通知到了')
})
const s2 = new Subscribe(() => {
  console.log('s2 被通知到了')
})
p.add(s1)
p.add(s2)
p.update()
```


# 10.arrow函数与常规函数的不同点
函数体内的this对象，就是定义时所在的对象，而不是使用时所在的对象。
不可以当作构造函数，也就是说，不可以使用new命令，否则会抛出一个错误。
不可以使用arguments对象，该对象在函数体内不存在。如果要用，可以用 rest 参数代替。
不可以使用yield命令，因此箭头函数不能用作 Generator 函数。

# 11.webpack tree-shaking实现
tree-shaking依赖了ES6 module静态结构特性，移除javascript上下文中的未引用的代码
ES6 module特点：
只能作为模块顶层的语句出现
import 的模块名只能是字符串常量
import binding 是 immutable的
ES6模块依赖关系是确定的，和运行时的状态无关，可以进行可靠的静态分析，这就是tree-shaking的基础。

# 12.为什么要使用流？
主要为了处理大文件，如果一次性读取一个大的文件，会导致内存被大量占用，而无法快速处理其它任务
使用流

# 13.浏览器渲染过程
处理HTML标记数据并生成DOM树
处理CSS标记数据并生成CSSOM树
将DOM树与CSSOM树合并在一起生成渲染树
遍历渲染树开始布局，计算每个节点的位置信息
将每个节点绘制到屏幕
https://juejin.im/post/59d489156fb9a00a571d6509

# 14.watch computed如何实现响应式以及区别
通过观察者模式，当被观察者发送变化，则会触发观察者更新，即调用render生成vnode，然后update渲染

# 15.数据库第三范式
第一范式（1NF）：要求各列原子性，不能再分
第二范式（2NF）：在1NF基础上，要求属性完全依赖主键
第三范式（3NF）：在2NF基础上，要求非主键外的所有字段必须互不依赖，即数据不冗余

# 16.TCP UDP区别
1.TCP是面向连接（3次握手，4次挥手）的通讯方式，而UDP是一个非连接的协议，即传输数据之前源端和终端不建立连接
2.TCP包头为20字节，UDP信息包标题很短，只有8个字节，相对于TCP的20个字节信息包的额外开销很小
3.UDP使用尽最大努力交付，即不保证可靠交付，而TCP保证数据正确性，相比UDP更可靠性
4.TCP保证数据顺序，UDP不保证

# 17.webpack tree shaking实例
若A文件有a b两个方法，若引用了a但未引用b，那么最后打包会把b打包吗？
如果是方法，那么不会删除b，如果A导出了a和b两个模块，那么最终b会被删除，但开发模式下不会删掉，只有生产环境才会删掉




