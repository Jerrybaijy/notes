# BOM

## BOM 基础

**BOM**（**B**rowser **O**bject **M**odel），即浏览器对象模型，是一套操作浏览器功能的 API。

BOM 的核心对象：

- `window` 对象
- `navigator` 对象
- `screen` 对象
- `history` 对象
- `location` 对象

## [window](https://developer.mozilla.org/zh-CN/docs/Web/API/Window)

`window` 对象是 BOM 的顶层对象，表示整个浏览器窗口；所有其他 BOM 对象都是 `window` 的属性或方法。

- [**`alert()`**](https://developer.mozilla.org/zh-CN/docs/Web/API/Window/alert)：弹窗输出
- [**`setinterval()`**](https://developer.mozilla.org/zh-CN/docs/Web/API/Window/setInterval)：时间间隔
- [**`confirm()`**](https://developer.mozilla.org/zh-CN/docs/Web/API/Window/confirm)：弹窗确认

### `addEventListener()`

- `addEventListener` 是 JavaScript 中的一个方法，用于为指定的 DOM 元素添加事件监听器。
- **语法**：`对象.addEventListener("事件类型", 函数)`

    ```javascript
    // 单击按钮执行func函数
    button.addEventListener("click", func)
    ```

## [console](https://developer.mozilla.org/zh-CN/docs/Web/API/console)

**`console`** 对象提供了浏览器控制台调试的接口；

- [**`console.log()`**](https://developer.mozilla.org/zh-CN/docs/Web/API/console/log_static)：控制台输出

## [location](https://developer.mozilla.org/zh-CN/docs/Web/API/Location)

- [**`location.reload()`**](https://developer.mozilla.org/zh-CN/docs/Web/API/Location/reload)：跨域调用