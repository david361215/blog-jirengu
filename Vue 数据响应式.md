## 目录
1. 什么是数据响应式，它解决了什么问题
2. 数据响应式是怎么实现的
3. 数据响应式的优点
4. 数据响应式的缺点，如何解决这些缺点

## 正文

### 1.什么是数据响应式，它解决了什么问题

数据响应式，就是 Vue 对作为 data 的属性的各种对象，做了监听和代理。

这样一来，当这些数据发生改变时，Vue 能够及时发现这些改变，从而渲染 UI。

### 2.数据响应式是怎么实现的

Vue2 通过 Object.defineProperty 来实现数据响应式

大致流程如下（源码不一定这么写，但是思想是一致的）：
  1. 将传入对象的 data 属性，赋值给函数的 data 变量，这个变量就保存着一个匿名对象。
  2. 对这个匿名对象的每个属性，都重写为访问器属性。
  3. 这样，就实现了对匿名对象的每个属性的监听，也就是对这个对象每个属性的修改，都在掌控之中。
  4. 为匿名对象设置代理对象，这个代理对象具有和匿名对象每个属性都相同的属性名，它的属性值都是访问器属性。
  5. 返回代理对象

之后，对 myData 对象的属性的读写，全权由另一个代理对象负责。

```
let myData = {n:0}
let data = proxy({ data:myData }) // 括号里是匿名对象，无法访问

function proxy({data}){
  // 这里的 'n' 写死了，理论上应该遍历 data 的所有 key，这里做了简化
  let value = data.n
  Object.defineProperty(data, 'n', {
    get(){
      return value
    },
    set(newValue){
      if(newValue<0)return
      value = newValue
    }
  })
  // 就加了上面几句，这几句话会监听 data

  const obj = {}
  Object.defineProperty(obj, 'n', {
    get(){
      return data.n
    },
    set(value){
      data.n = value
    }
  })
  
  return obj // obj 就是代理
}
// data 就是 obj
console.log(`需求：${data.n}`)
myData.n = -1
console.log(`需求：${data.n}，设置为 -1 失败了`)
myData.n = 1
console.log(`需求：${data.n}，设置为 1 成功了`)
```
控制台显示如下：

![image](https://user-images.githubusercontent.com/20218586/171553076-c7ef9d9a-97c0-4882-86db-cd2eb60f6eb0.png)

### 3. 数据响应式的优点

可以避免冗长的 DOM 操作，只需要直接修改数据，那么 UI 会自动更新。

### 4.数据响应式的缺点，如何解决这些缺点

不熟悉数据响应式特点的程序员，可能会误操作。举个例子，说明使用 data 容易出问题的方式。 

例子：如果是在声明 data 选项完毕后，才成为 data 选项中对象的属性，那么需要使用 set 来完成对新属性的监听和代理。或者一开始就把属性写好，否则 Vue 是不会触发 UI 更新的。

比如下面的代码，向 data 选项的 obj 对象添加了属性 b，那么 {{obj.b}} 会把属性 b 的内容显示出来么？答案是不会。因为 Vue 没法监听一开始不存在的 obj.b。

```
import Vue from "vue/dist/vue.js";
Vue.config.productionTip = false;
new Vue({
  data: {
    obj: {
      a: 0 // obj.a 会被 Vue 监听 & 代理
    }
  },
  template: `
    <div>
      {{obj.b}}
      <button @click="setB">set b</button>
    </div>
  `,
  methods: {
    setB() {
      this.obj.b = 1; //请问，页面中会显示 1 吗？
    }
  }
}).$mount("#app");

```

怎么办？

1. 把 key 都提前声明好，后面不再增加新的 key。
2. 使用 Vue.set 或者 this.$set。把 setB 方法改成下面这样。Vue.set 和 this.$set 是一样的。 

```
    setB() {
       Vue.set(this.obj,'b',1)
       this.$set(this.obj,'b',1)
    }
```
