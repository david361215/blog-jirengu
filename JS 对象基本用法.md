# JS 对象基本用法

## 目录
1. 声明对象的两种语法
2. 如何删除对象的属性
3. 如何查看对象的属性
4. 如何修改或增加对象的属性
5. 'name' in obj和obj.hasOwnProperty('name') 的区别

## 正文

### 1.声明对象的两种语法

`let obj = { 'name': 'frank', 'age': 18 }`

`let obj = new Object({'name': 'frank'})`

`console.log({ 'name': 'frank, 'age': 18 })`

第二种是正规写法，但是大部分人用第一种写法。

第三种是匿名对象。

### 2.如何删除对象的属性

```
var obj = { 'name':'frank', 'age':18}
obj.name = undefined 
```

此时打印出 obj，是这样：

`obj = { 'name':undefined, 'age':18 }`

```
var obj = { 'name':'frank', 'age':18}
delete obj.name 或者 delete obj['name']
```

此时打印出 obj，是这样：

`obj = { 'age':18 }`

delete 删除了整个属性。设置为 undefined 只是删除了属性值。

'name' in obj 如果返回 false，表示删除成功，否则删除失败。一定要加引号.

### 3.如何查看对象的属性

1、查看所有属性（读属性）

查看自身所有属性

`Object.keys(obj)`

类似的还有 Object.values、Object.entries 含义分别是查看所有属性值，查看所有键值对。

查看自身+共有属性

`console.dir(obj)`

或者自己依次用 Object.keys 打印出 obj.__proto__。（但是这种方式不推荐，因为不同浏览器对于 __proto__ 的命名可能不同，这既然是一个隐藏属性，JS 是不建议直接访问的）

判断一个属性是自身的还是共有的

`obj.hasOwnProperty('toString')`

2、查看某个属性

三种方法查看属性

中括号语法：`obj['key']` 

点语法：`obj.key`

坑新人语法：`obj[key] // 变量 key 值一般不为 'key'`

请优先使用中括号语法，点语法会误导你，让你以为 key 不是字符串，等你确定不会弄混两种语法，再改用点语法

obj.name 等价于 obj['name']

obj.name 不等价于 obj[name]

简单来说，这里的 name 是字符串，而不是变量。

`let name = 'frank'`

obj[name] 等价于 obj['frank']，而不是 obj['name'] 和 obj.name

这里 name 是变量。

### 4.如何修改或增加对象的属性

1、直接赋值

`let obj = {name: 'frank'} // name 是字符串`

`obj.name = 'frank' // name 是字符串`

`obj['name'] = 'frank' `

`obj[name] = 'frank' // 错，因 name 值不确定`

`obj['na'+'me'] = 'frank'`

```
let key = 'name'; 
obj[key] = 'frank'
```

```
let key = 'name'; 
obj.key = 'frank' // 错
```

因为 obj.key 等价于 obj['key']

2、批量赋值

`Object.assign(obj, {age: 18, gender: 'man'})`

3、修改或增加共有属性

无法通过自身修改或增加共有属性

```
let obj = {}, obj2 = {} // 共有 toString
obj.toString = 'xxx' //只会在 obj 改自身属性
obj2.toString  //还是在原型上
```

我偏要修改或增加原型上的属性，也能做到，但是一般来说，不要修改原型，会引起很多问题

```
obj.__proto__.toString = 'xxx' // 不推荐用 __proto__
Object.prototype.toString = 'xxx' 
``` 

程序员可以随时毁掉整个 JS 的对象体系，但是没法阻止这种行为。这是 JS 脆弱的一面。

### 5.'name' in obj 和 obj.hasOwnProperty('name') 的区别

obj.hasOwnProperty('name')  //判断一个属性是否存在，以及是自身的还是共有的

in 操作符只判断有没有某个属性，不会区分属性是自身的，还是共有的。
