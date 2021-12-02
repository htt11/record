## vue中echats图表自适应窗口的方法：

在使用echarts时,为了兼容移动端.使用了flxe布局，出现echarts超出父盒子宽度的问题；

echarts绘制机制：echarts图形只绘制一次，且绘制时自动获取父级大小填写宽度；

echarts要实现自适应大小，需要在页面发生大小改变的时候，对图表实例进行**重绘**；

在echarts里边，提供了一个重绘的方法：**resize()** 图表的实例对象调用该方法即可进行重绘。

### 1. 使用 window.onresize：

```js
initChart() {
  let option = {......};
  let myChart = this.getChartByDom(this.$refs.EChartDom);
  myChart.setOption(option);
    
  // 单个图表的自适应
  window.onresize = function () {
    myChart.resize()；
  }
}
```

缺点：多个echarts的时候就只有最后一个生效了，onresize会被覆盖；



### 2. 使用 window.addEventListener 添加 resize 方法：

```js
initChart() {
  // ......
    
  // 多个图表的自适应
  let myChart = this.getChartByDom(this.$refs.EChartDom);
  let listener= function () {
    myChat.resize();
  }
  window.addEventListener('resize', listener);
}
```

缺点：当vue页面路由跳转到下一个页面时，上一个页面的onresize方法会继续执行；



上面所涉及到的图表，我只在home页使用了，于是添加了路由验证：

```js
initChart() {
  let _this = this;
  // ......
  window.onresize = function () {
    if (_this.$route.name === 'Home') {
	  chart.resize()
	}
  }
}
```

如果echarts图表在多个路由中使用，无法用路由区分的话，可以参考https://www.cnblogs.com/xikui/p/14148224.html中的第三种方法；



如果在使用中缩放echarts图时发现，随着宽度改变，会自适应，但是自适应的宽度不正确；

这可能是因为窗口改变时Echarts立即获取的宽度不正确，可以尝试加一个延时：

```js
window.onresize = function () {
  setTimeout(function(){
	chart.resize();
  },100)
}
```







