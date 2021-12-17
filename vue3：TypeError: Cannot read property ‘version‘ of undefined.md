学习vue3项目，练习的时候因为觉得eslint不需要。就给删除了，然后后面再次安装依赖，准备运行项目时，出现了以下报错:

```
ERROR  TypeError: Cannot read property 'version' of undefined
TypeError: Cannot read property 'version' of undefined
    at module.exports (E:\Vue3\vue3_ts_cms\node_modules\@vue\cli-plugin-eslint\index.js:20:27)
    at E:\Vue3\vue3_ts_cms\node_modules\@vue\cli-service\lib\Service.js:78:7
    at Array.forEach (<anonymous>)
    at Service.init (E:\Vue3\vue3_ts_cms\node_modules\@vue\cli-service\lib\Service.js:76:18)
    at Service.run (E:\Vue3\vue3_ts_cms\node_modules\@vue\cli-service\lib\Service.js:215:10)
    at Object.<anonymous> (E:\Vue3\vue3_ts_cms\node_modules\@vue\cli-service\bin\vue-cli-service.js:36:9)
    at Module._compile (internal/modules/cjs/loader.js:1072:14)
    at Object.Module._extensions..js (internal/modules/cjs/loader.js:1101:10)
    at Module.load (internal/modules/cjs/loader.js:937:32)
    at Function.Module._load (internal/modules/cjs/loader.js:778:12)
PS E:\Vue3\vue3_ts_cms> vue -V
@vue/cli 4.5.13
```

后面重新使用npm install eslint 安装eslint ，然后重新安装依赖npm install ,在次使用npm run serve
