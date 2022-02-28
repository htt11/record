**需求**：从组件1携带参数跳转到组件2中，组件2中获取到相应的参数，并触发相应的事件；

```js
// menu1.vue
this.$router.push({
  name:'menu2',
  params: {
  	id: 1
  }
})
```

```vue
// menu2.vue
<script>
export default {
  ...
  computed: {
    routeParams() {
      return this.$route.params
    }
  },
  watch: {
    routeParams(val) {
      this.onDetail(val)
    }
  },
  methods: {
    onDetail(row) {
      console.log(row)  
    }
  }
}
</script>
```

**遇到的问题**：watch中并没有监听到`routeParams`的变化；

**原因**：

- 首次进入`menu2`组件时，computed中相当于定义了`routeParams`这样一个变量，并将`this.$route.params`赋值给它；
- watch在最初绑定的时候不会执行，要等到`监听的属性`改变时才执行监听函数；
- **computed**是在HTML DOM加载后马上执行的，如赋值；
- 也就是，给`routeParams`变量赋值的过程在watch首次绑定之前，因此当代码顺序执行到watch时，只是对

`routeParams`变量进行了绑定，并没有执行里面的onDetail方法；

**解决**：

方式一：watch在最初绑定`routeParams`时，就执行；

```vue
// menu2.vue
<script>
export default {
  ...
  computed: {
    routeParams() {
      return this.$route.params
    }
  },
  watch: {
    routeParams: {
      obj: {
        handler(val) {
         this.onDetail(val)
        },
        immediate: true		// 立即执行hander
      }
    }
  },
  methods: {
    onDetail(row) {
      console.log(row)  
    }
  }
}
</script>
```

方式二：提前定义一个`routeParams`变量，路由改变时再赋值；
- 在data中先定义一个`routeParams`变量，赋值为‘ ’ ；
- 当跳转时获取到`this.$route.params`，再对`routeParams`变量进行重新赋值；

```vue
// menu2.vue
<script>
export default {
  data() {
    return {
      routeParams: ''    
    }
  },
  mounted() {
    this.routeParams = this.$route.params
  },
  watch: {
    routeParams(val) {
      this.onDetail(val)
    }
  },
  methods: {
    onDetail(row) {
      console.log(row)  
    }
  },
}
</script>
```

方式三：直接在computed中调用`onDetail()`方法

```vue
// menu2.vue
<script>
export default {
  ...
  computed: {
    routeParams() {
      this.onDetail(this.$route.params)
      return this.$route.params
    }
  },
  watch: {
    routeParams: {}		// 解决routeParams属性未被引用不生效问题
  },
  methods: {
    onDetail(row) {
      console.log(row)  
    }
  }
}
</script>
```

新问题：当computed中的`routeconsole.log()Params`属性在视图部分不需要展示时，可能会因未被引用而不生效，并不会执行`this.onDetail()`；

解决：配合watch一起使用 或者 在某处调用一次（如console.log(this.routeconsole)）

```js
watch: {
  routeParams: {}		// 解决routeParams属性未被引用不生效问题
}
```

