### axios
#### 1. 常见的响应状态码
- 200 请求成功
- 201 已创建，成功请求并创建了新的资源
- 401 未授权/请求要求用户的身份认证
- 404 not found
- 500 服务器内部错误

#### 2. API的分类
1. REST API： restful
    - 发送请求进行CRUD哪个操作由请求方式来决定
    - 同一个请求路径可以进行多个操作
    - 请求方式会用到GET/POST/PUT/DELETE
2. 非REST API： restless
    - 请求方式不决定请求的CRUD操作
    - 一个请求路径只对应一个操作
    - 一般只有GET/POST


#### 3. 使用json-server搭建REST API
懒，不想写

#### 4. 区别一般http请求与ajax请求
- ajax请求是一种特别的http请求
- 对服务器来说，没有任何区别，区别在浏览器
- 浏览器端发请求，只XHR或fetch发出的才是ajax请求，其他所有的都是非ajax请求
- 浏览器端接收到响应
    - 一般请求：浏览器一般会直接显示响应体数据，也就是我们常说的刷新/跳转页面
    - ajax请求：浏览器不会对界面进行任何更新操作，只是调用监视的回调函数并传入响应相关数据


#### 5. XHR API
1. XMLHttpRequest(): 创建XHR对象的构造函数
2. status：响应状态码值，200，404
3. statusText：响应状态文本
4. readyState：标识请求状态的只读属性
    - 0: 初始
    - 1: open()之后
    - 2: send()之后
    - 3: 请求中
    - 4: 请求完成
5. onreadystatechange：绑定readyState改变的监听
6. responseType：指定响应数据类型，如果是json，得到响应后自动解析响应体数据
7. response：响应体数据，类型取决于responseType的指定
8. timeout：指定请求超时时间，默认为0代表没有限制
9. ontimeout：绑定超时的监听
10. onerror：绑定请求网络错误的监听
11. open()：初始化一个请求，参数为：(method, url, async)
12. send(data)：发送请求
13. abort()：请求中断
14. getResponseHeader(name)：获取指定名称的响应头值
15. getAllResponseHeaders()：获取所有响应头组成的字符串
16. setRequestHeader(name, value)：设置请求头

#### 6. XHR的ajax封装(简单版axios)
特点：
1. 函数的返回值为promise，成功的结果为response，异常的结果为error
2. 能处理多种类型的请求：GET/POST/PUT/DELETE
3. 函数的参数为一个配置对象 `{url,method,params, data}`
4. 响应json数据自动解析为js

```javascript
function axios({
    url,
    method = 'GET',
    params = {},
    data = {}
}) {
    // 返回一个promise对象
    return new Promise((resolve, reject) => {
        // 执行异步ajax请求，创建XHR对象
        const request = new XMLHttpRequest()
        // 打开链接（初始化请求，没有请求）
        request.open(method, url, true)
        // 发送请求
        request.send()
    })
}
function test() {
    axios({
        url: 'http://localhost:3000/get'
    })
}
test()
```

