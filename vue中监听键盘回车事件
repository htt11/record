## vue中监听键盘回车事件：

- 使用键盘修饰符：

  ```html
  <input v-on:keyup.13 = "submit"></input>
  ```

- 或使用按键的别名：

  ```html
  <input v-on:keyup.enter = "submit"></input>
  <!--语法糖-->
  <input @keyup.enter = "submit"></input>
  ```

注意！！！如果用了封装组件的话，比如element，这个时候使用按键修饰符需要加上`.native`

例如：

```html
<el-input v-model="account" @keyup.enter.native="search()"></el-input>
```



### 扩：

#### 常见的按键别名：

- .enter		回车
- .tab 		   换行
- .delete	  (捕获“删除”和“退格”键)
- .esc 		   退出
- space 	   空格
- .up
- .down
- .left
- .right



#### 修饰键：

除了上面提到的按键别名，还可以用如下修饰键开启鼠标或键盘事件监听，使在按键按下时发生响应。

- .ctrl
- .alt
- .shift
- .meta (window系统下是window键，mac下是command键)

**与按键别名不同的是，修饰键在与keyup配合时，只有在按键按下时且没有操作其他键才能生效。**

```html
<!-- Alt + C -->
<input @keyup.alt.67="doSth">
<!-- Ctrl + Click -->
<div @click.ctrl="doSth">点我</div>
```



也可以使用keycode去指定具体的按键（不推荐）

`Vue.config.keyCodes.自定义键名=键码`，可以去定制按键别名

