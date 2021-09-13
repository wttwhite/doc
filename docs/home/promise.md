### promise

#### 1. 区别实例对象与函数对象

- 实例对象：new函数产生的对象，称为实例对象，简称对象
- 函数对象：将函数作为对象使用时，简称为函数对象

```javascript
function Fn(){}
const fn = new Fn() -> Fn是构造函数，fn是实例对象
Fn.prototype -> 函数对象
```

#### 2. 宏队列与微队列

- 宏队列：dom事件回调、ajax 回调、定时器回调
- 微队列：promise回调、mutation（new MutationObserver(callback)观察DOM树结构发生变化时,做出相应处理的API）

**js执行时会区别这2个队列**

1. Js引擎首先必须先执行所有的初始化同步任务代码
2. 每次准备取出一个宏任务执行前都要将所有的微任务一个一个取出执行

```javascript
setTimeout(() => { // 立即放入宏队列
  console.log('settimeout 1')
  Promise.resolve(1).then(() => { // 立即放入微队列
    console.log('promise 2')
  })
})
setTimeout(() => { // 立即放入宏队列
  console.log('settimeout 2')
})
Promise.resolve(1).then(() => { // 立即放入微队列
  console.log('promise 1')
})
// promise 1; settimeout 1; promise 2; settimeout 2
```

#### 面试题

```javascript
setTimeout(() => { 
  console.log(1)
})
new Promise((resolve) => {
  console.log(2)
  resolve()
}).then(() => {
  console.log(3)
}).then(() => {
  console.log(4)
})
console.log(5)
// 2 5 3 4 1
宏队列[1]
微队列[3]
3执行之后，微队列又放入4，继续执行4，最后执行1
```

```javascript
const first = () => new Promise((resolve, reject) => {
  console.log(3) 
  let p = new Promise((resolve, reject) => {
    console.log(7)
    setTimeout(() => {
      console.log(5)
      resolve(6) // 状态已经改变
    })
    resolve(1) // 立马成功，then 放入微队列
  })
  resolve(2)
	p.then(arg => {
    console.log(arg)
  })
})
first().then(arg => {
  console.log(arg)
})
console.log(4)
// 3 7 4 1 2 5
```

```javascript
setTimeout(() => {
  console.log(0)
})
new Promise((resolve, reject) => {
  console.log(1)
  resolve()
}).then(() => {
  console.log(2)
  new Promise((resolve, reject) => {
    console.log(3)
    resolve()
  }).then(() => {
    console.log(4)
  }).then(() => {
    console.log(5)
	})
}).then(() => {
  console.log(6)
})
new Promise((resolve, reject) => {
  console.log(7)
  resolve()
}).then(() => {
	console.log(8)
})
// 1 7 2 3 8 4 5 6 0
// 1 7 2 3 8 4 6 5 0
```





