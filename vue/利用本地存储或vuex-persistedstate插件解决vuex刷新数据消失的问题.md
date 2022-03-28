## vuex刷新数据消失的问题：

vuex可以进行全局的状态管理，但刷新后数据会消失；

解决：1.结合本地存储做到数据持久化；2.利用插件 vuex-persistedstate;

### 1. 利用HTML5本地存储：

**方法**：

- vuex的state在localStorage或sessionStorage或其它存储方式中取值
- 在mutations,定义的方法里对vuex的状态操作的同时对存储也做对应的操作。 这样state就会和存储一起存在并且与vuex同步

**问题**：手动写比较麻烦

### 2. 利用插件 vuex-persistedstate
vuex-persistedstate可以让vuex中的数据持久保存在sessionstorage或localstorage中，刷新后不会变成初始状态，实现 vuex 的持久化；

**原理**：结合了存储方式,只是统一的配置就不需要手动每次都写存储方法

**安装**：`npm install vuex-persistedstate --save`

**配置**：

```js
// store/index.js
import createPersistedState from "vuex-persistedstate"
const store = new Vuex.Store({
  // ...
  plugins: [createPersistedState()]
})
```

**默认存储到localStorage**

- #### 指定存储在sessionStorage：

```js
// store/index.js
import createPersistedState from "vuex-persistedstate"
const store = new Vuex.Store({
  // ...
  plugins: [createPersistedState({
      storage: window.sessionStorage
  })]
})
```

**默认持久化所有state**

- #### 指定需要持久化的state：

```js
// store/index.js
import createPersistedState from "vuex-persistedstate"
const store = new Vuex.Store({
  // ...
  plugins: [createPersistedState({
      storage: window.sessionStorage,
      reducer(val) {
          return {
          // 只储存state中的assessmentData
          assessmentData: val.assessmentData
        }
     }
}]
```

- #### vuex引用多个插件

  例如：vuex提示的插件和持久化的插件一起使用，配置如下：

  ```js
  import createPersistedState from "vuex-persistedstate"
  import createLogger from 'vuex/dist/logger'
  // 判断环境 vuex提示生产环境中不使用
  const debug = process.env.NODE_ENV !== 'production'
  const createPersisted = createPersistedState({
    storage: window.sessionStorage
  })
  export default new Vuex.Store({
   // ...
    plugins: debug ? [createLogger(), createPersisted] : [createPersisted]
  }]
  ```

  <!--注：plugins要是一个一维数组，不然会解析错误-->







