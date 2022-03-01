Map 对象是键值对集合，和 JSON 对象类似，但是 key 不仅可以是字符串还可以是对象。

Set 对象类似于数组，且成员的值都是唯一的。

## JS中Set、Map的区别：

**共同点**：Map 和 Set 都不允许键重复

**不同点**：

- 初始化需要的值不一样，Map需要的是一个二维数组，而Set 需要的是一维 Array 数组；
- Map的键是不能修改，但是键对应的值是可以修改的；Set不能通过迭代器来改变Set的值，因为Set的值就是键。
- Map 是键值对的存在，值也不作为健；而 Set 没有 value 只有 key，value 就是 key；

## Map

JavaScript 中的对象（Object），本质上是键值对的集合，但是只能用字符串来做键名，在使用上有很大的限制；

为了解决这个问题，ES6 提供了Map数据结构。它类似于对象，也是键值对的集合，但是“键”的范围不限于字符串，各种类型的值（包括对象、数字、数组等）都可以当作键

**总结：Object 结构提供了“字符串 - 值”的对应，Map 结构提供了“值 - 值”的对应，是一种更完善的 JSON 数据结构的实现**

**特性：键值对=>任意类型=>更好的处理有映射需求的问题。**

### 创建Map：

Map本身时一个构造函数，使用构造函数进行数据初始化；

```js
let m = new Map();
```

Map 函数可以接受一个数组作为参数，用来进行初始化。但是跟 Set 不同的是，Map 中该数组中的成员是一对对表示键值对的数组（或有点类似数组的对象）

```js
let m1 = new Map([["name", "zhangsan"], ["age", 20]]);
let m2 = new Map([{0:"name",1:"zhangsan"},{"0":"age","1":20}]);
```

### size属性：

返回 Map 实例的成员总数

```js
let m = new Map([["name", "zhangsan"], ["age", 20]]);
console.log( m.size );//2
```

### Map的方法：

#### 操作方法：

set(key, value)　　 添加或修改数据。设置 key 所对应的键值，并返回 Map 结构本身

get(key)　　　　　 获取数据。读取 key 对应的键值，如果找不到 key，返回 undefined

has(key)　　　　　查看是否存在某个数据，返回一个布尔值。

delete(key)　　　　删除数据。删除成功返回 true

clear()　　　　　　清除所有数据，没有返回值

```js
let map = new Map([["name", "zhangsan"], ["age", 20]]);
map.set("name", "lisa"); // Map(2) {"name" => "lisa", "age" => 20}
map.get("name");// lisa
map.has("age"); // true
map.delete("age"); // true
map.clear();
console.log(map); // Map(0) {}
```

#### 遍历方法：

keys()　　　　 返回一个键名的遍历器

values()　　　 返回一个键值的遍历器

entries()　　　 返回一个键值对的遍历器

forEach()　　  使用回调函数遍历每个成员

```js
let num = new Map([["one", 1], ["two", 2], ["three", 3]]);
console.log(num.keys());	// {'one', 'two', 'three'}
console.log(num.values());		// {1, 2, 3}
console.log(num.entries());		// {'one' => 1, 'two' => 2, 'three' => 3}
for(let [key, value] of num.entries()){
     console.log(key, value);
}
// one 1
// two 2
// three 3
num.forEach((value, key) => {
    console.log(value, key)
})
// 1 one
// 2 two
// 3 three
```

### 数据结构转换：

#### Map -> Array：

使用扩展运算符 ... 

```js
let myMap = new Map();
myMap
 .set(true, "真")
 .set(false, "假");//因为每次会返回新Map，可以连着写
console.log(myMap); // {true => "真", false => "假"}
let newMap = [...myMap];
console.log(newMap); // [[true, "真"], [false, "假"]]
```

#### Array -> Map：

将数组传入Map 构造函数中，实现转换；

```js
let arr = [[true, "真"], [false, "假"]];
let map = new Map(arr);
console.log(map); // {true => "真", false => "假"}
```

#### Map -> Object：

前提：如果 Map 所有的键都是字符串，它就可以转为对象；

```js
function strMapToObj(strMap){
     let obj = {};
     for(let [k, v] of strMap){
         obj[k] = v;
     }
     return obj;
}
let myMap = new Map().set("green","绿").set("red","红");
console.log(myMap); // {"green" => "绿", "red" => "红"}
console.log( strMapToObj(myMap) ); // { green: "绿", red: "红" }  
```

#### Object -> Map：

将数组传入Map 构造函数中，实现转换；

```js
function objToStrMap(obj){
    let map = new Map();
    for(let item in obj){
        map.set(item, obj[item]);
    }
    return map;
}
let obj = { green: "绿", red: "红" };
console.log( objToStrMap(obj) );
```

## Set()

ES6 提供了新的数据结构 Set，它类似于数组，但是成员的值都是唯一的，没有重复的值;

特性：唯一性=>不重复=>能够对数据进行去重操作；

**特性：唯一性=>不重复=>能够对数据进行去重操作；**

<!--注：集合去重，是全等匹配，===-->

### 创建Set：

Set本身时一个构造函数，使用构造函数进行数据初始化；

```js
let s = new Set();
```

Set 函数可以接受一个数组（或类似数组的对象）作为参数，用来进行数据初始化;

```js
let s = new Set([1,2,3,4,1]);
console.log(s);	// {1, 2, 3, 4}
```

注：如果初始化时给的值有重复的，会自动去除。集合并没有字面量声明方式。

### size属性：

返回 Set 实例的成员总数

```js
let s = new Set([1, 2, 3]);
console.log( s.size ); // 3
```

### Set的方法：

#### 操作方法：

add(value)　　　　添加数据，并返回新的 Set 结构

delete(value)　　　删除数据，返回一个布尔值，表示是否删除成功

has(value)　　　　查看是否存在某个数据，返回一个布尔值

clear()　　　　　　清除所有数据，没有返回值

```js
let set = new Set([1, 2, 3, 4, 4]);
set.add(5); // Set(5) {1, 2, 3, 4, 5}
set.delete(4); // true
set.has(4);	// false
set.clear();
console.log(set); // Set(0) {}
```

#### 遍历方法：

keys()　　　　 返回一个键名的遍历器

values()　　　 返回一个键值的遍历器

entries()　　　 返回一个键值对的遍历器

forEach()　　　使用回调函数遍历每个成员

## 与数组相关操作：

#### Set -> 数组：

由于扩展运算符...，内部的原理也是使用的 for-of 循环，所以也可以用于操作 Set 结构

```js
let color = new Set(["red", "green", "blue"]);
let colorArr = [...color];
```

#### 数组去重：

扩展运算符和 Set 结构相结合，就可以去除数组的重复成员

#### 扩展：

```js
let num1 = new Set([1, 2, 3, 4]);
let num2 = new Set([3, 4, 5, 6]);

//并集
let union = new Set([...num1,...num2]);
console.log(union);//Set { 1, 2, 3, 4, 5, 6 }

//交集
let intersect = new Set(
    [...num1].filter(x=> num2.has(x))
)
console.log(intersect); //Set { 3, 4 }

//差集
let difference = new Set(
    [...num1].filter(x => !num2.has(x))
)
console.log(difference); //Set { 1, 2 }
```
