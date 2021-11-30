# DOM 事件模型

## 目录

1. 事件捕获
2. 事件冒泡
3. 事件模型

## 正文

### 1.事件冒泡
  
冒泡（bubbling）原理很简单。

当一个事件发生在一个元素上，它会首先运行在该元素上的处理程序，然后运行其父元素上的处理程序，然后一直向上到其他祖先上的处理程序。

几乎所有事件都会冒泡。例如，focus 事件不会冒泡。同样，我们以后还会遇到其他例子。但这仍然是例外，而不是规则，大多数事件的确都是冒泡的。
  
### 2.事件捕获

事件处理的另一个阶段被称为“捕获（capturing）”。它很少被用在实际开发中，但有时是有用的。

### 3.事件模型

DOM 事件标准描述了事件传播的 3 个阶段，可以把这个称为事件模型：

* 捕获阶段（Capturing phase）—— 事件（从 Window）向下走近元素。
* 目标阶段（Target phase）—— 事件到达目标元素。
* 冒泡阶段（Bubbling phase）—— 事件从元素上开始冒泡。

下面是在表格中点击 &lt;td&gt; 的图片，摘自规范：

![image](https://www.w3.org/TR/DOM-Level-3-Events/images/eventflow.svg)

也就是说：点击&lt;td&gt;，事件首先通过祖先链向下到达元素（捕获阶段），然后到达目标（目标阶段），最后上升（冒泡阶段），在途中调用处理程序。

请注意，虽然形式上有 3 个阶段，但第 2 阶段（“目标阶段”：事件到达元素）没有被单独处理：捕获阶段和冒泡阶段的处理程序都在该阶段被触发。

让我们来看看捕获和冒泡：

```
<style>
  body * {
    margin: 10px;
    border: 1px solid blue;
  }
</style>

<form>FORM
  <div>DIV
    <p>P</p>
  </div>
</form>

<script>
  for(let elem of document.querySelectorAll('*')) {
    elem.addEventListener("click", e => alert(`Capturing: ${elem.tagName}`), true);
    elem.addEventListener("click", e => alert(`Bubbling: ${elem.tagName}`));
  }
</script>  
```

上面这段代码为文档中的每个元素都设置了点击处理程序，以查看哪些元素上的点击事件处理程序生效了。

如果你点击了&lt;p&gt;，那么顺序是：

* HTML → BODY → FORM → DIV（捕获阶段第一个监听器）
* P（目标阶段，触发两次，因为我们设置了两个监听器：捕获和冒泡）
* DIV → FORM → BODY → HTML（冒泡阶段，第二个监听器）

