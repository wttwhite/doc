### webpack

```javascript
// add.js
exports.default = function (a, b) {
  return a + b
}
// index.js
const add = require('add.js').default
console.log(add(1, 2))
```

webpack工作原理：分析收集文件之间的依赖关系，使用babel将ES6转成ES5，替换导入导出的require和exports，从入口文件执行自执行函数

#### 1. exports is not defined

```javascript
<script>
    exports.default = function (a, b) {
        return a + b
    }
</script>
// exports is not defined
```

直接使用会报错，相当于`exports`是个对象，里边有个属性

```javascript
const exports = {}
exports.default = function (a, b) {
    return a + b
}
console.log(exports.default(1, 2)) // 3
```

`exports`在其他文件，以字符串的形式引入

```javascript
const exports = {}
eval(`exports.default = function (a, b) {
    return a + b
}`)
console.log(exports.default(1, 2)) // 3
```

会污染全局环境 - 用自执行函数

```javascript
eval(`var a = 111; exports.default = function (a, b) {
    return a + b
}`)
// 执行之后a会污染全局环境，所以使用自执行函数
```

**自执行函数**

```javascript
const exports = {}; // 分号必加 -> {} is not a function
(function(exports, code) {
    eval(code)
})(exports, `var a = 111; exports.default = function (a, b) {
return a + b
}`)
console.log(exports.default(1, 2)) // 3
```

#### 2. require is not defined

```javascript
const require = function (file) {
    const exports = {};
    (function(exports, code) {
        eval(code)
    })(exports, `var a = 111; exports.default = function (a, b) {
    return a + b
    }`)
    return exports
}
const add = require('add.js').default
console.log(add(1, 2))
```

file传值

```javascript
const require = function (file) {
    const exports = {};
    (function(exports, code) {
        eval(code)
    })(exports, files[file])
    return exports
}
const files = {
    'add.js': `var a = 111; exports.default = function (a, b) {
    return a + b
    }`
}
const add = require('add.js').default
console.log(add(1, 2))
```

自执行函数

```javascript
(function (files) {
    const require = function (file) {
        const exports = {};
        (function(exports, code) {
            eval(code)
        })(exports, files[file])
        return exports
    }
    // 从入口执行
    require('index.js')
})(
    {
        'add.js': `var a = 111; exports.default = function (a, b) {
return a + b
}`,
        'index.js': `const add = require('add.js').default
console.log(add(1, 2))`
    }
)
```





```javascript
// add.js
export default (a, b) => {
  return a + b
}
// index.js
import add from './add'
console.log(add(1, 2))
```



npm i @babel/parser @babel/traverse @babel/core @babel/preset-env 

- @babel/parser
- @babel/traverse
- @babel/core
- @babel/preset-env

#### 3. 收集依赖

读取文件

```javascript
const fs = require('fs')
function getModuleInfo (file) {
  // 读取文件
  const body = fs.readFileSync(file, 'utf-8')
  console.log(body)
  // 分析
}
getModuleInfo('./src/index.js')
// node index.js
// import add from './add'
// console.log(add(1, 2))
```







```javascript
// index.js import了哪些文件
const fs = require('fs')
const path = require('path')
const parser = require('@babel/parser') // AST
const traverse = require('@babel/traverse').default // 处理节点遍历
const babel = require('@babel/core') // babel核心代码，ES6转ES5

function getModuleInfo (file) {
  // 读取文件
  const body = fs.readFileSync(file, 'utf-8')
  // 文本转换成AST
  const ast = parser.parse(body, {
    sourceType: 'module'
  })
  // 分析：节点遍历
  const deps = {}
  traverse(ast, {
    // 访问者模式
    // 访问所有的import
    ImportDeclaration({ node }) {
      // 遇到import， node：import语句的节点
      // 做一个路径转换
      const dirName = path.dirname(file) // 获取给定路径的目录名称
      const absPath = './' + path.join(dirName, node.source.value)
      deps[node.source.value] = absPath.replace('\\', '/')
    }
  })
  // ES6 -> ES5
  const { code } = babel.transformFromAst(ast, null, {
    presets: ['@babel/preset-env']
  })

  const moduleInfo = {
    file,
    deps,
    code
  }
  return moduleInfo
}
function parseModule (file) {
  const entry = getModuleInfo(file)
  const temp = [entry]
  const depsGraph = {}
  getDeps(temp, entry)
  temp.forEach(item => {
    depsGraph[item.file] = {
      deps: item.deps,
      code: item.code
    }
  })
  return depsGraph
}
function getDeps (temp, { deps }) {
  Object.keys(deps).forEach(key => {
    const child = getModuleInfo(deps[key])
    temp.push(child)
    getDeps(temp, child)
  }) 
}
console.log(parseModule('./src/index.js'))
// 输出
{ './src/index.js':
   { deps: { './add.js': './src/add.js' },
     code:
      '"use strict";....' 
   },
  './src/add.js':
   { deps: {},
     code:
      '"use strict";...' 
   } 
}
```



生成bundle文件

```javascript
function bundle (file) {
  const depsGraph = JSON.stringify(parseModule(file)) // 不转字符串传参会变成[Object Object]
  return `(function(depsGraph) {
    const require = function(file) {
      const absRequire = function(absFile) {  // 递归调用
        return require(depsGraph[file].deps[absFile])
      }
      const exports = {};
      (function(require, exports, code){
        eval(code)
      })(absRequire, exports, depsGraph[file].code)
      return exports
    }
    require('${file}') // 带引号 - 字符串
  })(${depsGraph})
  `
}
const content = bundle('./src/index.js')
!fs.existsSync('./dist') && fs.mkdirSync('./dist')
fs.writeFileSync('./dist/bundle.js', content)
```



