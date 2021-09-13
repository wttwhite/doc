### 函数式编程
#### 1. 基本概念
用函数写程序
实现最小粒度的函数封装、组合、复用（积木逻辑）
更换思维方式：用表达式来描述程序（而非用过程组织计算）

特点：
- 程序像是写的文章（富有描述性），尽量避免变量定义和计算过程；（用函数的组合来表达计算过程，而非计算步骤）
- 函数很小巧，灵活组装使用（特别是流式计算）
- 递归是常见的手段
- 函数通常没有副作用

实现一个排列组合‘abc’ -> ['abc','acb','bac','bca','cab','cba]
```javascript
function permutation(str) {
    function remove(str, i) {
        const newSet = new Set([...str])
        newSet.delete(i)
        return newSet
    }
    function flattern (array) {
        if (!Array.isArray(array)) {
            return array
        } else {
            // return [].concat(...array.map(arr => flattern(arr))) 同下
            return [].concat(...array.map(flattern))
        }
    }
    // console.log(flattern([1,[2,[3,[4,5]],6]]))
    function R(set) {
        if(set.size === 1) {
            return [set.values().next().value]
        } else {
            return flattern([...set].map(char => R( remove(set,char)).map(perm => char + perm) ))
        }
    }
    return R(new Set([...str])) // ['a','b','c']
}
console.log(permutation('abc')) //  ["abc", "acb", "bac", "bca", "cab", "cba"]
```
#### 2. 节流

#### 3. 柯里化
#### 4. 实现一个Animated<T>的Monad
