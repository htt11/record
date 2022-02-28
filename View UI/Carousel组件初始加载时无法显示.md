## View UI的Carousel组件初始加载时无法显示的问题：

需求：点击图片时使用Modal，用于展示轮播图

这里用的view ui组件库中的 Carousel组件

**问题**：首次显示Modal时，Carousel组件中添加的图片都没显示。然后小小的动一下窗口，图片居然显示了！！！

![Carousel图片未显示](https://github.com/htt11/records/blob/master/img/Carousel.jpg)

查看DOM发现Carousel的轮播容器没有宽度，但数据是存在div内部的，就是无法正常显示出来

**原因**：包含Carousel的父组件在初次被渲染时处于隐藏状态，而Carousel也同时被隐藏起来，两个组件无法同时渲染的话，就造成类似的问题，Carousel组件内其实是在正常工作的；

![Carousel图片未显示](https://github.com/htt11/records/blob/master/img/Carousel-width.jpg)

**解决**：

```html
<Modal v-model="modal">
  <Carousel v-model="value" v-if="modal">
    <CarouselItem>......</CarouselItem>
  </Carousel>
</Modal>
```

