# DOM 事件委托

捕获和冒泡允许我们实现一种被称为**事件委托**的强大的事件处理模式。

这个想法是，如果我们有许多以类似方式处理的元素，那么就不必为每个元素分配一个处理程序 —— 而是将单个处理程序放在它们的共同祖先上。

在处理程序中，我们获取 event.target 以查看事件实际发生的位置并进行处理。

让我们看一个示例 —— 反映中国古代哲学的 八卦图。

如下所示：

![image](https://user-images.githubusercontent.com/20218586/144075217-a751e2d0-9f87-4ce3-98bd-dfb46895b3f8.png)

其 HTML 如下所示：

```
<table>
  <tr>
    <th colspan="3"><em>Bagua</em> Chart: Direction, Element, Color, Meaning</th>
  </tr>
  <tr>
    <td class="nw"><strong>Northwest</strong><br>Metal<br>Silver<br>Elders</td>
    <td class="n">...</td>
    <td class="ne">...</td>
  </tr>
  <tr>...2 more lines of this kind...</tr>
  <tr>...2 more lines of this kind...</tr>
</table>  
```

该表格有 9 个单元格（cell），但可以有 99 个或 9999 个单元格，这都不重要。

我们的任务是在点击时高亮显示被点击的单元格 &lt;td&gt;。

与其为每个&lt;td&gt;（可能有很多）分配一个 onclick 处理程序 —— 我们可以在&lt;table&gt; 元素上设置一个“捕获所有”的处理程序。

它将使用 event.target 来获取点击的元素并高亮显示它。

```
let selectedTd;

table.onclick = function(event) {
  let target = event.target; // 在哪里点击的？

  if (target.tagName != 'TD') return; // 不在 TD 上？那么我们就不会在意

  highlight(target); // 高亮显示它
};

function highlight(td) {
  if (selectedTd) { // 移除现有的高亮显示，如果有的话
    selectedTd.classList.remove('highlight');
  }
  selectedTd = td;
  selectedTd.classList.add('highlight'); // 高亮显示新的 td
}
```

此代码不会关心在表格中有多少个单元格。我们可以随时动态添加/移除 &lt;td&gt;，高亮显示仍然有效。
