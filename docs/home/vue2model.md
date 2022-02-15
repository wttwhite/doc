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
