# 1.实现fetch的超时机制
```
/**
 * @description 模拟timeout
 */
const _fetch = (function (fetch) {
  return function(url, options) {
    let timeoutPromise = new Promise((resolve, reject) => {
      setTimeout(reject, options.timeout, 'it is timeout!')
    })
    let promise = Promise.race([
      fetch(url, options),
      timeoutPromise
    ])
    return promise
  }
})(fetch)

var url = 'http://m.51ping.com/beautytry/zerohelp/trialturn?channel=16'
const p = _fetch(url, {
  timeout: 1000
})

p.then(res => {
  console.log(res)
  res.json().then(data => console.log(data))
}, err => {
  console.error(err)
})
```

# 2.实现一个组件，它有一个props，类型为数字，当数字变化后，组件会实现一个数字的变化过程
举例：如果首次传1，后来传10，那么页面会展示1 2 3...10的一个变化
核心实现就是通过watch props + setTimeout动态更新
```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <div id="app">
        <input type="text" v-model="origin">
        <div>{{ current }}</div>
    </div>

    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script>
        new Vue({
            el: '#app',
            data() {
                return {
                    origin: 1,
                    current: 1
                }
            },
            mounted() {
                this.current = this.origin
            },
            methods: {
                change() {
                    if(this.current != this.origin) {
                        this.origin > this.current ? this.current++ : this.current--
                        setTimeout(this.change.bind(this), 50)
                    }
                }
            },
            watch: {
                origin: function(oldVal, newVal) {
                    if(newVal !== oldVal) {
                        this.change()
                    }
                }
            }
        })
    </script>
</body>
</html>
```


# 3.讲讲js的模块化，以及对比
commonjs、AMD（requireJs）、ES Module

# 4.讲讲字符集
ASCII、Unicode（包含UTF-32、UTF-16和 UTF-8）、GBK等

# 5.有了解树吗？具体应用树的栗子
二叉树、红黑树、B+树
栗子：磁盘文件、html、
