## typeOf操作符：

鉴于ECMAScript是松散型的，因此需要一些手段来检测给定变量的数据类型；

- #### typeOf操作符可能返回下列某个字符串：

  - "underfined"  ——未定义
  - "boolean"  ——布尔值
  - "string"  ——字符串
  - "number" ——数值
  - "object" —— 值是对象或者null
  - "function" ——函数

  ```js
  typeOf 'hello'		// string
  typeOf('hello')		// string
  typeOf 95         // number
  ```

- typeOf操作符的操作数可以是变量（message）,也可以是数值字面量；

- **注意**，typeOf是一个操作符而不是函数，因此例子中的圆括号可用可不用，非必需；

- 关于`typeOf null = object`，因为特殊值null被认为是一个空的对象引用；

- Safari 5及之前版本、Chrome 7及之前的版本在对`正则表达式`调用typeOf操作符时会返回`“function”`，而其他浏览器在这种情况下会返回`"object"`；

- typeOf操作符对`未初始化`和`未声明`的变量执行typeOf操作符都都返回了`underfined`值；

  - 这种结果有其逻辑上的合理性。
  - 虽然这两种变量从技术角度看有本质区别，但实际上无论对哪种变量也不可能执行真正的操作；

  ```js
  var name;
  console.log(name);		// underfined
  console.log(age);		// 报错
  
  console.log(typeOf name);	// underfined
  console.log(typeOf age);	// underfined
  ```

  
