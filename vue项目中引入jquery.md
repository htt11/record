# vue项目中引入jquery：

使用场景：用vue-cli脚手架工具构建项目成功后 ，当需要引入JQ时

- 安装依赖：`npm install jquery --save-dev`

- 引入 / 修改配置文件：

  - 引入：组件中需要使用jQuery库时

    ```js
    import $ from 'jquery'
    ```

  - 修改配置文件

    ```js
    // vue.config.js
    const webpack = require('webpack')
    module.exports={
        configureWebpack:{  
            plugins: [
                // 使用ProvidePlugin加载的模块可以全局使用，在使用时将不再需要import和require进行引入
                new webpack.ProvidePlugin({		// 实例初始化
                    $: 'jquery',
                    jQuery: 'jquery',
                    'windows.jQuery':'jquery'
                })
            ]js
    }
    ```

- 使用：

  ```js
  mounted(){
      $('#loginName').focus();
  }
  ```

**注：如果项目中引用了.eslintrc.js文件，此时会提示 找不到 $或者jquery的错误;**

解决：需要在文件的module.exports中，为env添加一个键值对 jquery: true

```js
// .eslintrc.js
module.exports = {
  root: true,
  env: {
    // ...
    jquery: true
  }
    // ...
}
```

