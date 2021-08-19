### Axios post传参的两种方式：

params是添加到url的请求字符串中的；

dara是添加到请求体body中的；

<!--注：get请求只有params方式；-->

#### 第一种：data方式：

```js
this.$axios({
   url: '/api/user/login' ,
   method: 'post',
   headers: {
      'Content-Type': 'application/json'
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
      'Content-Type': 'application/json'
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
      'Content-Type': 'application/json'
    }
  }).then(res => {
      console.log(res)
  })
```

### 使用场景：

使用 `data` 还是 `params `方式，与后端的接口有关；