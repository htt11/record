### Axios post传参的两种方式：

- **params** 是添加到url的请求字符串中的；
- **data**是 添加到请求体body中的；

**使用场景**：使用 `data` 还是 `params `方式，与后端的接口有关；

<!--注：get请求只有params方式；-->

#### 第一种：data方式：

```js
this.$axios({
   url: '/api/user/login' ,
   method: 'post',
   headers: {
      'Content-Type': 'application/x-www-form-urlencoded'
   },
   data:{
      username: this.user,
      pwd: this.pwd
   }
}).then(res => {
  console.log(res)
})
```

#### 第二种：params方式：

```js
this.$axios({
   url: '/api/user/login' ,
   method: 'post',
   headers: {
      'Content-Type': 'application/x-www-form-urlencoded'
   },
   params:{
      username: this.user,
      pwd: this.pwd
   }
}).then(res => {
  console.log(res)
})
```

**注：直接使用post方法，传递的参数为data的方式**

```js

this.$axios.post('/api/user/login',{username: this.user, pwd: this.pwd }),
  {
    headers: {
      'Content-Type': 'application/x-www-form-urlencoded'
    }
  }).then(res => {
      console.log(res)
  })
```



#### 扩展：

#### post 请求常见的 content-type 类型：

- Content-Type: application/json ： 请求体中的数据会以json字符串的形式发送到后端；<!--默认-->
- Content-Type: application/x-www-form-urlencoded：请求体中的数据会以普通表单形式（键值对）发送到后端；<!--使用较多-->
- Content-Type: multipart/form-data： 它会将请求体的数据处理为一条消息，以标签为单元，用分隔符分开。既可以上传键值对，也可以上传文件；

`注：当content-type类型与后端要求的不一样时，可能会导致数据获取不到;`

#### 配置axios请求头中的content-type为指定类型：

```js
// main.js
import axios from 'axios';
axios.defaults.headers.post['Content-Type'] = 'application/x-www-form-urlencoded';
Vue.prototype.$axios = axios;
```



