## 目录
1. 二者的区别
2. 使用方法
3. 如何在 codesandbox 上写代码

## 正文

### 1. 二者的区别

#### 问题一：为什么要区分完整版和运行时版本？

答：vue 想使用模板语法，但是模板需要翻译成 JS 代码，而这个过程需要编译器完成，编译器很大，最好不要发送给浏览器，否则用户需要花更多时间来下载。
那这个编译的过程就通过 webpack 提前完成，于是，只需要一个更精简的 Vue 即可理解浏览器上的代码，这个精简的 Vue 就不需要包编译器，从而大大提高包含 Vue 语法的代码的下载速度。

#### 问题二：二者有什么区别？

|      | vue完整版| vue非完整版 | 评价 | 
|:------|:------|:------|:------|
| 特点 | 有编译器 | 没有编译器 | 编译器占 40% 的体积 |
| 视图 | 写在 HTML 里或者写在 template 选项中 | 写在 render 函数里，用 h 来创建标签 | h 是尤雨溪写好传给 render 的|
| cdn 引入 | vue.js | vue.runtime.js | 文件名不同，生产环境后缀为 min.js |
| webpack 引入 | 需要配置alias | 默认使用此版本 | 尤雨溪配置的 |
| @vue/cli 引入 | 需要额外配置 | 默认使用此版本 | 尤雨溪、蒋豪群配置的 |

### 2. 使用方法

* 总是使用非完整版，然后配合 vue-loader 和 vue 文件。
* 为了保证用户体验，使用户下载的 JS 文件更小，但问题是这些文件只支持 h 函数，不支持html 模板。
* 为了保证开发体验，让开发者直接在 vue 文件中写 HTML 标签，不写 h 函数。
* 上述两者有冲突，就是开发者不写 h 函数，但是浏览器在 vue 的协助下只认识 h 函数，为了解决这个冲突，写一个 loader，即 vue-loader，它负责把 vue 文件中的 HTML 标签转为 h 函数。

假设已经使用 @vue/cli 配置好了环境。

#### 1. 完整版使用方法：
  
  去 bootcdn 上，搜索 vue，使用 2.6.10 版，具体就使用 vue.min.js 这个版本，这是生产环境下的完整版本，将下面的代码复制到 index.html 中：

```
    <script src="https://cdn.bootcdn.net/ajax/libs/vue/2.6.10/vue.min.js"></script>
  ```

在 index.html 中，不向 div 元素添加一个模板。

```
    <div id="app"></div>
```

  在 main.js 中，添加 template 属性，用 JavaScript 字符串的方式写模板，这就是官网说的，组件模板是内联的 JavaScript 字符串。

```
new Vue({
  el:'#app',
  template:`<div>{{n}}</div>`,
  data:{
    n:0
  }
})
```

此时，页面上显示 0。

#### 2. 非完整版使用方法：

  去 bootcdn 上，搜索 vue，使用 2.6.10 版，具体就使用 vue.runtime.min.js 这个版本，这是生产环境下的非完整版本，将下面的代码复制到 index.html 中：

```
    <script src="https://cdn.bootcdn.net/ajax/libs/vue/2.6.10/vue.runtime.min.js"></script>
```

在 main.js 中写一个 render 函数。

```
new Vue({
  el:'#app',
  render(h){
    return h('div',this.n)
  },
  data:{
    n:0
  }
})
```
 此时，页面上也显示 0。


### 3. 如何在 codesandbox 上写代码

#### 问题一：codsandbox 是什么？

答：codesandbox 是一个免费的创建 demo 的网站，可以实时预览，它已经把写代码要配置的环境都提前配置好了，打开它就可以直接写符合 vue 语法的代码，省去了复杂的配置过程，而且这些代码还可以下载到本地，十分方便。

#### 问题二：如何使用 codesandbox？

1. 搜索进入codesandbox 官网，无论是否登录，都可以在这里创建无限多个项目。
2. 点击右上角的 create sandbox
3. 然后可以选择创建哪种类型的沙盒。比如 vue、react、原生 JavaScript 等等。
4. 然后就可以开始写代码了

这些代码可以下载到本地：

&nbsp;&nbsp;点击左上角的的三条横线——点击 File——Export to ZIP，即可下载到本地

&nbsp;&nbsp;然后查看解压缩后的目录中的 package.json，可以知道怎么运行它。会读 package.json 文件就行。
