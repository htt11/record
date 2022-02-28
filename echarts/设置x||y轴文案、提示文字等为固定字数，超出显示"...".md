## echarts - 设置x||y轴文案、提示文字等为固定字数，超出显示"..."

关于x轴文案的设置，是**axisLabel**属性，

而跟内容有关的是**formatter**，它有一个强大的**回调函数**，其参数value就是轴上显示的文案，

- 形式 ：string / Function

```js
// 使用字符串模板，模板变量为刻度默认标签 {value}
formatter: '{value} kg'
// 使用函数模板，函数参数分别为刻度数值（类目），刻度的索引
formatter: function (value, index) {
    return value + 'kg';
}
```

代码如下：

```js
// 超出四个字数，则显示为...
axisLabel : 
  {
    formatter : function (value) {
	  let valueTxt = '';
	  if (value.length > 4) {
		valueTxt = value.substring(0, 4) + '...';
	  } else {
		valueTxt = value;
	  }
	  return valueTxt ;
	}
  }
```



### 饼图的提示文案加...

饼图的设置里，负责显示文案的是**label**属性，同样和内容有关的是**formatter**属性，

形式 ：

- 字符串模板 

  - `{a}`：系列名。
  - `{b}`：数据名。
  - `{c}`：数据值。
  - `{d}`：百分比。
  - `{@xxx}`：数据中名为 `'xxx'` 的维度的值，如 `{@product}` 表示名为 `'product'` 的维度的值。
  - `{@[n]}`：数据中维度 `n` 的值，如 `{@[3]}` 表示维度 3 的值，从 0 开始计数。

  ```js
  formatter: '{b}: {d}'
  ```

- 回调函数

  - 格式：`(params: Object|Array) => string`

  - 参数 `params` 是 formatter 需要的单个数据集。格式如下：

    ```js
    {
        componentType: 'series',
        // 系列类型
        seriesType: string,
        // 系列在传入的 option.series 中的 index
        seriesIndex: number,
        // 系列名称
        seriesName: string,
        // 数据名，类目名
        name: string,
        // 数据在传入的 data 数组中的 index
        dataIndex: number,
        // 传入的原始数据项
        data: Object,
        // 传入的数据值。在多数系列下它和 data 相同。在一些系列下是 data 中的分量（如 map、radar 中）
        value: number|Array|Object,
        // 坐标轴 encode 映射信息，
        // key 为坐标轴（如 'x' 'y' 'radius' 'angle' 等）
        // value 必然为数组，不会为 null/undefied，表示 dimension index 。
        // 其内容如：
        // {
        //     x: [2] // dimension index 为 2 的数据映射到 x 轴
        //     y: [0] // dimension index 为 0 的数据映射到 y 轴
        // }
        encode: Object,
        // 维度名列表
        dimensionNames: Array<String>,
        // 数据的维度 index，如 0 或 1 或 2 ...
        // 仅在雷达图中使用。
        dimensionIndex: number,
        // 数据图形的颜色
        color: string,
    
        // 百分比
        percent: number,
    
    
    }
    ```

  - 其中，参数params的name属性就是要显示的文案

代码如下：

```js
label :
 {
     normal :
     {
         show : true, position : 'inner',
         formatter : function (params)
         {
             console.log(params) 
             let newName = '';
             if (params.name.length > 5) {
                 newName = params.name.substring(0, 5) + '...';
             }
             else {
                 newName = params.name;
             }
             return newName;
         }
     }
 }
```

