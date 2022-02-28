## 本地存储localStorage的使用：

**localStorage 和 sessionStorage 属性允许在浏览器中存储 key/value 对的数据：**

- localStorage 属于永久性存储，保存的数据没有过期时间，直到手动去删除；

- sessionStorage 属于临时存储，当会话结束的时候，sessionStorage 中的键值对会被清空；

**localStorage 语法：**

- 新增：localStolrage.setItem("key", "value")
- 读取：localStorage.getItem(key)
- 删除单个值：localStorage.removeItem(key)
- 清空：localStorage.clear()

```js
// localStolrage实际可通过三种方式存取，官方推荐的是 getItem\setItem 对其进行存取

//写入a字段
storage["a"]=1;
//写入b字段
storage.b=2;
//写入c字段
storage.setItem("c",3);

//读取a字段
var a=storage.a;
console.log(a);		// "1"
//读取b字段
var b=storage["b"];
console.log(b);		// "2"
//读取c字段
var c=storage.getItem("c");		// "3"
```

**注意：localStorage 只支持 string 类型的存储**

- 例如存储进去的是int类型，打印出来的却是string类型

- localStorage 存储JSON对象类型数据时需要进行一些转换：

  - 使用 JSON.stringify() 方法，来将 JSON对象 转换成为 JSON 字符串进行存储；
  - 读取之后使用 JSON.parse()方法，重新转化为 JSON对象形式；

  ```js
  var data = {
      test:"text",
      test1:"123456",
      test2:"字段值",
  }
  // 存
  localStorage.setItem("data", JSON.stringify(data));
  // 取
  var data1 = localStorage.getItem("data");
  data1 = JSON.parse(data1);
  ```

  

