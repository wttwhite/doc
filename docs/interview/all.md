
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

监听滚动条滚动事件

输入框实时搜索

函数默认执行频率太高

防抖

 触发事件后在 n 秒内函数只能执行一次，如果在 n 秒内又触发了事件，则会重新计算函数执行时间。 （重点是清空计时）

- 非立即执行： 非立即执行版的意思是触发事件后函数不会立即执行，而是在 n 秒后执行，如果在 n 秒内又触发了事件，则会重新计算函数执行时间。 
- 立即执行版 ： 触发事件后函数会立即执行，然后 n 秒内不触发事件才能继续执行函数的效果。 
- 结合 —— 增加第三个参数immediate控制方式

节流

 连续触发事件但是在 n 秒中只执行一次函数 （ 稀释执行频率 ）