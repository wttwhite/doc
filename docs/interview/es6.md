### 1. var let const 
var
1. 变量声明提升 var  let 报错
2. 重复定义，变量覆盖 var  let 不能重复定义
3. 没有块级作用域 var
   
const 
1. 声明之后必须赋值
2. 值不能被修改
3. 支持let其他特性

### 2. promise
1. 构造函数同步执行
2. .then方法异步执行
```javascript
const promise = new Promise((resolve, reject) => {
  console.log(1)
  resolve(3)
  console.log(2)
})
promise.then(res => {
  console.log(res)
})
console.log(4)
```
1 2 4 3
