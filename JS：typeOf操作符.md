## typeOf操作符：

鉴于ECMAScript是松散型的，因此需要一些手段来检测给定变量的数据类型；

typeOf操作符可能返回下列某个字符串：

- "underfined"  ——未定义
- "boolean"  ——布尔值
- "string"  ——字符串
- "number" ——数值
- "object" —— 对象或者null
- "function" ——函数

```js
typeOf 'hello'		// string
typeOf('hello')		// string
typeOf 95			// number
```

typeOf操作符的操作数可以是变量（message）,也可以是数值字面量；

**注意，typeOf是一个操作符而不是函数，因此例子中的圆括号可用可不用，非必需；**

关于`typeOf null = object`，因为特殊值null被认为是一个空的对象引用；

Safari 5及之前版本、Chrome 7及之前的版本在对`正则表达式调用typeOf操作符`时会返回`“function”`，而其他浏览器在这种情况下会返回`"object"`；
