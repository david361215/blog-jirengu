## 目录
1. 浏览器渲染原理
2. CSS 动画————transition 
3. CSS 动画————animation

## 正文
#### 1. 浏览器渲染原理

浏览器拿到 HTML CSS 后做了什么？
1. 根据 HTML 构建 HTML 树（DOM）
2. 根据 CSS 构建 CSS 树（CSSOM）
3. 将两棵树合并成一颗渲染树（render tree）
4. 布局 layout，根据文档流、盒模型，计算大小和位置
5. 绘制 Paint，把边框颜色、文字颜色、阴影等画出来
6. 合成 Compose，根据层叠关系，展示画面!

要了解根据原理如何做性能优化，这些优化没啥规律，老师推荐了 Google 的一些文章，里面包含一些性能优化措施。

#### 2. transition

它用于控制 CSS 属性值之间形成过渡，将值的瞬间改变改为逐渐改变，使变化看起来更加平滑。也叫，补充中间帧。

transition 是以下四个属性的缩写。一般都使用缩写，不单独写。
* transition-delay: 0s
* transition-duration: 0s
* transition-property: all
* transition-timing-function: ease

#### 3. animation

 animation 动画包含两部分，一部分是 animation 属性，另一部分是 keyframes 关键帧。关键帧描述成为动画的样式的起始和结束状态。

animation 属性是 8 个子属性的简写，如下，一般最少要写动画名和持续时间两个子属性的值。
* animation-duration
* animation-timing-function
* animation-delay
* animation-iteration-count
* animation-direction
* animation-fill-mode
* animation-play-state
* animation-name
