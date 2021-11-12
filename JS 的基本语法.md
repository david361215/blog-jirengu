# 目录
1. 什么是表达式和语句
2. 标识符的规则
3. if else 语句
4. while for 语句
5. break continue
6. label

# 正文
### 1.什么是表达式和语句

1、表达式一般都有值，语句可能有也可能没有，但一般语句都没有值。
所以也不能完全根据是否有值来区分表达式和语句。

2、语句一般会改变环境。

&emsp;&emsp;二者的主要功能：表达式一般用来取值，语句一般用来改变环境。

常见表达式

* 1+2 表达式的值为3
* add(1,2) 表达式的值为函数的返回值
* console.log表达式的值为函数本身
* console.log(3) 表达式的值是多少？console.log 也是一个函数，所以表达式的值就是函数的返回值，这个值是 undefined。可以打开开发者工具输入看到就是 undefined。

常见语句

var a = 1 是一个语句。他也有值，值是 undefined。


### 2. 标识符的规则

* 取名字的时候用的符号
* 第一个字符可以是 Unicode 字母、$、_ 或中文。
* 其他字符，除了上面所说，还可以是数字。

例子：var 方方 = 'hi'。

&emsp;&emsp;这个 Unicode 字母包含希腊字母、拉丁字母、法语字母、德语字母、英文字母等，但是我们一般只用英文字母，所以这里的 Unicode 字母就可以当成英文字母来理解。

&emsp;&emsp;下划线最多连用两个，多了大家分不清到底有几个下划线。

&emsp;&emsp;除了变量名之外，还有很多标识符，用到时再说。

### 3. if else 语句

1、语法

if (表达式) {语句1} else  {语句2}

&emsp;&emsp;() 不能省略。括号里的表达式要有一个值。

&emsp;&emsp;{} 在语句只有一句时，可以省略，但是不建议这么做。

&emsp;&emsp;if 语句总会执行其中一条语句。

2、变态

1. 圆括号中的表达式可以非常变态，如 a=1，这是一个赋值语句，返回 true。
2. 语句 1 里可以变态，如嵌套的 if else。
3. 语句 2 里可以变态，如嵌套的 if else。
4. 缩进也可以很变态，面试常常下套的

例一：省略花括号
~~~
a=1
if(a===2)
  console.log('a')
  console.log('a等于2')
~~~

&emsp;&emsp;会打出 a 等于2，因为省略了花括号后，if 只管到后面的第一个语句，即 console.log('a')，也就是有个无形的花括号包围着 console.log('a')。再下一个语句相当于另外一条语句了，不再属于 if 语句。所以即使按照下面这样写，也是会打出 a等于2。

~~~
if(a===2)
  console.log('a');  console.log('a等于2')
~~~

&emsp;&emsp;如果将分号换成了逗号，那么就返回 undefined。因为逗号表示这个语句还没结束，后面的 console.log('a等于2') 依然属于 if 语句，而 a===2 是 false，所以 if 语句里的内容都不会打出来。

~~~
if(a===2)
  console.log('a'),  console.log('a等于2')
~~~


### 4. while for 语句

#### while 用的较少，do while 用的就更少了。

语法：
while ( 表达式 ) { 语句 }

&emsp;&emsp;判断表达式真假，当表达式为真，执行语句，执行完再次判断表达式真假。
    
&emsp;&emsp;当表达式为假，执行后面的语句。

&emsp;&emsp;一般，语句中，会间接修改 表达式的值，从而使表达式终究会为 false，从而停止循环。

例一：

~~~
var i = 0;
while ( i < 10 ){
  console.log(i);
  i = i +1;
}
~~~

&emsp;&emsp;Chrome 这个家伙会在打印出 1 到 9 后，还出现一个 10 ，估计是 bug。

例二：
~~~
while (true){}
~~~

&emsp;&emsp;它会一直运行，如果在开发者工具中运行，会占着 CPU，可能会导致死机。

例三：
~~~
var a = 0.1
while ( a !== 1 ){
  console.log(a)
  a = a + 0.1;
}
~~~

