## JS：Cannot set property 'display' of undefined问题

```js
handle(className) {
  var element = document.getElementsByClassName(className)
  element.style.display = "none"
}
```

点击按钮时，根据class名获取元素，并添加css样式进行隐藏，但是出错了

错误信息：`Uncaught TypeError: Cannot set property 'display' of undefined at HTMLInputElement.cancel.onClick....`

问题出在class名这里，class类不能简单直接拿来判断，因为具有多个class，所以要加上数组才能判断

```
handle(className) {
  var element = document.getElementsByClassName(className)[0]
  element.style.display = "none"
}
```
