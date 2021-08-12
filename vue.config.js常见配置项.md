```js
// vue.config.js
const webpack = require('webpack')
module.exports = {
    // 选项
}
```

## publicPath：

部署应用包时的基本URL：

- Type：`string`
- Default：`'/'`

默认情况下，Vue CLI 会假设你的应用是被部署在一个域名的根路径上;

`publicPath` 也可以设置为`''`或者`'./'`，设置成相对路径后可以任意部署

```js
module.exports = {
    // 指定子路径
    publicPath: '/my-app/'  
}
```

在开发环境下，如果想把开发服务器架设在根路径，可以使用一个条件式的值：

```js
module.exports = {
    publicPath: process.env.NODE_ENV === 'production'
}
```

## outputDir：

项目打包生成的文件存储目录路径（打包位置），可以是静态路径或绝对路径；

构建时传入 --no-clean 可关闭该行为；

- Type：`string`
- Default：`'dist'`

```js
module.exports = {
    outputDir: 'dist',
}
```

<u>注意：请始终使用 `outputDir` 而不要修改 webpack 的 `output.path`</u>

<u>原因： `vue.config.js` 中的值会被用在配置里的多个地方</u>

## indexPath：

指定生成的`index.htm`l的输出位置：

- Type：`string`
- Default：`'index.html'`<!--相对于outputDir，也可以是绝对路径-->

```js
module.exports = {
    indexPath: 'window.html',
}
```

## assetsDir：

静态资源目录，放置生成的静态资源 (js、css、img、fonts) 的目录<!--相对于outputDir-->

- Type：`string`
- Default：`''`

```js
module.exports = {
    assetsDir: 'assets',
}
```

## devServer：

webpack-dev-server 相关配置，所有 webpack-dev-server 的选项都支持；

- Type: `Object`

```js
module.exports = {
    devServer: {
     	open: true,		// 自动打开浏览器
        inline: true, 	// 开启实时刷新
    	host: '0.0.0.0', 	// 允许外部ip访问
    	port: '8060',   
    	proxy：'http://localhost:4000',		// API访问代理，或proxy:{...}
        // ......
    }
}
```

[Vue CLI4.0 webpack配置属性——devServer](https://blog.csdn.net/weixin_44869002/article/details/105864712)

[Vue CLI4.0 webpack配置属性——devServer.proxy](https://blog.csdn.net/weixin_44869002/article/details/108814772)

## configureWebpack:

调整webpack配置：

- Type: `object | Function`

**以对象形式**：会通过 [webpack-merge](https://github.com/survivejs/webpack-merge) 合并到最终的配置中；

```js
module.exports = {
	configureWebpack: {
        // 插件，对webpack本身的扩展
		plugins: [
            //...
        ],
        // 引入插件
        externals: [
			AMap: "AMap",
			AMapUI: "AMapUI"
        ],
		// 设置路径别名，默认webpack设置src的别名为@
    	resolve: {
			alias: {
				'components': '@/components',
				'content': 'components/content',
				'common': 'components/common',
				'assets': '@/assets',
				'network': '@/network',
				'views': '@/views',
			}
		}
	}
}
```

**以函数形式**：会接收被解析的配置作为参数。该函数既可以修改配置并不返回任何东西，也可以返回一个被克隆或合并过的配置版本。

```js
module.exports = {
	configureWebpack: config => {	
		if (process.env.NODE_ENV === 'production') {
			// 为生产环境修改配置...
		} else {
			// 为开发环境修改配置...
		}
        config["externals"] = {
			AMap: "AMap",
			AMapUI: "AMapUI"
		}
  }
}
```

[webpack > 简单的配置方式](https://cli.vuejs.org/zh/guide/webpack.html#简单的配置方式)

## chainWebpack：

允许对内部的 webpack 配置进行更细粒度的修改，链式操作；

- Type: `Function`

[webpack > 链式操作 (高级)](https://cli.vuejs.org/zh/guide/webpack.html#链式操作-高级)

## productionSourceMap：

生产环境是否生成 sourceMap 文件

- Type: `boolean`
- Default: `true`

```
module.exports = {
	productionSourceMap: true
}
```

## filenameHashing：

设置打包生成的的静态资源的文件名中是否加入`hash`以便控制浏览器缓存问题

- Type: `boolean`
- Default: `true`

## lintOnSave：

是否开启eslint保存检测

- Type: `boolean` | `'warning'` | `'default'` | `'error'
- Default: `default`

```js
module.exports = {
	lintOnSave: false
}
```









