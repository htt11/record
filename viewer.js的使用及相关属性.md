viewer.js：

是什么：JavaScript 图像查看器；

### 安装：

NPM 安装：

```bash
npm install viewerjs
```

CDN 引入：

```html
<link  href="/path/to/viewer.css" rel="stylesheet">
<script src="/path/to/viewer.js"></script>
```

### 用法：

**语法**：`new Viewer(element[, options])`

Example:

```html
<!-- 一张图片 -->
<div>
  <img id="image" src="picture.jpg" alt="Picture">
</div>
<!-- 多张图片 -->
<div>
  <ul id="images">
    <li><img src="picture-1.jpg" alt="Picture 1"></li>
    <li><img src="picture-2.jpg" alt="Picture 2"></li>
    <li><img src="picture-3.jpg" alt="Picture 3"></li>
  </ul>
</div>
```

```js
// import 'viewerjs/dist/viewer.css';
import Viewer from 'viewerjs';

// View an image.
const viewer = new Viewer(document.getElementById('image'), {
  inline: true,
  viewed() {
    viewer.zoomTo(1);
  },
});
// Then, show the image by clicking it, or call `viewer.show()`.

// View a list of images.
// Note: All images within the container will be found by calling `element.querySelectorAll('img')`.
const gallery = new Viewer(document.getElementById('images'));
// Then, show one image by click it, or call `gallery.show()`.
```

### 键盘支持：

> 仅在模态模式下可用。

- `Esc`：退出全屏或关闭查看器或退出模态模式或停止播放。
- `Space`: 停止播放。
- `Tab`：切换查看器中按钮的焦点状态。
- `Enter`：触发按钮上的点击事件处理程序。
- `←`：查看上一张图片。
- `→`：查看下一张图片。
- `↑`：放大图像。
- `↓`：缩小图像。
- `Ctrl + 0`：缩小到初始大小。
- `Ctrl + 1`：放大到自然大小。

### Options：

**backdrop**：是否启用模态背景

- 作用：。

- Type: `Boolean` or `String`
- Default: `true`

**button**：是否显示查看器右上角的关闭按钮

- Type: `Boolean`
- Default: `true`

**navbar**：指定导航栏的可见性

- Type: `Boolean` or `Number`
- Default: `true`
- Options:
  - `0` or `false`:  隐藏
  - `1` or `true`:  显示
  - `2`: 仅在屏幕宽度大于 768 像素时显示
  - `3`:  仅在屏幕宽度大于 992像素时显示
  - `4`:  仅在屏幕宽度大于 1200像素时显示

**title**：指定图片标题的可见性和内容

- Type: `Boolean` or `Number` or `Function` or `Array`
- Default: `true`
- Options:
  - `0` or `false`:  隐藏
  - `1` or `true`or `Function` or `Array`:  显示
  - `2`: 仅在屏幕宽度大于 768 像素时显示
  - `3`:  仅在屏幕宽度大于 992像素时显示
  - `4`:  仅在屏幕宽度大于 1200像素时显示
  - `Function`: 自定义标题内容
  - `[Number, Function]`:  Number表示可见性，Function自定义标题内容

> 该名称来自`alt`图像元素的属性或从其 URL 解析的图像名称。

```js
new Viewer(image, {
  title: [4, (image, imageData) => {
  	return `${image.alt} (${imageData.naturalWidth} × ${imageData.naturalHeight})`
  }]
});
```

**toolbar**：指定工具栏及其按钮的可见性和布局

- Type: `Boolean` or `Number` or `Object`
- Default: `true`
- Options:
  - `0` or `false`:  隐藏
  - `1` or `true`:  显示
  - `2`: 仅在屏幕宽度大于 768 像素时显示
  - `3`:  仅在屏幕宽度大于 992像素时显示
  - `4`:  仅在屏幕宽度大于 1200像素时显示
  - `{ key: Boolean | Number }`: 显示或隐藏工具栏
  - `{ key: String }`: 自定义按钮的大小
  - `{ key: Function }`: 自定义按钮的点击处理程序
  - `{ key: { show: Boolean | Number, size: String, click: Function }`: 自定义按钮的每个属性
  - 可用的内置键："zoomIn", "zoomOut", "oneToOne", "reset", "prev", "play", "next", "rotateLeft", "rotateRight", "flipHorizontal", "flipVertical"
  - 可用的内置尺寸："small", "medium" (default) and "large"

