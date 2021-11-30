## Date：

要创建日期对象，就使用 new 操作符来调用 Date 构造函数： 

```js
let now = new Date();
```

在不给 Date 构造函数传参数的情况下，创建的对象将保存当前日期和时间。要基于其他日期和时 间创建日期对象，必须传入其毫秒表示（UNIX 纪元 1970 年 1 月 1 日午夜之后的毫秒数）;

ECMAScript 为此提供了两个辅助方法：Date.parse()和 Date.UTC()；

### Date.parse()：

- 该方法接收一个表示日期的字符串参数，尝试将这个字符串转换为表示该日期的毫秒数；
- ECMA-262 第 5 版定义了 Date.parse()应该支持的日期格式，填充了第 3 版遗留的空白。所有实
  现都必须支持下列日期格式：
  - “月/日/年”，如"5/23/2019"； 
  - “月名 日, 年”，如"May 23, 2019"； 
  - “周几 月名 日 年 时:分:秒 时区”，如"Tue May 23 2019 00:00:00 GMT-0700"； 
  -  ISO 8601 扩展格式“YYYY-MM-DDTHH:mm:ss.sssZ”，如 2019-05-23T00:00:00（只适用于 兼容 ES5 的实现）

- 如果传给 Date.parse()的字符串并不表示日期，则该方法会返回 NaN；

- 如果直接把表示日期的字符串传给Date构造函数，那么 Date 会在后台调用 `Date.parse()` ;

  ```js
  // 下面的两种方式是等价的，得到的日期对象相同
  let someDate1 = new Date(Date.parse("May 23, 2019"));
  let someDate2 = new Date(("May 23, 2019"));
  ```

- **注：不同浏览器对 Date 类型的实现有很多问题：**

  - 很多浏览器会选择用当前日期替代越界的日期，因此有些浏览器会将"January 32, 2019"解释为"February 1,  2019"；
  - Opera 则会插入当前月的当前日，返回"January 当前日, 2019"。就是说，如 果是在 9 月 21 日运行代码，会返回"January 21, 2019"。

  

### Date.UTC()：

- 该方法也返回日期的毫秒表示，但和 `Date.parse()` 的参数不同；

- **参数**：年、零起点月数（1 月是 0，2 月是 1，以此类推）、日（1~31）、时（0~23）、 分、秒和毫秒；

  - 只有前两个参数（年和月）是必须的；
  - 如果不提供日，那么默认为 1 日；其他参数的默认值都是 0；

  ```js
  // GMT 时间 2000 年 1 月 1 日零点
  let y2k = new Date(Date.UTC(2000, 0)); 
  // GMT 时间 2005 年 5 月 5 日下午 5 点 55 分 55 秒
  let allFives = new Date(Date.UTC(2005, 4, 5, 17, 55, 55)); 
  ```

- 与 `Date.parse()`一样，`Date.UTC()`也会被 Date 构造函数隐式调用:

  - 区别在于：这种情况 下创建的是本地日期，不是 GMT 日期；
  - 不过 Date 构造函数跟 `Date.UTC()`接收的参数是一样的，因 此，如果第一个参数是数值，则构造函数假设它是日期中的年，第二个参数就是月，以此类推；

  ```js
  // 本地时间 2000 年 1 月 1 日零点
  let y2k = new Date(2000, 0); 
  // 本地时间 2005 年 5 月 5 日下午 5 点 55 分 55 秒
  let allFives = new Date(2005, 4, 5, 17, 55, 55);
  ```

  - 以上代码创建了与前面例子中相同的两个日期，但这次的两个日期是（由于系统设置决定的）本地 时区的日期。

## Date.now()：

- ECMAScript 还提供了 Date.now()方法，返回表示方法执行时日期和时间的毫秒数。这个方法可 以方便地用在代码分析中；

  ```js
  // 起始时间
  let start = Date.now(); 
  // 调用函数
  doSomething(); 
  // 结束时间
  let stop = Date.now(), 
  result = stop - start; 
  ```



## js获取时间戳的方式：

1、**Date.parse()**

```js
let time1 = Date.parse(new Date());			// 1638258443000，精确到秒
```

2、**Date.getTime()**

```js
let time2 = new Date().getTime();			// 1638258443327，精确到毫秒
```

3、**new Date().valueOf()**

```js
let time3 = new Date().valueOf();			// 1638258443327,精确到毫秒
```

4、**Date.now()**

```js
let time4 = Date.now();						// 1638258443327,精确到毫秒
```

5、**+new Date（）**

```js
let time5 = +new Date();			// 1638258443000，精确到秒
```



### js的 `getTime()` 和 `Date.parse()` 方法的陷阱：

**陷阱一**：getTime()和Date.parse()方法都是返回某个时间到1970年1月1日0:00的时间戳，但是下面代码结果却是 1970年1月1日08:00 开始，这样就相差八个小时；

```js
function startTime() {
  let date = new Date;
  year = date.getFullYear();
  month = date.getMonth() + 1;
  day = date.getDate();
  return Date.parse(year + '-' + month + '-' + day) ;
}
// 因为当年月日中间是 ‘-’ 短横线的时候，它的解析是用UTC 时区处理，而不是用本地时区处理的，因此相差八个小时，就成了这个时间点到1970年1月1日08:00的毫秒数。
// 解决办法就是将日期中的短横线替换成 ‘/’ ,
// getTime()和Date.parse()方法 都会有相同的情况
```

**陷阱二**：JS用Date.gettime("yyy-MM-dd hh:mm:ss")解析时间格式，IE8以下的环境下出现NaN, safari浏览器出现NaN；

```js
function time(){
  var timeBegin = ''2018-09-18 12:00:00"

  var startTime =timeBegin.replace(/\-/g, "/"); // 需要将字符串日期中的 ‘-’ 替换成 ‘/’ ,
  return new Date(startTime).getTime();// 这里得的就是时间戳，不会是NaN

  function test() {
    var dateStr = "02/01/2015"
    var date = Date.parse(dateStr )
    alert(date );
　}
}
```



