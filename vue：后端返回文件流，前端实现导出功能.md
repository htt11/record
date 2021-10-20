## vue中后端返回文件流，前端实现导出功能：

项目中有一个导出功能的实现，因为需求对导出文件的数据格式和样式有要求，所以这个导出功能放到后端来做，而且后端返回的是文件流，所以需要处理成想要的文件并导出来。

```html
<button @click="onExport">导出</button>
```

后端返回的文件流，在浏览器F12控制面板中看到的是一堆看不懂的乱码，

```
��ࡱ�;��	���������������������������������������������������������������������������������������������������������������������������������������������������������������������������������������������������������������������������������������Entry������������Workbook�������������p��������	

 !"#$%&'()*+,-./0123456789:;<=>?@ABCDEFGHIJKLMNOPQRSTUVWXYZ[\]^_`abcdefghijklmnopqrstuvwxyz{|}~�	��A����\proot              ....
```

但是在控制台打印`.then(res => ...)`中的数据时，得到了类似这样的代码：

```js
{
  config: {url: "xxxx/downloadname", method: "get", headers: {…}, baseURL: "", …},
  data: "xxxxx...",
  headers: {...,content-disposition: "xxx.xsl", content-type: "application/vnd.ms-excel",…}
  request: XMLHttpRequest {readyState: 4, timeout: 120000,  …}
  status: 200
  statusText: "OK"
  __proto__: Object
}
```

接下来要处理这堆乱码，因为用到的地方多，所以封装了一个公共方法并抛出：

- 虽然vue里有封装好的请求接口的方法，但是这里要单独使用axios，所以这里先引入axios

```js
// src/common/export.js
import axios from 'axios'

// 导出功能公用方法
export function exportMethod(data) {
    // 区分get 、post请求
    let axiosParams = {}
    if (data.method === 'get') {
        axiosParams = {
            method: data.method,
            url: `${data.url}${data.params ? '?' + data.params : ''}`,
            responseType: 'blob'
        }
    } else {
        axiosParams = {
            method: data.method,
            url: data.url,
            responseType: 'blob',
            data:data.data
        }
    }
    axios(axiosParams).then((res) => {
        const link = document.createElement('a')
        let blob = new Blob([res.data], {type: res.data.type || 'application/vnd.ms-excel'})  //这里设置默认导出为excel，需要其他格式时单独传参数
        
        link.style.display = 'none'
        link.href = URL.createObjectURL(blob)
 
        link.download = data.fileName ? data.fileName : res.headers['content-disposition'] //下载后文件名可由前端固定写死，或由后端提供
        document.body.appendChild(link)
        link.click()
        document.body.removeChild(link)
    }).catch(error => {
        this.$Notice.error({
            title: '错误',
            desc: '网络连接错误'
        })
        console.log(error)
    })
}
```

在使用的页面中引入方法：

```js
import { exportMethod } from '@/common/export'
```

在methods导出的方法里，调用共用导出方法。

```js
// get请求
let myObj = {
  method: 'get',
  url: 'xxx/xxx/export',
  fileName: '导出文件标题',	// 指定导出文件名
  params: params，
  type: 'application/octet-stream'	// 指定导出文件格式
}
exportMethod(myObj)

//post请求
let myObj = {
  method: 'post',
  url: 'xxx/xxx/export',
  fileName: '导出文件标题',
  data: data
}
exportMethod(myObj)
```

