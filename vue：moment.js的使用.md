## vue中使用moment.js：

1. 安装：

   ```bash
   npm install moment --save
   ```

2. main.js中引入并配置：

   ```js
   import moment from moment;
   
   Vue.prototype.$moment = moment;
   ```

3. 组件中使用：

   ```js
   import moment from 'moment';
   
   // 获取当前日期和时间 并格式化，同 moment(new Date())
   var now = moment().format('YYYY-MM-DD HH:mm:ss');		// 2021-11-10 14:22:20
   ```

   ```js
   // moment(String)
   moment("2010-03-05 15:10:03");
   // moment(Object) 
   moment({ y:2010, M:3, d:5, h:15, m:10, s:3});
   // moment(Number) 
   moment(1318781876406);		// 毫秒为单位
   // moment(Date)
   moment(new Date(2010, 3, 5));
   // moment.unix(Number)
   moment.unix(1318781876);	// Unix时间戳，秒为单位
   ......
   ```

4. 也可设置过滤器进行使用：

- 全局过滤器：

  ```js
  // main.js
  Vue.filter('moment', function (value, formatString='YYYY-MM-DD HH:mm:ss') {
    return moment(value).format(formatString); // value可以是普通日期 20170723
    // return moment.unix(value).format(formatString); // 这是时间戳转时间
  });
  ```

  ```html
  <p>{{ msg | moment}}</p>
  ```

- 局部过滤器：

  ```js
  filter：{
    moment: function(value, formatString='YYYY-MM-DD HH:mm:ss') {
        return moment(value).format(formatString);
    }
  }
  ```

  ```html
  <p>{{ msg | moment}}</p>
  ```

 
moment() 与 moment.unix() : [moment官方解释](http://momentjs.cn/docs/#/parsing/unix-timestamp/)

- moment 日期格式化：

  ```js
  moment().format('MMMM Do YYYY, h:mm:ss a'); // 十一月 10日 2021, 10:02:28 上午
  moment().format('dddd');                    // 星期三
  moment().format("MMM Do YY");               // 11月 10日 21
  moment().format('YYYY [escaped] YYYY');     // 2021 escaped 2021
  moment().format();                          // 2021-11-10T10:02:28+08:00
  ```

- moment 相对时间：

  ```js
  moment("20111031", "YYYYMMDD").fromNow(); // 10 年前
  moment("20120620", "YYYYMMDD").fromNow(); // 9 年前
  moment().startOf('day').fromNow();        // 10 小时前
  moment().endOf('day').fromNow();          // 14 小时内
  moment().startOf('hour').fromNow();       // 2 分钟前
  ```

- 日历时间：

  ```js
  moment().subtract(10, 'days').calendar(); // 2021/10/31
  moment().subtract(6, 'days').calendar();  // 上星期四10:02
  moment().subtract(3, 'days').calendar();  // 上星期日10:02
  moment().subtract(1, 'days').calendar();  // 昨天10:02
  moment().calendar();                      // 今天10:02
  moment().add(1, 'days').calendar();       // 明天10:02
  moment().add(3, 'days').calendar();       // 下星期六10:02
  moment().add(10, 'days').calendar();      // 2021/11/20
  ```
......
  