```js
new Viewer(image, {
  toolbar: {
    zoomIn: 4,		// 放大
    zoomOut: 4,		// 缩小
    oneToOne: 4,
    reset: 4,		// 重置
    prev: 4,		// 上一张
    play: {			// 播放
      show: 4,
      size: 'large',
    },
    next: 4,			// 下一张
    rotateLeft: 4,		// 向左旋转
    rotateRight: 4,		// 向右旋转
    flipHorizontal: 4,	// 水平翻转
    flipVertical: 4,	// 垂直翻转
    // 自定义工具栏
    download: function() {
      const a = document.createElement('a');
      a.href = viewer.image.src;
      a.download = viewer.image.alt;
      document.body.appendChild(a);
      a.click();
      document.body.removeChild(a);
    }
  },
});
```

自定义工具栏需要引入对应的图标文字：iconfont需要下载Unicode类型

```html
<link rel="stylesheet" href="css/font/iconfont.css">
<style>
.viewer-download {
  color: #fff;
  font-family: FontAwesome, serif;
  font-size: 0.75rem;
  line-height: 1.5rem;
  text-align: center;
}
.viewer-download:before {
  content:"\e600";
  font-family: "iconfont" !important;
  font-size: 16px;
}
</style>
```

**className**：添加到查看器根元素的自定义类名

- Type: `String`
- Default: `''`

**container**：将查看器置于模态模式的容器。

- Type: `Element` or `String`
- Default: `'body'`
- `Document.querySelector`的元素或有效选择器

> 注：仅在`inline`选项设置为时可用`false`；

**filter**：过滤图像以供查看（`true`如果图像可见，则应返回，返回`false`忽略图像）

- Type: `Function`
- Default: `null`

```js
new Viewer(image, {
  filter(image) {
    return image.complete;
  },
});
```

**fullscreen**：表示是否在播放时请求全屏

