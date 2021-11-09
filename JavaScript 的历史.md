# 目录
1. JavaScript 的设计背景
2. JavaScript 的设计思路
3. JavaScript 的设计缺陷
4. 浏览器大战
5. 标准化

# 正文
### 1.JavaScript 的设计背景

&emsp;&emsp;1994 年，Netscape 公司开发了 Navigator 浏览器，并希望为该浏览器添加交互功能，因此需要使用脚本语言来完成交互。当时可以选择使用一门现有语言，比如 Perl、Python、Scheme 等，或者重新开发一门新的语言，Netscape 选择了后者，同时要求这门新的语言尽可能类似 Java。这个任务落在了年轻的 Brendan Eich 肩上。只是他原本的任务是研究将 Scheme 用作网页脚本语言的可能性。他本人对开发一款类似 Java 的新的脚本语言并不感冒。

### 2.JavaScript 的设计思路
&emsp;&emsp;他用十天时间设计了这门语言。

&emsp;&emsp;具体的设计思路：
1. 借鉴 C 语言的基本语法；
2. 借鉴 Java 语言的数据类型和内存管理；
3. 借鉴 Scheme 语言，将函数提升到"第一等公民"（first class）的地位；
4. 借鉴 Self 语言，使用基于原型（prototype）的继承机制。

&emsp;&emsp;这些设计思路都体现在现在 JavaScript 的各种核心特性。

### 3.JavaScript 的设计缺陷
&emsp;&emsp;仓促地出现，导致 JavaScript 有各种奇怪的难以理解的特性，列举几个典型的如下。
* 没有 namespace，很难进行模块化开发。（由于 ES6 引进了 module 概念，这一问题得到了缓解）
* 标准库很小，导致功能太少。（由于 jQuery、underscore、lodash 等函数库的出现，这一问题也得到了一定的缓解）
* null 属于 object 的一种，意思是该对象为空；undefined 则是一种数据类型，表示未定义。两者非常容易混淆，但是含义完全不同。
~~~
    var foo;

　　alert(foo == null); // true

　　alert(foo == undefined); // true

　　alert(foo === null); // false

　　alert(foo === undefined); // true
~~~

### 4.浏览器大战
&emsp;&emsp;1995 年，微软推出了 IE，采用了微软自己的脚本语言 JScript，这个语言是 JavaScript 语言的另一种实现，但是两个不同的语言版本的存在，意味这开发人员要适应各种不同的语言特性，大大增加工作的复杂性。后来随着微软将 IE 绑定进了 Windows 系统，Netscape 的浏览器节节败退，2001 年，IE 6 的发布，它在 2004 年全球占有率就达到 80% 以上。

### 5.标准化
&emsp;&emsp;1996年11月，Netscape 向 ECMA 提交了 JavaScript 的语言标准，随即，在 1997 年 6 月，第一版 ECMAScript 就发布了。1999 年 12 月，第三版 ECMAScript 发布，这个版本使用最广泛。与此同时，第四版，也在酝酿中，但是由于加入了太多新功能，这一版本遭到了众多浏览器厂商的抵制（最终，这一版的很多功能在 2015 年的第六版中才真正实现），所以这个方案被抛弃了。因此 ECMAScript 没有第四版，直接跳到了第五版。

&emsp;&emsp;2009 年 12 月，第五版发布，增加了一些功能。这十年 IE6 如日中天，Chrome 刚发布，还没占太多份额，所以不敢大肆更新 JS。

&emsp;&emsp;2015 年 6 月，第六版发布，新浏览器都支持这一版，之后每年发布一版，版本号以年份命名。
