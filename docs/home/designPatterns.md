## 设计模式
### 工厂模式

### 1.检查大写按键是否打开
可以使用 `KeyboardEvent.getModifierState()` 来检测是否 `Caps Lock` 打开。
```javascript
const passwordInput = document.getElementById('password');

passwordInput.addEventListener('keyup', function (event) {
    if (event.getModifierState('CapsLock')) {
        // CapsLock 已经打开了
    }
}); 
```
### 2. 复制到剪贴板
可以使用 `Clipboard` API 创建“复制到剪贴板”功能
```javascript
function copyToClipboard(text) {
    navigator.clipboard.writeText(text);
}    
```
### 3. 获取鼠标位置
可以使用 `MouseEvent` 对象下 `clientX` 和 `clientY` 的属性值，获取鼠标的当前位置坐标信息。
```javascript
document.addEventListener('mousemove', (e) => {
    console.log(`Mouse X: ${e.clientX}, Mouse Y: ${e.clientY}`);
}); 
```
### 4. 元素的自定义数据属性(data-*)
```javascript
<div id="user" data-name="John Doe" data-age="29" data-something="Some Data">
    <div data-key="aaaa">
      John Doe
    </div>
</div>
<script>
    const user = document.getElementById('user');
  
    console.log(user.dataset); 
    // { name: "John Doe", age: "29", something: "Some Data" }
    // 获取元素
    const id = 'aaaa'
    user.querySelector(`div[data-key="${id}"]`)
    
</script> 
```
