## null 和 underfined ：

### underfined：

underfined 类型只有一个值，即特殊的 underfined；

只声明变量但未对其加以初始化时，这个变量会被自动赋值为 underfined；

```js
var name;
console.log(name);		// underfined
```

```js
var name = underfined;
console.log(name == underfined);		// true
```

这个例子使用 underfined 值 显式初始化了变量，但是一般不需要显式地把一个变量设置为 underfined，因为未经初始化的值默认会取得 underfined 值；

字面量 underfined 的主要目的是在于比较，而ECMA-262第3版之前的版本中并没有规定这个值，第3版之后引入这个值是为了正式区分空队象指针和未经初始化的变量；

但包含 underfined 值的变量和尚未定义的变量还是不一样的：

```js
var name;				// 声明后默认取得了underfined值
console.log(name);		// underfined
console.log(age);		// 报错

console.log(typeof name);	// underfined
console.log(typeof age);	// underfined
```

### null：

null类型也只有一个值，即特殊的null；

从逻辑角度来说null是一个空指针对象，这也是使用typeof操作符检测null值时返回"object"的原因；

如果定义的变量准备在将来用于保存对象，那么最好将该变量初始化为null而不是其他值；这样一来只要检查null值就可以知道相应的变量是否已经保存了一个对象的引用：

```js
if (car != null) {
    // 对call对象执行某些操作
}
```



### 对比：

使用typeof操作符进行检测：

```js
typeof null				// object
typeof underfined		// underfined
```

**实际上，underfined 值是派生自 null 值的，因此ECMA-262规定对它们的相等性测试要返回 true：**

```js
alert(underfined == null);		// true
```

这里，位于 null 和 underfined 之间的相等操作符（==）总会返回true，不过需要注意的是，这个操作符出于比较的目的会转换其操作数。

尽管 null 和 underfined 有这样的关系，但它们的用途完全不同。因此：

- 无论在什么情况下都没有必要把一个变量的值显式地设置为underfined；
- 而对于null，只要意在保存对象的变量还没有真正保存对象，就应该明确地让该变量保存null值；
- 这样做不仅可以体现null作为空对象指针的惯例，而且也有助于进一步区分 null 和 underfined；
