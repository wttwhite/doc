### 防抖节流

函数默认执行频率太高

#### 1.防抖

触发事件后在 n 秒内函数只能执行一次，如果在 n 秒内又触发了事件，则会重新计算函数执行时间。 （重点是清空计时）

##### 1.1 核心代码

```javascript
debounce = function (func, wait) {
    let timeout
    return function () {
        clearTimeout(timeout)
        timeout = setTimeout(func, wait)
    }
}
```
##### 1.2 this指向

不做处理的调用this会指向window（非vue环境）
```javascript
debounce = function (func, wait) {
    let timeout
    function debounced () {
        if (timeout) clearTimeout(timeout)
        timeout = setTimeout(() => {
            func.apply(this, arguments)
        }, wait)
    }
    return debounced
}
const box = document.getElementById('box')
function mouseMove () {
    console.log('this', this)
}
box.onmousemove = debounce(mouseMove, 500)
```
**注：**
- debounced如果是箭头函数，this指向window，arguments是debounce函数的；
- debounce和debounced都是箭头函数，arguments报错
- mouseMove函数如果是箭头函数，this也指向window；

##### 1.3 扩展功能
- 非立即执行： 非立即执行版的意思是触发事件后函数不会立即执行，而是在 n 秒后执行，如果在 n 秒内又触发了事件，则会重新计算函数执行时间。
- 立即执行版 ： 触发事件后函数会立即执行，然后 n 秒内不触发事件才能继续执行函数的效果。
- 结合 —— 增加第三个参数immediate控制方式

```javascript
const debounceAll = (func, wait, immediate) => { 
    let timeout, result 
    const debounced = function () { 
        if (timeout) clearTimeout(timeout) 
        if (immediate) { 
            timeout = setTimeout(() => { 
                timeout = null 
            }, wait) 
            if (!timeout) result = func.apply(this, arguments) 
        } else { 
            timeout = setTimeout(() => { result = func.apply(this, arguments) }, wait) 
        } 
        return result 
    } 
    return debounce 
}
```

##### 1.4 取消功能
```javascript
debounced.cancel = () => {
    if (timeout) clearTimeout(timeout)
    timeout = null
}
```

##### 1.5 返回值
真没看出来哪里可以接debounced函数的return
```javascript
debounced.result = () => {
    return result
}
// lodash 
function flush() {
    return timerId === undefined ? result : trailingEdge(now());
}
// underscore
// debounced 函数内 return result
```

##### 1.6 应用场景
1. scroll事件滚动触发
2. 输入框实时搜索
3. 按钮提交事件
4. 浏览器窗口缩放(resize)

#### 2. 节流
连续触发事件但是在 n 秒中只执行一次函数 （ 稀释执行频率 ）
##### 2.1 时间戳
```javascript
const now = Date.now || function () {
    return new Date().getTime()
}
// 时间戳 --- 立即执行
const throttle1 = (func, wait) => {
    let prev = 0
    return function () {
        let _now = now()
        if (_now - prev > wait) {
            func.apply(this, arguments)
            prev = _now
        }
    }
}
```
##### 2.2 定时器
// 定时器 --- 延后执行
```javascript
const throttle2 = (func, wait) => {
    let timeout
    return function () {
        if (!timeout) {
            timeout = setTimeout(() => {
                func.apply(this, arguments)
                timeout = null
            }, wait)
        }
    }
}
```
结合 --- 刚开始执行，最后也执行
```javascript
const throttle3 = (func, wait) => {
    let timeout; let prev = 0
    return function () {
        let _now = now()
        if (_now - prev > wait) {
            if (timeout) {
                clearTimeout(timeout)
                timeout = null
            }
            func.apply(this, arguments)
            prev = _now
        } else if (!timeout) {
            timeout = setTimeout(() => {
                func.apply(this, arguments)
                prev = now()
                timeout = null
            }, wait)
        }
    }
}
```
##### 2.3 传参option
```javascript
{
    leading: false // 禁用第一次首先执行
    trailing: false // 禁用最后一次执行
}
const throttle4 = (func, wait, options) => {
    let timeout; let prev = 0
    if (!options) options = {}
    return function () {
        let _now = now()
        // 一开始不执行
        if (!prev && options.leading === false) {
            prev = _now
        }
        if (_now - prev > wait) {
            if (timeout) {
                clearTimeout(timeout)
                timeout = null
            }
            func.apply(this, arguments)
            prev = _now
        } else if (!timeout && options.trailing !== false) { // 最后一次不执行
            timeout = setTimeout(() => {
                func.apply(this, arguments)
                prev = options.leading === false ? 0 : now()
                timeout = null
            }, wait)
        }
    }
}
```
##### 2.4 应用场景
1. DOM元素拖拽
2. 鼠标移动
3. scroll事件滚动触发