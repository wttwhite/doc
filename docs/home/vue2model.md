- 发布订阅者模式
- 数据劫持

#### 简单实现发布订阅
```javascript
const Dep = {
    list: [],
    listen: function (key, fn) {
      (this.list[key] || (this.list[key] = [])) && this.list[key].push(fn)
    },
    trigger: function () {
      const key = Array.prototype.shift.call(arguments)
      const fns = this.list[key] || []
      fns.length && fns.forEach(fn => {
        fn.apply(this, arguments)
      })
    }
  }
```
#### 简单实现数据劫持
```javascript
function demo (obj, key, htmlId ) {
  let value = ''
  Object.defineProperty(obj, key, {
    get: function () {
      return value
    },
    set: function (val) {
      value = val
      // 发布数据变更事件
      Dep.trigger(key, val)
    }
  })
  // 劫持数据，订阅事件
  Dep.listen(key, function(val) {
    console.log('objobjobj' , obj)
    document.getElementById(htmlId).innerHTML = val
  })
}
let obj = {}
demo(obj, 'demo', 'demo1')
```
#### vue具体是怎么做的

#### 类似vue中连续多次修改响应式数据但只会触发一次更新
```javascript
let obj = {
      a: 1
    }
    let value = obj.a
    Object.defineProperty(obj, 'a', {
      get () {
        // console.log('value', value)
        // effect()
        return value 
      },
      set (val) {
        // console.log('val', val)
        effect()
        value = val
        return val
      }
    })
    const jobQueue = new Set()
    function effect() {
      jobQueue.add(dosomthing)
      // console.log('jobQueue', jobQueue)
      // jobQueue.forEach(job => job())
      flushJob()
    }
    function dosomthing () {
      console.log(obj.a)
    }
    const p = Promise.resolve()
    let isFlushing = false
    function flushJob () {
      if (isFlushing) return
      isFlushing = true
      p.then(() => {
        jobQueue.forEach(job => job())
      }).finally(() => {
        isFlushing = false
      })
    }
    
    obj.a++
    obj.a++
    
    最后只输出3
```
