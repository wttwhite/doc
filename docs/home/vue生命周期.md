### vue的生命周期是什么
**从一个组件创建、数据初始化、挂载、更新、销毁，这就是一个组件所谓的生命周期。**

具体：
1. new Vue()：开始创建vue实例
2. 执行**beforeCreate**：data:undefined;$el:undefined
3. 拦截观测data数据，初始化事件
4. 执行**created**：data可获取;$el:undefined
5. 判断是否有$el属性，没有则等待vm.$mount(el)；有则判断是否有template，有template则转成render函数，通过render函数去渲染创建dom树；没有则编译el外层html作为模板
6. 执行**beforeMount**，虚拟$el
7. 开始挂载
8. 执行**mounted**，挂载完成，真实$el


**beforeUpdate**，更新之前的事件，钩子中改变状态不会重复渲染

dom重新渲染，re-render和patch

**updated**，更新完成之后，此时dom已经更新，此时更改状态可能会导致更新无限循环

**beforeDestroy**,vue实例销毁前，实例仍然可用，一般用于清除定时器和监听事件

**destroyed**，vue实例销毁

```javascript
beforeCreate: data:undefined;$el:undefined
created: data可获取;$el:undefined
beforeMounted: $el:虚拟
mounted: $el:真实
```
beforeRouteEnter：满足某些条件才允许进入页面

### vue中内置的方法属性和vue生命周期的运行顺序（methods、computed、data、watch、props）
```javascript
function initState(vm: Component) {
  initProps
  initMethods
  initData
  initComputed
  initWatch
}
```
props => methods => data => computed => watch
### 父组件和子组件生命周期钩子执行顺序
渲染过程：父组件挂载完成一定要等子组件都挂载完成后，才算是父组件挂载完
`父beforeCreate -> 父created -> 父beforeMount -> 子beforeCreate -> 子created -> 子beforeMount -> 子mounted -> 父mounted`

子组件更新过程，影响到父组件的情况：`父beforeUpdate -> 子beforeUpdate->子updated -> 父updated`
> 父组件的钩子包裹子组件的钩子