- Type: `Boolean` or [`FullscreenOptions`](https://developer.mozilla.org/en-US/docs/Web/API/FullscreenOptions)
- Default: `true

> 要求浏览器支持 [Fullscreen API](https://caniuse.com/fullscreen).

**inheritedAttributes**：定义要从原始图像继承的额外属性

- Type: `Array`
- Default: `['crossOrigin', 'decoding', 'isMap', 'loading', 'referrerPolicy', 'sizes', 'srcset', 'useMap']`

> 请注意，基本属性`src`将`alt`始终从原始图像继承。

**initialViewIndex**：定义要查看的图像的初始索引

- Type: `Number`
- Default: `0`

**inline**：启用内联模式

- Type: `Boolean`
- Default: `false

**interval**：播放时自动循环图像之间的延迟时间

- Type: `Number`
- Default: `5000

**keyboard**：启用键盘支持

- Type: `Boolean`
- Default: `true

**focus**：初始化时聚焦导航栏中的活动项

- Type: `Boolean`
- Default: `true`

**loading**：指示在加载图像时是否显示加载微调器

- Type: `Boolean`
- Default: `true`

**loop**：是否启用循环查看

- Type: `Boolean`
- Default: `true`

**minWidth**：定义查看器的最小宽度

- Type: `Number`
- Default: 200

> 仅在内联模式下可用（将`inline`选项设置为`true`）

**minHeight**：定义查看器的最小高度

- Type: `Number`
- Default: 100

> 仅在内联模式下可用（将`inline`选项设置为`true`）

**movable**：可移动图像

- Type: `Boolean`
- Default: `true

**rotatable**：可旋转图像

- Type: `Boolean`
- Default: `true`

**scalable**：可翻转

- Type: `Boolean`
- Default: `true`

**zoomable**：可缩放

- Type: `Boolean`
- Default: `true`

**zoomOnTouch**：通过在触摸屏上拖动来缩放当前图像

- Type: `Boolean`
- Default: `true

**zoomOnWheel**：通过滚动鼠标来缩放图像

- Type: `Boolean`
- Default: `true`

slideOnTouch：通过在触摸屏上滑动来滑动到下一个或上一个图像

- Type: `Boolean`
- Default: `true`

Enable to slide to the next or previous image by swiping on the touch screen.

**toggleOnDblclick**：双击图像时在其自然大小和初始大小之间切换图像大小

- Type: `Boolean`
- Default: `true`

换句话说，[`toggle`](https://github.com/fengyuanchen/viewerjs#toggle)双击图像时自动调用该方法。

> 需要[`dblclick`](https://developer.mozilla.org/en-US/docs/Web/Events/dblclick)事件支持。

**tooltip**：放大或缩小时显示带有图像比例（百分比）的工具提示

- Type: `Boolean`
- Default: `true`

**transition**：启用 CSS3 过渡

- Type: `Boolean`
- Default: `true`

**zIndex**：在模态模式下定义查看器的 CSS`z-index`值

- Type: `Number`
- Default: `2015`

**zIndexInline**：在内联模式下定义查看器的 CSS`z-index`值

- Type: `Number`
- Default: `0`

**zoomRatio**：缩放比例

- Type: `Number`
- Default: `0.1`

**minZoomRatio**：最小缩放比例

- Type: `Number`
- Default: `0.01`

**maxZoomRatio**：最大缩放比例

- Type: `Number`
- Default: `100`

**url**：获取原始图像的URL

- Type: `String` or `Function`
- Default: `'src'`

> 如果它是一个字符串，它应该是每个图像元素的属性之一。如果它是一个函数，它应该返回一个有效的图像 URL

```html
<img src="picture.jpg?size=160">
```

```js
new Viewer(image, {  url(image) {    return image.src.replace('?size=160', '');  },});
```

**ready**：回调函数

- Type: `Function`
- Default: `null`

**show**：

- Type: `Function`
- Default: `null`

**shown**：

- Type: `Function`
- Default: `null`

**hide**：

- Type: `Function`
- Default: `null`

**hidden**：

- Type: `Function`
- Default: `null`

**view**：

- Type: `Function`
- Default: `null`

**viewed**：

- Type: `Function`
- Default: `null`

**move**：

- Type: `Function`
- Default: `null`

**moved**：

- Type: `Function`
- Default: `null`

**rotate**：

- Type: `Function`
- Default: `null`

**rotated**：

- Type: `Function`
- Default: `null`

**scale**：

- Type: `Function`
- Default: `null`

**scaled**：

- Type: `Function`
- Default: `null`

**zoom**：

- Type: `Function`
- Default: `null`

**zoomed**：

- Type: `Function`
- Default: `null`

**play**：

- Type: `Function`
- Default: `null`

**stop**：

- Type: `Function`
- Default: `null`

### Methods：

**show([immediate])**：显示查看器

- immediate(optional):
  - Type: `Boolean`
  - Default: `false`
  - 指示是否立即显示查看器

> 仅在模态模式下可用。

**hide([immediate])**：隐藏查看器

- immediate(optional):
  - Type: `Boolean`
  - Default: `false

> 仅在模态模式下可用。

**view([index])**：查看带有图像索引的图像之一。如果查看器被隐藏，它将首先显示

- index(optional):
  - Type: `Number`
  - Default: `0` (从`initialViewIndex`选项继承)
  - 供查看的图像索引

```
viewer.view(1); // View the second image
```

**prev([loop=false])**：查看上一张图片

- loop(optional):
  - Type: `Boolean`
  - Default: `false`

**next([loop=false])**：查看下一张图片

- loop(optional):
  - Type: `Boolean`
  - Default: `false`

**move(x[, y = x])**：使用相对偏移量移动图像

- **x**：水平方向的移动距离
  - Type: `Number`
- **y**： (可选)垂直方向的移动距离，如果不存在，则其默认值为`x`
  - Type: `Number

```js
viewer.move(1);viewer.move(-1, 0); // Move leftviewer.move(1, 0);  // Move rightviewer.move(0, -1); // Move upviewer.move(0, 1);  // Move down
```

**moveTo(x[, y = x])**：将图像移动到指定位置

- **x**：水平方向的新位置
  - Type: `Number`
- **y**： (可选)垂直方向的新位置，如果不存在，则其默认值为`x`
  - Type: `Number`

**rotate(degree)**：以相对角度旋转图像

- degree：角度值，大于0向左旋转，小于0向右旋转
  - Type: `Number`

Rotate the image with a relative degree.

```js
viewer.rotate(90);viewer.rotate(-90);
```

**rotateTo(degree)**：将图像旋转到绝对角度

- degree:
  - Type: `Number`

```js
viewer.rotateTo(0); // Reset to zero degreeviewer.rotateTo(360); // Rotate a full round
```

**scale(scaleX[, scaleY])**：

- **scaleX**: 水平翻转
  - Type: `Number`
  - Default: `1`
  - When equal to `1` it does nothing.
- **scaleY**:  垂直翻转，如果不存在，则其默认值为`scaleX`
  - Type: `Number`

```js
viewer.scale(-1); // 水平和垂直翻转viewer.scale(-1, 1); // 水平翻转viewer.scale(1, -1); // 垂直翻转
```

**scaleX(scaleX)**：水平翻转

- scaleX:
  - Type: `Number`
  - Default: `1`

```js
viewer.scaleX(-1); // Flip horizontal
```

**scaleY(scaleY)**：垂直翻转

- scaleY:
  - Type: `Number`
  - Default: `1`

```js
viewer.scaleY(-1); // Flip vertical
```

**zoom(ratio[, hasTooltip])**：以相对比例缩放图像

- **ratio**: 大于0放大，小于0缩小
  - Type: `Number`
- **hasTooltip** (optional): 是否提示缩放比例
  - Type: `Boolean`
  - Default: `false`

**zoomTo(ratio[, hasTooltip])**：将图像缩放到绝对比例

- **ratio**:
  - Type: `Number`
  - 一个正数（比率 > 0）
- **hasTooltip** 

```js
viewer.zoomTo(0); // 缩放到零尺寸 (0%)viewer.zoomTo(1); // 缩放到自然大小 (100%)
```

**play([fullscreen])**：播放图像

- fullscreen(optional): 表示是否请求全屏
  - Type: `Boolean` or [`FullscreenOptions`](https://developer.mozilla.org/en-US/docs/Web/API/FullscreenOptions)
  - Default: `false`

**stop()**：停止播放

**full()**：进入模态模式。

> 仅在内联模式下可用。

**exit()**：退出模态模式。

> 仅在内联模式下可用。

**tooltip()**：按百分比显示图像的当前比例。

> 需要将`tooltip`选项设置为`true`。

**toggle()**：在当前大小和自然大小之间切换图像大小。

> 由[`toggleOnDblclick`](https://github.com/fengyuanchen/viewerjs#toggleOnDblclick)选项使用。

**reset()**：将图像重置为其初始状态

**update()**：当源图像更改（添加、删除或排序）时更新查看器实例。

> 如果动态加载图像（使用 XMLHTTPRequest），可以使用此方法将新图像添加到查看器实例

**destroy()**：销毁查看器并移除实例



### Event:

所有事件都可以`this.viewer`在其处理程序中访问查看器实例。

#### ready

- **event.bubbles**: `true`
- **event.cancelable**: `true`
- **event.detail**: `null`

当查看器实例准备好查看时触发此事件

> 在模态模式下，只有单击其中一张图像才会触发此事件

#### show

- **event.bubbles**: `true`
- **event.cancelable**: `true`
- **event.detail**: `null`

当查看器模式开始显示时触发此事件

> 仅在模态模式下可用。

#### shown

- **event.bubbles**: `true`
- **event.cancelable**: `true`
- **event.detail**: `null`

当查看器模式显示时触发此事件

> 仅在模态模式下可用。

#### hide

- **event.bubbles**: `true`
- **event.cancelable**: `true`
- **event.detail**: `null`

当查看器模式开始隐藏时触发此事件

> 仅在模态模式下可用。

#### hidden

- **event.bubbles**: `true`
- **event.cancelable**: `false`
- **event.detail**: `null`

当查看器模式隐藏时触发此事件

> 仅在模态模式下可用。

#### view

- **event.bubbles**: `true`
- **event.cancelable**: `true`
- **event.detail.index**:原始图像的索引
  - Type: `Number`
- **event.detail.image**:
  - Type: `HTMLImageElement`
  - The current image (a clone of the original image).
- **event.detail.originalImage**: 当前图像（原始图像的克隆）
  - Type: `HTMLImageElement`

当查看器开始显示（查看）图像时会触发此事件

#### viewed

- **event.bubbles**: `true`
- **event.cancelable**: `false`
- **event.detail**: 与`view`事件相同

当查看者显示（查看）图像时触发此事件

#### move

- **event.bubbles**: `true`
- **event.cancelable**: `true`
- **event.detail.x**: 水平方向的新位置
  - Type: `Number`
- **event.detail.y**: 垂直方向的新位置
  - Type: `Number`
- **event.detail.oldX**: 水平方向的旧位置
  - Type: `Number`
- **event.detail.oldY**: 垂直方向的旧位置
  - Type: `Number`
- **event.detail.originalEvent**:
  - Type: `Event` or `null`
  - Options: `pointermove`, `touchmove`, and `mousemove`.

当查看器开始移动图像时会触发此事件

#### moved

- **event.bubbles**: `true`
- **event.cancelable**: `false`
- **event.detail**: 与`move`事件相同

当移动图像时触发此事件

#### rotate

- **event.bubbles**: `true`
- **event.cancelable**: `true`
- **event.detail.degree**: 新的旋转度数
  - Type: `Number`
- **event.detail.oldDegree**: 旧的旋转度数
  - Type: `Number`

当查看器开始旋转图像时触发此事件

#### rotated

- **event.bubbles**: `true`
- **event.cancelable**: `false`
- **event.detail**: 与`rotate`事件相同

当查看器旋转完图像时触发此事件

#### scale

- **event.bubbles**: `true`
- **event.cancelable**: `true`
- **event.detail.scaleX**:
  - Type: `Number`
- **event.detail.scaleY**:
  - Type: `Number`
- **event.detail.oldScaleX**:
  - Type: `Number`
- **event.detail.oldScaleY**:
  - Type: `Number`

当查看器开始翻转图像时会触发

#### scaled

- **event.bubbles**: `true`
- **event.cancelable**: `false`
- **event.detail**: 与`scale`事件相同.

#### zoom

- **event.bubbles**: `true`
- **event.cancelable**: `true`
- **event.detail.ratio**: 图像的新（下一个）比例 ( `imageData.width / imageData.naturalWidth`)
  - Type: `Number`
- **event.detail.oldRatio**: 图像的旧（当前）比率
  - Type: `Number`
- **event.detail.originalEvent**:
  - Type: `Event` or `null`
  - Options: `wheel`, `pointermove`, `touchmove`, and `mousemove`.

当查看器开始放大（放大或缩小）图像时触发此事件

#### zoomed

- **event.bubbles**: `true`
- **event.cancelable**: `false`
- **event.detail**: 与`zoom`事件相同

#### play

- **event.bubbles**: `true`
- **event.cancelable**: `true`
- **event.detail**: `null`

当查看器开始播放时触发此事件

> 可以通过调用 中止播放过程`event.preventDefault()`

#### stop

- **event.bubbles**: `true`
- **event.cancelable**: `true`
- **event.detail**: `null`

当查看器开始停止时触发此事件

> 可以通过调用来中止停止过程`event.preventDefault()`



### No conflict

如果必须使用具有相同命名空间的另一个查看器，请调用`Viewer.noConflict`静态方法来恢复它

```js
<script src="other-viewer.js"></script><script src="viewer.js"></script><script>  Viewer.noConflict();  // Code that uses other `Viewer` can follow here.</script>
```

