### instanceof

```javascript
typeof [] // "object"
typeof {} // "object"
[] instanceof Array // true
let obj = {}
obj instanceof Array // false
```

`a instanceof A` a的原型链上是否存在A.prototype

```javascript
function instance (L, R) {
  const prototype = R.prototype
  while(true) {
    if (L === null) {
      return false
    }
    L = L.__proto__
    if (L === prototype) {
      return true
    }
  }
}
```



