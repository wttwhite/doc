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


#### 1. promise 解决的问题

回调地狱

缺点：

1. 无法中途取消promise
2. 如果不设置回调函数，promise内部抛出的错误，不会反应到外部
3. 当处于pending时，无法得知当前发展到哪一阶段（刚刚开始还是即将完成）

#### 2. 基本规范

- 三种状态:  pending、fulfilled、rejected
- 状态只能从等待到已完成或已拒绝，不可逆
- then方法接受一个成功的回调和一个失败的回调
- then方法返回promise，可链式调用

#### 3. 基本api

- Promise.resolve()
- Promise.reject()
- Promise.all()：参数可以不是数组，但必须有iterator接口；全部变为resolve或遇到第一个reject时调用then； 同时开始、并行执行；
- Promise.race()：只要有一个resolve或者reject就会调用then；后面的promise对象还是会继续执行的；
- Promise.prototype.then()
- Promise.prototype.catch()

##### 3.1 catch

promise对象的错误具有"冒泡"性质，会一直向后传递，直到被捕获为止。也就是说，错误总会被下一个catch语句捕获

有了then里面的第二个函数捕获错误，为什么还要catch

- then的第二个函数并不能捕获第一个函数参数抛出的错误，then针对的是promise对象抛出的错误

##### 3.2 resolve 

可以将现有对象转为promise对象

该函数的参数四种情况：

1. 参数是一个promise实例， 直接返回实例
2. 参数是一个thenable对象（一个具有.then方法的对象），会将其转为promise对象，并立即执行then方法
3. 参数是其他基础类型，返回一个新的promise对象，并且状态resolved； `Promise.resolve(1)`
4. 不带任何参数，直接返回状态为resolved的promise对象

##### 3.3 reject

 返回一个新的 Promise 实例，该实例的状态为rejected 

##### 3.4 all

Promise.all方法用于将多个Promise实例，包装成一个新的Promise实例。如果传入的不是不是Promise对象就会调用Promise.reslove()方法将其转换成Promise实例。

#### 4. 基本使用

```javascript
function getUrl(url) {
    return new Promise((resolve, reject) => {
        const req = new XMLHttpRequest()
        req.open('GET', url, true)
        req.onload = function () {
            if (req.status === 200) {
                resolve(req.statusText)
            } else {
                reject(new Error(req.statusText))
            }
        }
        req.onerror = function () {
            reject(new Error(req.statusText))
        }
        req.send()
    })
}
getUrl('https://www.jianshu.com/p/d731c2b4c10a').then(res => {
    console.log('res', res)
}).catch(err => {
    console.log('err', err)
})
```

#### 5.promise只能进行异步操作?

 因为同步调用和异步调用同时存在容易导致一些混乱。 调用先后顺序不可控

 **为了解决这个问题，我们可以选择统一使用异步调用的方式。** 

#### 6. 实现

```jsx
 _this.onResolvedCallback = [] // Promise resolve时的回调函数集，因为在Promise结束之前有可能有多个回调添加到它上面
```

```jsx
 // 根据标准，如果then的参数不是function，则我们需要忽略它，此处以如下方式处理   实参留空 且让值可以穿透到后面
  onResolved = typeof onResolved === 'function' ? onResolved : function(value) {return value;}
```

https://blog.csdn.net/my_new_way/article/details/104730105



