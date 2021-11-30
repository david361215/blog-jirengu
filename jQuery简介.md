# jQuery 简介

jQuery 最基础的概念，就是获取一些元素，然后对其进行操作。

## 目录
1. jQuery 如何获取元素
2. jQuery 如何创建元素
3. jQuery 的链式操作是怎样的
4. jQuery 如何移动元素
5. jQuery 如何修改元素的属性

## 正文

### 1.jQuery 如何获取元素

jQuery 支持大部分 CSS3 选择器，也支持一些非标准的选择器。
```
$( "#myId" ); // 通过 ID 选择元素

$( ".myClass" );  // 通过类名选择元素

$( "input[name='first_name']" );  // 通过属性选择元素

$( "#contents ul.people li" );  // 通过复杂的选择器选择元素

$( "div.myClass, ul.people" );  // 通过逗号分隔的多个选择器选择元素

$( "a.external:first" );  //  通过伪选择器选择元素

$( "tr:odd" );  // 通过伪选择器选择元素
```
### 2.jQuery 如何创建元素

jQuery 提供平凡但优雅的方式来创建元素。
```
// 根据 HTML 字符串创建新的元素

$( "<p>This is a new paragraph</p>" );

$( "<li class=\"new\">new list item</li>" );

// 根据 attribute 对象，创建新的元素
// 注意，第二个参数，即 attributes 对象中，class 属性名加了引号，另外两个没加，因为 class 是一个保留字。

$( "<a/>", {
    html: "This is a <strong>new</strong> link",
    "class": "new",
    href: "foo.html"
});
```

当创建一个新元素后，它还没有被添加到页面上，有几种方式可以在元素被创建出来后，将其添加到页面上
```
// 将新元素放在网页中
 
var myNewElement = $( "<p>New element</p>" );
 
myNewElement.appendTo( "#content" );
 
myNewElement.insertAfter( "ul:last" ); // 这会把 p 元素移除出 #content
 
$( "ul" ).last().after( myNewElement.clone() ); // 复制 p 元素，所以现在有两个 p。
```

### 3.jQuery 的链式操作是怎样的

如果在选取到的元素上调用一个方法，这个方法会返回一个 jQuery 对象，可以在这个对象上继续调用 jQuery 方法，而不需要使用分号暂停下来。这种操作叫做 chaining.
```
$( "#content" ).find( "h3" ).eq( 2 ).html( "new text for the third h3!" );
```

可以将链式操作分成几行，使代码获得更好的可读性。
```
$( "#content" )
    .find( "h3" )
    .eq( 2 )
    .html( "new text for the third h3!" );
```

jQuery 还提供了 end 方法，可以回到之前的选取到的元素上，用于应付万一需要修改 chain 上的操作的元素的情况。
```
$( "#content" )
    .find( "h3" )
    .eq( 2 )
        .html( "new text for the third h3!" )
        .end() // 回到 #content 上的所有 h3 元素上
    .eq( 0 )
        .html( "new text for the first h3!" );
```
Chaining 十分强大，自从 jQuery 使用这种方式之后，很多其他的库也采用了这种方式。但是必须小心使用 chaining，过多的链式操作会使代码极难修改或 debug。

关于一个 chain 多长才算是太长，没有明确的规则，只是要记住，过度使用 chaining 会让事情失控。

### 4.jQuery 如何移动元素

尽管有很多在 DOM 中移动元素的方法，但是，它们其实可以分为两类：

1.相对于另一个元素，放置选取的元素

2.相对于选取的元素，放置元素。

例如，jQuery 提供了 insertAfter 方法和 after 方法。insertAfter 将选取的元素放置在作为参数的元素后面。after 相反，将作为参数的元素放置在选取的元素后面。

其他几个方法也遵循这种模式：insertBefore 和 before，appendTo 和 append，prependTo 和 prepend。

这些方法最大的不同在于，它们选择了哪些元素，我们是否需要保存添加到页面上的元素的索引。

如果需要保存索引，我们应该选择第一种方式，即让选择的元素相对于另一个元素放置，因为这会返回被放置的元素。在这种情况下，应该选择：insertAfter(), .insertBefore(), .appendTo(), and .prependTo()

```
// 让第一个 list item 成为最后一个 list item:
var li = $( "#myList li:first" ).appendTo( "#myList" );
 
// 同一个问题的另一种解决方式：
$( "#myList" ).append( $( "#myList li:first" ) );
 
// 注意，Note that there's no way to access the list item
// that we moved, as this returns the list itself.
```

### 5.jQuery 如何修改元素的属性

jQuery 操作属性的能力很强大。虽然基本的操作十分简单，但是 attr 方法也提供更复杂的操作。

它设置一个显式的值，或者使用函数的返回值设置一个值。

当使用函数语法时，函数接受两个参数：1、基于零的元素的索引值，这个元素将被操作属性，2、被修改的属性目前的值。

```
// 操作单个属性
$( "#myDiv a:first" ).attr( "href", "newDestination.html" );

// 操作多个属性
$( "#myDiv a:first" ).attr({
    href: "newDestination.html",
    rel: "nofollow"
});

// 使用函数确定属性的新的值
$( "#myDiv a:first" ).attr({
    rel: "nofollow",
    href: function( idx, href ) {
        return "/new/" + href;
    }
});
 
$( "#myDiv a:first" ).attr( "href", function( idx, href ) {
    return "/new/" + href;
});
```