&emsp;&emsp;这个例子永远停不下来，因为浮点数计算不太精确，做几次加法后就没那么精确了。所以加了 9 次后，偏离就更多了，a 很可能不等于 1，而是可能会出现 a =  0.999999999998 这个情况。


#### for 是 while 的语法糖，比较方便。

一个循环，初始化、判断、循环体、增长，四部分必不可少。既然如此,为什么不把他们写在一起呢，因此就有了 for 循环。

~~~
var a = 0.1    // 初始化
while ( a !== 1 ){     //判断
  console.log(a)       //循环体
  a = a + 0.1;           //增长
}
~~~

语法：

for( 语句1; 表达式2; 语句3){
  循环体
}

* 先执行语句1，初始化。
* 然后执行表达式2，做判断。
* 如果为真，执行循环体，然后执行语句3，语句 3 作为自增。（这是考点）
* 如果为假，直接退出循环，执行后面的语句

注意：
* 语句 1 可以写在 for 循环外面，
* 表达式 2 如果不写，那么会一直执行，占满 CPU，导致浏览器崩溃。
* 语句 3 不写的效果和表达式不写是一样的。


例一：
~~~
for( let i = 0; i < 5; i++){
  console.log(i);
}
~~~

&emsp;&emsp;循环结束后，这个 i 的值是 5，但是在 for 循环外是访问不到的。

~~~
for( var i = 0; i < 5; i++){
  console.log(i);
}
~~~

&emsp;&emsp;循环结束后，这个 i 的值是 5，但是在 for 循环外是访问的到的。

例二：
~~~
for ( var i = 0; i < 5; i++){
  setTimeout( ()=>{
    console.log(i);  
  },0)
}
~~~

&emsp;&emsp;打印出 五个 5。

&emsp;&emsp;因为 for 循环是一个比 setITimeout 早一点的任务，换言之，得等到 for 循环执行完毕，才执行 setTimeout，此时 i 已经变成了 5。

&emsp;&emsp;因为设置了 5 次 setTimeout，所以会出现 五 个 5。

例三：
~~~
for ( let i = 0; i < 5; i++){
  setTimeout( ()=>{
    console.log(i);  
  },0)
}
~~~

&emsp;&emsp;此时依次打印出 0、1、2、3、4。

### 5.break continue

~~~
for( var i = 0; i < 10; i++){
  if( i%2===1){
    break;
  }
}
~~~

&emsp;&emsp;循环结束后， i===1。因为 当循环中的 i 等于 1 时，就 break 了，表示不执行后面的 i++，而且立刻跳出当前 for 循环。

~~~
for( var i = 0; i < 10; i++){
  if( i%2===1){
    continue;
    console.log('hi');
  }else{
    console.log(i);
  }
}
~~~
&emsp;&emsp;continue 表示这一步不做，跳过这次循环，但是 i++ 还是会执行，因此遇到 i 是奇数就不执行接下来的循环体 console.log('hi');，而是直接 i++，

&emsp;&emsp;有些语言会把 continue 换成 next。

例子：
~~~
for( var i =0; i <10; i++){
 for( var j = 100; j < 110; j++){
     if( i===5 ){
        break;
       }
    }
  console.log(i);
}
~~~

&emsp;&emsp;还是会打出 0、1、2、3、4、5、6、7、8、9，因为 break 只会跳出内层的 for 循环，外面的 for 循环不受影响。

### 6. label

label 很少用，但是面试可能会考

语法：
~~~
foo:{
  console.log( 1 );
  break foo;
  console.log(' 本行不会输出 ');
}
console.log(2)
~~~

&emsp;&emsp;foo 是一个标识符，规则之前讲过。后面是一个语句或代码块。

&emsp;&emsp;作用是标识一个代码块或语句，经常和 break 或 continue 联合使用。

例子：
~~~
{
 a:1
}
~~~

&emsp;&emsp;请问这是个啥东西，对象么？不是，a 是一个 label。Chrome 和 Edge 都显示是个对象，这是不对的。

&emsp;&emsp;这个东西就只能用来考试，实际没啥用。

&emsp;&emsp;只有 var a ={a:1} 花括号及其内容才是一个对象。
