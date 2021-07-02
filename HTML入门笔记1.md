## 目录：
1. HTML 是谁发明的
2. HTML 起手应该写什么
3. 常用的表章节的标签有哪些，分别是什么意思（h1~h6、section、article、main、aside 等等）
4. 全局属性有哪些
5. 常用的内容标签有哪些，分别是什么意思（a、strong、em、code、pre 等等）

## 正文：
1. HTML 是 Tim Berners Lee 发明的。
2. HTML 起手应该写 感叹号+tab，得到一个如下的模板，然后就可以在 body 元素中写代码啦。
```
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>
  <body></body>
</html>
```
3. 常用表示章节的标签及含义如下：
* 标题 h1~h6
* 章节 section
* 文章 article
* 段落 p
* 头部 header
* 尾部 footer
* 主要内容 main
* 旁支内容 aside
* 划分 div

4. 全局属性有如下这些：
* class
* id
* contenteditable
* hidden
* style
* tabindex
* title

5. 常用表示内容的标签及含义如下：
* ul li 无序列表
* ol li 有序列表
* dl dt dd  描述性列表
* pre code  前者表示保留空格、回车、tab，后者表示输入的是代码。这俩经常一起使用，因为代码显示出来时，为了格式好看，最好保留、空格、换行、tab。
* hr 分割线
* br 换行
* a 超链接
* em strong 前者表示语气上强调，后者表示真的很重要
* quote blockquote  前者表示引用，但没有任何样式改变，后者表示块引用，会换行。

