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

