
### 输入URL到浏览器显现给用户经过了什么过程
- 用户输入URL，浏览器获取URL
- 浏览器进行DNS解析（直接输入IP地址则跳过该步骤）
- 浏览器发起HTTP请求
- 请求到达传输层，TCP协议通过三次握手来保证传输过程的可靠
- 到达网络层，网络层通过ARP寻址得到接收方的Mac地址，IP协议把数据包传送给接收方
- 数据到达数据链路层，请求阶段完成
- 接收方收到HTTP请求之后，进行请求文件资源并响应报文
- 发送方收到响应报文，如果请求成功，则接受返回的资源进行页面渲染
- 内容解析
- HTML解析器将HTML解析成DOM树
- CSS解析器将DOM中各元素对象加入样式信息
- JS引擎解析JS代码并把逻辑应用到布局中
- 构建一棵render tree
- **重排**：当render tree中任意节点的尺寸大小发生改变，render tree都会重新布局
- **重绘**：render tree中任意元素的属性样式发生改变，render tree都会重新画
### TCP/IP
#### 三次握手
#### 四次挥手
### 描述cookie、sessionStorage、localStorage的区别
- 保存位置
- 存储大小
- 有效时间

防抖节流

函数默认执行频率太高

防抖

 触发事件后在 n 秒内函数只能执行一次，如果在 n 秒内又触发了事件，则会重新计算函数执行时间。 （重点是清空计时）

核心

    debounce = function (func, wait) {
        let timeout
        return function () {
            clearTimeout(timeout)
            timeout = setTimeout(func, wait)
        }

this指向

不做处理的调用this会指向window（非vue环境）

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

注：

1. debounced如果是箭头函数，this指向window，arguments是debounce函数的；
2. debounce和debounced都是箭头函数，arguments报错
3. mouseMove函数如果是箭头函数，this也指向window；

扩展功能

- 非立即执行： 非立即执行版的意思是触发事件后函数不会立即执行，而是在 n 秒后执行，如果在 n 秒内又触发了事件，则会重新计算函数执行时间。 
- 立即执行版 ： 触发事件后函数会立即执行，然后 n 秒内不触发事件才能继续执行函数的效果。 
- 结合 —— 增加第三个参数immediate控制方式

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
                timeout = setTimeout(() => {
                    result = func.apply(this, arguments)
                }, wait)
            }
            return result
        }
        return debounce
    }

取消功能

    debounced.cancel = () => {
        if (timeout) clearTimeout(timeout)
        timeout = null
    }
    

返回值

    // 真没看出来哪里可以接debounced函数的return
    debounced.result = () => {
        return result
    }
    // lodash 
    function flush() {
        return timerId === undefined ? result : trailingEdge(now());
    }
    // underscore
    // debounced 函数内 return result

应用场景

1. scroll事件滚动触发
2. 输入框实时搜索
3. 按钮提交事件
4. 浏览器窗口缩放(resize)

节流

 连续触发事件但是在 n 秒中只执行一次函数 （ 稀释执行频率 ）

时间戳

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

定时器

    // 定时器 --- 延后执行
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

结合 --- 刚开始执行，最后也执行

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

传参option

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



应用场景

1. DOM元素拖拽
2. 鼠标移动
3. scroll事件滚动触发

