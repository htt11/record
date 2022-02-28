View UI 更改主题色：

项目中使用了webpack，这里使用了变量覆盖的方式进行修改：

1. 新建iview-theme.less文件

```less
@import '~view-design/src/styles/index.less';

// Here are the variables to cover, such as:
@primary-color: #5ac19a;
```

2. 在入口文件main.js中导入less文件

```js
import Vue from 'vue'
import iView from 'view-design';
// import 'view-design/dist/styles/iview.css';
import './common/iview-theme.less';

Vue.use(iView);
```

**报错：Inline JavaScript is not enabled. Is it set in your options?**

**解决：在vue.config中配置**

```js
css: {
    loaderOptions: {
      less: {
        javascriptEnabled: true
      }
    }
},
```

<!--注意：需重新启动项目生效-->
