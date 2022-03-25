# vuex-persistedstate的使用：

vue项目中，我们常用 vuex 进行状态管理，但存在刷新数据丢失的问题；

vuex-persistedstate可以让vuex中的数据持久保存在sessionstorage或localstorage中，刷新后不会变成初始状态，实现 vuex 的持久化；

**安装：**

```bash
npm install --save vuex-persistedstate
```

**使用：**

```js
// store/index.js
import Vue from 'vue'
import Vuex from 'vuex'
import createPersistedState from 'vuex-persistedstate'
Vue.use(Vuex)
export default new Vuex.Store({
    // ...
    plugins: [createPersistedState()]
})
```

**自定义存储方式：**

- vuex-persistedstate默认使用localStorage来存储数据，如果要使用sessionStorage:

```js
plugins: [createPersistedState({ 
  storage: window.sessionStorage 
})]
```

**指定需要持久化的state：**

- vuex-persistedstate默认持久化所有state；
- 可以配置哪些state需要持久化存储，哪些还是存储在内存里；

```js
state： {
  name: 'zs',
  age: 18
}
// ...
plugins: [createPersistedState({ 
  storage: window.sessionStorage,
  reducer(val) {
    return {
      // 只储存state中的age
      age: val.age
    }
  }
})]
```

**引用多个插件：**

如：vuex提示的插件和持久化的插件一起使用，配置如下

```js
// store/index.js
import Vue from 'vue'
import Vuex from 'vuex'
import createPersistedState from 'vuex-persistedstate'
import createLogger from 'vuex/dist/logger'
// 判断环境 vuex提示生产环境中不使用
const debug = process.env.NODE_ENV !== 'production'

Vue.use(Vuex)
export default new Vuex.Store({
  // ...
  plugins: debug ? [createLogger(), createPersisted] : [createPersisted]
})
```

