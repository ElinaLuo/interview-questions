# 1.性能优化
全局搜索【性能优化】
# 2.vue virtual dom diff算法
全局搜索【vue diff算法原理实现】

# 3.vue响应式实现原理
考点：Object.defineProperty get收集依赖 set通知依赖更新；发布订阅模式

# 4.为什么需要virtual dom？vnode构成
虚拟dom可以以最小的代价来更新dom，因为操作DOM的代价仍旧是昂贵的，频繁操作还是会出现页面卡顿，影响用户的体验，特别是复杂的页面，大面积的重绘直接降低用户体验

# 5.compute响应式是如何实现的？
通过观察者模式，当调用方法的时候，将此观察者收集起来，下次修改数据的时候，通知观察者更新

# 6.Koa中间件
全局搜索【koa中间件实现原理】

# 7.手撕Promise.all
```
/**
 * @description 手撕Promise.all
 */
Promise.myAll = function (q) {
    const length = q.length
    let count = 0
    let result = []
    return new Promise((resolve, reject) => {
        for(let i = 0; i < length; i++) {
            q[i].then(res => {
                count++
                result[i] = res
                if(count === length) {
                    resolve(result)
                }
            }).catch(err => {
                reject(err)
            })
        }
    })
}
function fn1(time) {
    return new Promise(resolve => {
        setTimeout(() => {
            resolve(time)
        }, time);
    })
}
Promise.myAll([
    fn1(100),
    fn1(200),
    fn1(300)
]).then(res => {
    console.log(res);// [100, 200, 300]
})
```


# 8.async内部实现
是generator的语法糖，但是在它的基础上做了如下改造：
- 内置执行器，generator需要依赖co
- 更广的适用性，await后面可接原始类型，如number，boolean
- 返回值是Promise，generator返回值是Iterator

# 9.await 与 yield的不同
co模块约定，yield命令后面只能是 Thunk 函数或 Promise 对象(实际yield是可以带原始类型的，比如yield 1)
而await命令后面，可以是 Promise 对象和原始类型的值（数值、字符串和布尔值，但这时会自动转成立即 resolved 的 Promise 对象）

# 10.[1, 7, -10, 4, 12, 9, -12, 20]找出相加和最大的数组片段

# 11.内存泄露
- 意外的全局变量: 无法被回收
- 定时器: 未被正确关闭，导致所引用的外部变量无法被释放
- 事件监听: 没有正确销毁 (低版本浏览器可能出现)
- 闭包: 会导致父级中的变量无法被释放
- dom 引用: dom 元素被删除时，内存中的引用未被正确清空

# 12.编程题
补充下面缺少的代码，条件：实现最多有2个异步任务在执行
```
class Scheduler {
  /**
  * @param {function}
  * @return {Promise}
   */
  add(promiseCreator) {
    //...
  }

  //...
}
//最多有2个异步任务在执行
const timeout = time => () => new Promise(resolve => {
  setTimeout(resolve, time)
})


const scheduler = new Scheduler();

const addSchedule = (time, order) => {
  scheduler.add(timeout(time)).then(() => {
    console.log(order)
  })
}



addSchedule(1000, 1)
addSchedule(500, 2)
addSchedule(300, 3)
addSchedule(400, 4)

// 2, 3, 1, 4
```

答案：
```
const MAX = 2

class Scheduler {
  constructor() {
    this.tasks = []
    this.count = 0
  }
  /**
  * @param {function}
  * @return {Promise}
   */
  add(promiseCreator) {
    return new Promise(resolve => {
      this.tasks.push(() => {
        return promiseCreator().then(resolve)
      })

      this.run();
    })
  }

  run() {
    if (this.count < MAX && this.tasks.length > 0) {
      this.count += 1;
      const task = this.tasks.shift();
      task().then(() => this.done())
    }
  }

  done() {
    this.count -= 1;
    this.run();
  }
}
//最多有2个异步任务在执行

const timeout = time => () => new Promise(resolve => {
  setTimeout(resolve, time)
})


const scheduler = new Scheduler();

const addSchedule = (time, order) => {
  scheduler.add(timeout(time)).then(() => {
    console.log(order)
  })
}



addSchedule(1000, 1)
addSchedule(500, 2)
addSchedule(300, 3)
addSchedule(400, 4)

// 2, 3, 1, 4

```
