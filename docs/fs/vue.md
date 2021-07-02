### 指令
只能输入数字(不包括计数法)
```javascript
Vue.directive(
    'number-only', {
        bind: function(el, binding, vnode) {
            let ele = el.tagName === 'INPUT' ? el: el.querySelector('input')
            ele.oninput = function() {
                vnode.context.$nextTick(() => {
                    let rule = /\D/g
                    let val = ele.value.replace(rule, '')
                    ele.value = val
                    let arr = binding.expression.split('.')
                    switch(arr.length) {
                        case 1: vnode.context[binding.expression] = ele.value
                            break
                        case 2: vnode.context[arr[0]][arr[1]] = ele.value
                            break
                    }

                })
            }
        }
    }
)

```
使用：
`v-number-only = "form.number"`