# 使用CSS变换和动画实现钢铁侠电弧反应堆

Kunal Sarkar 2018.4.2  动画 变换 [原文地址](https://css-tricks.com/iron-mans-arc-reactor-using-css3-transforms-and-animations/)

钢铁侠粉丝们好，启动你的代码编辑！ 我们将使用CSS实现钢铁侠套装的弧形反应堆。 以下是最终结果的样子：

<div class="cp_embed_wrapper resizable" style="height: 500px; overflow: hidden;">
    <iframe id="cp_embed_QmLEWN" src="//codepen.io/supersarkar/embed/QmLEWN?height=400&amp;theme-id=1&amp;slug-hash=QmLEWN&amp;default-tab=result&amp;user=supersarkar&amp;embed-version=2&amp;pen-title=Iron%20Man's%20Arc%20Reactor" scrolling="no" frameborder="0" height="400" allowtransparency="true" allowfullscreen="true" name="CodePen Embed" title="Iron Man's Arc Reactor" class="cp_embed_iframe " style="width: 100%; overflow: hidden; height: 100%;"></iframe>
</div>

## 满屏wrapper

我们把弧形反应堆放在一个黑色背景的满屏页上。 这是我们制作一个完整的页面wrapper元素的代码：

 ```css
 body {
  margin: 0;
}

.fullpage-wrapper {
  height: 100vh;
  background: radial-gradient(#353c44, #222931);
}
```

为什么我们要声明没有外边距的body？ 默认情况下，`<body>`元素在用户代理样式表中设置了一些外边距。 这可以防止`<body>`内的元素接触屏幕的边缘。由于我们希望我们的wrapper覆盖整个屏幕，所以我们通过将`<body>`元素的默认边距设置为0来移除它的外边距。

我们设置`.fullpage-wrapper`的height为视口的整个高度。 我们不必指定宽度，因为默认情况下div是全宽度。我们还可以采用另一种方法将元素的宽度和高度都设置为`100％`，但随着更多元素添加到屏幕中，这会带来一些潜在的缺点。使用视口单位可确保我们的wrapper始终占据屏幕的整个垂直空间，而不管它是什么或添加了什么元素到布局上。

我们在wrapper上还使用CSS函数[radial-gradient()](https://css-tricks.com/snippets/css/css-radial-gradient/)实现径向渐变效果。 函数内部的参数是颜色的起点和终点。 因此，背景的中心到边缘将从`＃353c44`往`＃222931`渐变。 这是微妙的，也是个不错的尝试。

<figure id="post-268738" class="align-none media-268738"><img src="https://cdn.css-tricks.com/wp-content/uploads/2018/03/ironman-1.jpg" srcset="https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_714,f_auto,q_auto/v1521762064/ironman-1_o38vzq.jpg 714w, https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_200,f_auto,q_auto/v1521762064/ironman-1_o38vzq.jpg 200w" sizes="(min-width: 1850px) calc( (100vw - 555px) / 3 )
       (min-width: 1251px) calc( (100vw - 530px) / 2 )
       (min-width: 1086px) calc(100vw - 480px)
       (min-width: 626px)  calc(100vw - 335px)
                           calc(100vw - 30px)" alt=""></figure>

## 居中反应堆容器

在我们开始创建反应堆之前，为它创建一个居中的容器：

```css
.reactor-container {
  width: 300px;
  height: 300px;
  margin: auto;
  border: 1px dashed #888;
}
```

我们给出一个带虚线边框的、`300px` X `300px`的容器。 `margin:auto;` 这个声明确保容器水平方向居中。

<figure id="post-268739" class="align-none media-268739"><img src="https://cdn.css-tricks.com/wp-content/uploads/2018/03/ironman-2.jpg" srcset="https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_947,f_auto,q_auto/v1521762066/ironman-2_c7jsda.jpg 947w, https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_200,f_auto,q_auto/v1521762066/ironman-2_c7jsda.jpg 200w" sizes="(min-width: 1850px) calc( (100vw - 555px) / 3 )
       (min-width: 1251px) calc( (100vw - 530px) / 2 )
       (min-width: 1086px) calc(100vw - 480px)
       (min-width: 626px)  calc(100vw - 335px)
                           calc(100vw - 30px)" alt=""></figure>

但是它为什么垂直方向不居中呢？
根据[CSS2规范](https://www.w3.org/TR/CSS22/visudet.html#Computing_heights_and_margins)，如果我们给左边和右边的外边距都是auto，那么整个可用空间将平分为左右边距。 尽管如此，顶部和底部边缘的情况并非如此。 对于顶部和底部边距，CSS2规范是这样描述的：

```
If margin-top, or margin-bottom are auto, their used value is 0.
如果上外边距和下外边距的值是auto，它们会认为值是0.
```

然而，我们确实有个好消息。 Flexbox布局遵循新的对齐规则，以下是[Flexbox规范](https://www.w3.org/TR/css-flexbox-1/#auto-margins)的特意指明的：

```
Prior to alignment via justify-content and align-self, any positive free space is distributed to auto margins in that dimension.
通过justify-content和align-self进行对齐之前，任何可用的自由空间都将分配给该维度中的自动边距。
```

这意味着如果考虑的元素显示为弹性布局项，则margin：auto; 将在水平和垂直两个方向上生效。 让我们将wrapper设置为一个弹性容器，其子元素形成弹性布局项：

```css
.fullpage-wrapper {
  width: 100%;
  height: 100vh;
  background: radial-gradient(#353c44, #222931);
  display: flex;
}
```

然后，这样就好多了：

<figure id="post-268740" class="align-none media-268740"><img src="https://cdn.css-tricks.com/wp-content/uploads/2018/03/ironman-3.jpg" srcset="https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_947,f_auto,q_auto/v1521762067/ironman-3_njqv2m.jpg 947w, https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_200,f_auto,q_auto/v1521762067/ironman-3_njqv2m.jpg 200w" sizes="(min-width: 1850px) calc( (100vw - 555px) / 3 )
       (min-width: 1251px) calc( (100vw - 530px) / 2 )
       (min-width: 1086px) calc(100vw - 480px)
       (min-width: 626px)  calc(100vw - 335px)
                           calc(100vw - 30px)" alt=""></figure>

还有许多其他方法可以将元素在HTML中居中。 这里有更多的[让元素居中的CSS技巧指南](https://css-tricks.com/centering-css-complete-guide/)可以去了解。

## 反应堆堆芯：CSS实现同心圆
我们知道HTML中的新元素是从左到右创建的(用于从左到右的语言)，或者是自上而下创建的。元素永远不会重叠，直到你提供一些负的边距。
那么，我们将如何显示同心圆呢？我们将使用绝对定位。

[position](https://css-tricks.com/almanac/properties/p/position/)属性的默认值是`static`. 静态和相对定位遵循从上到下、从左到右的流程。然而, 绝对定位元素不被视为文档流的一部分，可以使用顶部、右侧、底部和左侧属性定位到任何地方。

让我们从创建最小的圆开始：

```HTML
<div class="fullpage-wrapper">
  <div class="reactor-container">
    <!-- the smallest circle -->
    <div class="core-inner"></div>
  </div>
</div>
```

```css
.core-inner {
  position: absolute;
  width: 70px;
  height: 70px;
  border-radius: 50%;
  border: 5px solid #1b4e5f;
  background-color: #fff;
}
```

<figure id="post-268741" class="align-none media-268741"><img src="https://cdn.css-tricks.com/wp-content/uploads/2018/03/ironman-4.jpg" srcset="https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_650,f_auto,q_auto/v1521762069/ironman-4_dpsgt6.jpg 650w, https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_200,f_auto,q_auto/v1521762069/ironman-4_dpsgt6.jpg 200w" sizes="(min-width: 1850px) calc( (100vw - 555px) / 3 )
       (min-width: 1251px) calc( (100vw - 530px) / 2 )
       (min-width: 1086px) calc(100vw - 480px)
       (min-width: 626px)  calc(100vw - 335px)
                           calc(100vw - 30px)" alt=""></figure>

我们需要把这个`div`居中。你可能也会尝试应用我们用来居中反应堆这个圆同样的`flexbox`概念。但是，以下是[CSS2规范](https://www.w3.org/TR/CSS22/visudet.html#abs-non-replaced-height)中关于关于绝对定位的元素设置`margin: auto`：

```
If none of the three (top, height, and bottom) are auto: If both margin-top and margin-bottom are auto, solve the equation under the extra constraint that the two margins get equal values.
如果这三个(顶部、高度和底部)中没有一个是自动的：如果`margin-top`和`margin-bottom`都是`auto`，那就在两个边距相等的附加约束下求解。
```

这意味着如果一个绝对定位的元素的顶部、高度和底部的值除了是`auto`外有任何其他值，那么将顶部和底部的边距设置为`auto`可以将元素垂直居中。
水平居中的相同情况：如果一个绝对定位的元素的顶部、高度和底部的值除了是`auto`外有任何其他值，那么将顶部和底部的边距设置为`auto`才可以将元素水平居中。
这意味着我们不需要`flexbox`布局来居中一个已知的高度和宽度的绝对定位元素。我们只要确保，我们给`top`，`right`，`bottom`，`left`的值除了`auto`之外的一些值，因此，我们用`0`:

```css
.core-inner {
  position: absolute;
  width: 70px;
  height: 70px;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  margin: auto;
  border-radius: 50%;
  border: 5px solid #1b4e5f;
  background-color: #fff;
}
```

我们不想给我们将有的所有同心圆重复这五条线，所以让我们为它创建一个单独的类。我们也不想为我们像显示成圆形的`div`定义`border-radius: 50%;`，所以我们也将为它创建一个类：

```css
.circle {
  border-radius: 50%;
}

.abs-center {
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  margin: auto;

}

.core-inner {
  width: 70px;
  height: 70px;
  border: 5px solid #1b4e5f;
  background-color: #fff;
}
```

另外，将这些新类添加到`.core-inner`元素上：

```HTML
<div class="fullpage-wrapper">
  <div class="reactor-container">
    <!-- the smallest circle -->
    <div class="core-inner circle abs-center"></div>
  </div>
</div>
```

<figure id="post-268742" class="align-none media-268742"><img src="https://cdn.css-tricks.com/wp-content/uploads/2018/03/ironman-5.jpg" srcset="https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_661,f_auto,q_auto/v1521762070/ironman-5_qfarjc.jpg 661w, https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_200,f_auto,q_auto/v1521762070/ironman-5_qfarjc.jpg 200w" sizes="(min-width: 1850px) calc( (100vw - 555px) / 3 )
       (min-width: 1251px) calc( (100vw - 530px) / 2 )
       (min-width: 1086px) calc(100vw - 480px)
       (min-width: 626px)  calc(100vw - 335px)
                           calc(100vw - 30px)" alt=""></figure>

好的，我们的同心圆居中了。让我们继续发光(glow)。
但是 CSS没有任何"glow"属性.
别担心，我们有[`box-shadow`](https://css-tricks.com/almanac/properties/b/box-shadow/)属性。与其给阴影一个深色的颜色，我们将给它一个明亮的颜色，使阴影看起来像发光。很聪明，是不是？让我们这样做吧：

```css
.core-inner {
  width: 70px;
  height: 70px;
  border: 5px solid #1b4e5f;
  background-color: #fff;
  box-shadow: 0px 0px 7px 5px #52fefe;
}
```

<figure id="post-268743" class="align-none media-268743"><img src="https://cdn.css-tricks.com/wp-content/uploads/2018/03/ironman-6.jpg" srcset="https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_608,f_auto,q_auto/v1521762072/ironman-6_iu9spv.jpg 608w, https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_200,f_auto,q_auto/v1521762072/ironman-6_iu9spv.jpg 200w" sizes="(min-width: 1850px) calc( (100vw - 555px) / 3 )
       (min-width: 1251px) calc( (100vw - 530px) / 2 )
       (min-width: 1086px) calc(100vw - 480px)
       (min-width: 626px)  calc(100vw - 335px)
                           calc(100vw - 30px)" alt=""></figure>

让我们休息一下，先了解一下`box-shadow`的语法，因为我们会经常使用它。下面是`box-shadow`按顺序表示的含义：
-`x-offset`: x轴偏移, 我们想把阴影推到右边(x轴)。 负值会将阴影推到左侧。
-`y-offset`: y轴偏移, 我们想要把阴影向上还是向下推多远(y轴)。
-`blur-radius`: 我们希望我们的阴影变得多么模糊。
-`spread-radius`: 我们多么希望我们的阴影如何传播。
-`color`: 阴影的颜色.
使用这些值来实时查看它们的效果。
在现实生活中，阴影不会只落在物体的外面。阴影也落在物体上。想象一下狗挖的坑，里面会有阴影，对吧？
我们可以在`box-sizing`属性中使用`inset`关键字在元素中给出阴影。为了同时给出一个元素，外部和内部阴影，我们只需将它们用逗号分隔。让我们这样做，让我们的反应堆的内部核心内外发光：

```css
.core-inner {
  width: 70px;
  height: 70px;
  border: 5px solid #1B4e5f;
  background-color: #fff;
  box-shadow: 0px 0px 7px 5px #52fefe, 0px 0px 10px 10px #52fefe inset;
}
```

<figure id="post-268744" class="align-none media-268744"><img src="https://cdn.css-tricks.com/wp-content/uploads/2018/03/ironman-7.jpg" srcset="https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_544,f_auto,q_auto/v1521762073/ironman-7_suolkp.jpg 544w, https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_200,f_auto,q_auto/v1521762073/ironman-7_suolkp.jpg 200w" sizes="(min-width: 1850px) calc( (100vw - 555px) / 3 )
       (min-width: 1251px) calc( (100vw - 530px) / 2 )
       (min-width: 1086px) calc(100vw - 480px)
       (min-width: 626px)  calc(100vw - 335px)
                           calc(100vw - 30px)" alt=""></figure>

现在它开始看起来像科幻了！
让我们在上面再画一个圆圈。我们希望内部圆圈显示在其他圆圈的顶部，所以我们将在上面添加新的圆圈`div`代码中的核心圆圈：

```HTML
<div class="fullpage-wrapper">
  <div class="reactor-container">
    <!-- the second circle -->
    <div class="core-outer circle abs-center"></div>
    <!-- the smallest circle -->
    <div class="core-inner circle abs-center"></div>
  </div>
</div>
```

代码中的元素显示在屏幕上。如果我们在代码中将核心-外部置于内核-内部下面，那么核心-内部将不可见，因为核心-外部将覆盖它。
让我们给出外部代码的样式。 外核将比内核稍大一点，我们也会让核心-外部的外部和内部发光：

```css
.core-outer {
  width: 120px;
  height: 120px;
  border: 1px solid #52fefe;
  background-color: #fff;
  box-shadow: 0px 0px 2px 1px #52fefe, 0px 0px 10px 5px #52fefe inset;
}
```

<figure id="post-268745" class="align-none media-268745"><img src="https://cdn.css-tricks.com/wp-content/uploads/2018/03/ironman-8.jpg" srcset="https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_572,f_auto,q_auto/v1521762074/ironman-8_htenwe.jpg 572w, https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_200,f_auto,q_auto/v1521762074/ironman-8_htenwe.jpg 200w" sizes="(min-width: 1850px) calc( (100vw - 555px) / 3 )
       (min-width: 1251px) calc( (100vw - 530px) / 2 )
       (min-width: 1086px) calc(100vw - 480px)
       (min-width: 626px)  calc(100vw - 335px)
                           calc(100vw - 30px)" alt=""></figure>
我想让你做一件事：看着阴影(发光)，试着辨别哪一个是哪个圆圈。有四个阴影和两个圆圈(到现在为止)。
为了完成核心的设计，我们还需要一个圈来包裹内外圆：

```HTML
<div class="fullpage-wrapper">
  <div class="reactor-container">
    <!-- the third circle -->
    <div class="core-wrapper circle abs-center"></div>
    <!-- the second circle -->
    <div class="core-outer circle abs-center"></div>
    <!-- the smallest circle -->
    <div class="core-inner circle abs-center"></div>
  </div>
</div>
```
这将是一个大一点，并将再次有相同的阴影，我们将使用一个黑暗的背景为core-wrapper：

```css
.core-wrapper {
  width: 180px;
  height: 180px;
  background-color: #073c4b;
  box-shadow: 0px 0px 5px 4px #52fefe, 0px 0px 6px 2px #52fefe inset;
}
```

<figure id="post-268746" class="align-none media-268746"><img src="https://cdn.css-tricks.com/wp-content/uploads/2018/03/ironman-9.jpg" srcset="https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_541,f_auto,q_auto/v1521762076/ironman-9_nn86oe.jpg 541w, https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_200,f_auto,q_auto/v1521762076/ironman-9_nn86oe.jpg 200w" sizes="(min-width: 1850px) calc( (100vw - 555px) / 3 )
       (min-width: 1251px) calc( (100vw - 530px) / 2 )
       (min-width: 1086px) calc(100vw - 480px)
       (min-width: 626px)  calc(100vw - 335px)
                           calc(100vw - 30px)" alt=""></figure>

## 用CSS3变换建立反应堆线圈和旋转
我们有反应堆的核心，现在我们需要一个围绕着反应堆核心的隧道。实际上，我们只需要画一个比core-wrapper大一点的圆圈，就可以制造出一个圆形隧道的错觉。 让我们这样做：

```HTML
<div class="fullpage-wrapper">
  <div class="reactor-container">
    <!-- the largest circle -->
    <div class="tunnel circle abs-center"></div>
    <!-- the third circle -->
    <div class="core-wrapper circle abs-center"></div>
    <!-- the second circle -->
    <div class="core-outer circle abs-center"></div>
    <!-- the smallest circle -->
    <div class="core-inner circle abs-center"></div>
  </div>
</div>
```
...再宽一点，给隧道增添同样的光影：

```css
.tunnel {
  width: 220px;
  height: 220px;
  background-color: #fff;
  box-shadow: 0px 0px 5px 1px #52fefe, 0px 0px 5px 4px #52fefe inset;
}
```

<figure id="post-268747" class="align-none media-268747"><img src="https://cdn.css-tricks.com/wp-content/uploads/2018/03/ironman-10.jpg" srcset="https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_586,f_auto,q_auto/v1521762077/ironman-10_cytty9.jpg 586w, https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_200,f_auto,q_auto/v1521762077/ironman-10_cytty9.jpg 200w" sizes="(min-width: 1850px) calc( (100vw - 555px) / 3 )
       (min-width: 1251px) calc( (100vw - 530px) / 2 )
       (min-width: 1086px) calc(100vw - 480px)
       (min-width: 626px)  calc(100vw - 335px)
                           calc(100vw - 30px)" alt=""></figure>

我们的隧道准备好了。
确保您不只是复制粘贴代码。
看一看圆圈的光影，找出哪个光影是哪个圆圈的，是外部的光影还是镶嵌的光影。
现在，我们需要这条隧道上的八个线圈。
线圈是简单的矩形，但主要的挑战是，我们需要线圈沿着隧道的圆形路径运行，而不是直线。
一种方法是创建八个小矩形，将它们的中心移动到反应堆的中心，并以一个增大的角度(45度倍数)旋转每个线圈。
我们不要把它复杂化，一次做一个矩形线圈：

```Html
<div class="fullpage-wrapper">
  <div class="reactor-container">
    <div class="tunnel circle abs-center"></div>
    <div class="core-wrapper circle abs-center"></div>
    <div class="core-outer circle abs-center"></div>
    <div class="core-inner circle abs-center"></div>
    <div class="coil-1"></div>
  </div>
</div>
```

```CSS
.coil-1 {
  position: absolute;
  width: 30px;
  height: 26px;
  background-color: #073c4b;
  box-shadow: 0px 0px 5px #52fefe inset;
}
```

<figure id="post-268748" class="align-none media-268748"><img src="https://cdn.css-tricks.com/wp-content/uploads/2018/03/ironman-11.jpg" srcset="https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_602,f_auto,q_auto/v1521762079/ironman-11_uqldm1.jpg 602w, https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_200,f_auto,q_auto/v1521762079/ironman-11_uqldm1.jpg 200w" sizes="(min-width: 1850px) calc( (100vw - 555px) / 3 )
       (min-width: 1251px) calc( (100vw - 530px) / 2 )
       (min-width: 1086px) calc(100vw - 480px)
       (min-width: 626px)  calc(100vw - 335px)
                           calc(100vw - 30px)" alt=""></figure>
现在，我们想把这个线圈放在隧道的中央。就像这样：
<figure id="post-268749" class="align-none media-268749"><img src="https://cdn.css-tricks.com/wp-content/uploads/2018/03/ironman-12.jpg" srcset="https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_631,f_auto,q_auto/v1521762080/ironman-12_xjfnzm.jpg 631w, https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_389,f_auto,q_auto/v1521762080/ironman-12_xjfnzm.jpg 389w, https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_200,f_auto,q_auto/v1521762080/ironman-12_xjfnzm.jpg 200w" sizes="(min-width: 1850px) calc( (100vw - 555px) / 3 )
       (min-width: 1251px) calc( (100vw - 530px) / 2 )
       (min-width: 1086px) calc(100vw - 480px)
       (min-width: 626px)  calc(100vw - 335px)
                           calc(100vw - 30px)" alt=""></figure>
我们的反应堆容器`.reactor-container`是`300px` X `300px`，所以从顶部到左边的中心是`150px`。
隧道宽`220px`，半径为`110px`。
这就给出了线圈的顶部偏移量：`150px`-`110px`。
我们可以将线圈的左边保持到`150px`，但是由于我们的线圈宽`30px`，它会将线圈的中间部分向右移动`15px`，这就是为什么我们需要从`150px`减去`15px`才能得到线圈的左偏移量。
我们可以自己计算这些值，也可以使用CSS calc()函数。
让我们使用CSS calc()函数来计算线圈的顶部和左侧属性：

```CSS
.coil-1 {
  position: absolute;
  width: 30px;
  height: 20px;
  top: calc(50% - 110px);
  left: calc(50% - 15px);
  background-color: #073c4b;
  box-shadow: 0px 0px 5px #52fefe inset;
}
```
<figure id="post-268750" class="align-none media-268750"><img src="https://cdn.css-tricks.com/wp-content/uploads/2018/03/ironman-13.jpg" srcset="https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_558,f_auto,q_auto/v1521762082/ironman-13_o8lf3m.jpg 558w, https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_200,f_auto,q_auto/v1521762082/ironman-13_o8lf3m.jpg 200w" sizes="(min-width: 1850px) calc( (100vw - 555px) / 3 )
       (min-width: 1251px) calc( (100vw - 530px) / 2 )
       (min-width: 1086px) calc(100vw - 480px)
       (min-width: 626px)  calc(100vw - 335px)
                           calc(100vw - 30px)" alt=""></figure>
如您所见，calc()函数将一个数学表达式作为其参数并进行求解。
现在我们需要八个这样的线圈，但它们必须放在隧道里。
为了做到这一点，正如我们所讨论的，我们可以简单地把八个线圈放在同一个地方，然后把它们的原点转换到反应堆的中心，然后把每个线圈旋转45度。
我们需要更新线圈的来源，因为在默认情况下，它被设置为线圈的中心；我们希望它位于反应堆的中心：
<figure id="post-268751" class="align-none media-268751"><img src="https://cdn.css-tricks.com/wp-content/uploads/2018/03/ironman-14.jpg" srcset="https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_648,f_auto,q_auto/v1521762084/ironman-14_abhfxu.jpg 648w, https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_486,f_auto,q_auto/v1521762084/ironman-14_abhfxu.jpg 486w, https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_200,f_auto,q_auto/v1521762084/ironman-14_abhfxu.jpg 200w" sizes="(min-width: 1850px) calc( (100vw - 555px) / 3 )
       (min-width: 1251px) calc( (100vw - 530px) / 2 )
       (min-width: 1086px) calc(100vw - 480px)
       (min-width: 626px)  calc(100vw - 335px)
                           calc(100vw - 30px)" alt=""></figure>
我们将使用`transform-origin`属性来设置线圈的原点：

```CSS
.coil-1 {
  position: absolute;
  width: 30px;
  height: 20px;
  top: calc(50% - 110px);
  left: calc(50% - 15px);
  transform-origin: 15px 110px;
  background-color: #073c4b;
  box-shadow: 0px 0px 5px #52fefe inset;
}
```
`transform-origin`的第一个值15px是元素的左上角的x偏移（水平距离），第二个值为1px，是元素的左上角的y偏移（垂直距离）。
线圈的起源现在位于反应堆的中心，让我们用CSS3 `transform`属性把它旋转45度，看看会发生什么：
```CSS
.coil-1 {
  position: absolute;
  width: 30px;
  height: 20px;
  top: calc(50% - 110px);
  left: calc(50% - 15px);
  transform-origin: 15px 110px;
  transform: rotate(45deg);
  background-color: #073c4b;
  box-shadow: 0px 0px 5px #52fefe inset;
}
```
<figure id="post-268752" class="align-none media-268752"><img src="https://cdn.css-tricks.com/wp-content/uploads/2018/03/ironman-15.jpg" srcset="https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_537,f_auto,q_auto/v1521762085/ironman-15_uvlysy.jpg 537w, https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_200,f_auto,q_auto/v1521762085/ironman-15_uvlysy.jpg 200w" sizes="(min-width: 1850px) calc( (100vw - 555px) / 3 )
       (min-width: 1251px) calc( (100vw - 530px) / 2 )
       (min-width: 1086px) calc(100vw - 480px)
       (min-width: 626px)  calc(100vw - 335px)
                           calc(100vw - 30px)" alt=""></figure>
好棒！这正是我们想要的。
在创建所有八个线圈之前，让我们创建一个包含所有八个线圈的线圈容器`div`：
```HTML
<div class="fullpage-wrapper">
  <div class="reactor-container">
    <div class="tunnel circle abs-center"></div>
    <div class="core-wrapper circle abs-center"></div>
    <div class="core-outer circle abs-center"></div>
    <div class="core-inner circle abs-center"></div>
    <!-- the coil container -->
    <div class="coil-container">
      <div class="coil coil-1"></div>
    </div>
  </div>
</div>
```
您会注意到，我们还添加了一个类`coil`到`coil-1`元素。
我们将保持线圈中所有线圈的共同样式，而单独的线圈元件类只有它们的旋转角：
```css
.coil-container {
  position: relative;
  width: 100%;
  height: 100%;
}

.coil {
  position: absolute;
  width: 30px;
  height: 20px;
  top: calc(50% - 110px);
  left: calc(50% - 15px);
  transform-origin: 15px 110px;
  background-color: #073c4b;
  box-shadow: 0px 0px 5px #52fefe inset;
}

.coil-1 {
  transform: rotate(45deg);
}
```
输出将保持不变。
现在，让所有八个线圈在`.coil-container`里面。
```HTML
<div class="fullpage-wrapper">
  <div class="reactor-container">
    <div class="tunnel circle abs-center"></div>
    <div class="core-wrapper circle abs-center"></div>
    <div class="core-outer circle abs-center"></div>
    <div class="core-inner circle abs-center"></div>
    <!-- the coil container -->
    <div class="coil-container">
      <div class="coil coil-1"></div>
      <div class="coil coil-2"></div>
      <div class="coil coil-3"></div>
      <div class="coil coil-4"></div>
      <div class="coil coil-5"></div>
      <div class="coil coil-6"></div>
      <div class="coil coil-7"></div>
      <div class="coil coil-8"></div>
    </div>
  </div>
</div>
```
...并对所有线圈进行不同的旋转（增量为45度）：
```css
.coil {
  position: absolute;
  width: 30px;
  height: 20px;
  top: calc(50% - 110px);
  left: calc(50% - 15px);
  transform-origin: 15px 110px;
  background-color: #073c4b;
  box-shadow: 0px 0px 5px #52fefe inset;
}

.coil-1 {
  transform: rotate(0deg);
}

.coil-2 {
  transform: rotate(45deg);
}

.coil-3 {
  transform: rotate(90deg);
}

.coil-4 {
  transform: rotate(135deg);
}

.coil-5 {
  transform: rotate(180deg);
}

.coil-6 {
  transform: rotate(225deg);
}

.coil-7 {
  transform: rotate(270deg);
}

.coil-8 {
  transform: rotate(315deg);
}
```
<figure id="post-268753" class="align-none media-268753"><img src="https://cdn.css-tricks.com/wp-content/uploads/2018/03/ironman-16.jpg" srcset="https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_543,f_auto,q_auto/v1521762086/ironman-16_ogjzph.jpg 543w, https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_200,f_auto,q_auto/v1521762086/ironman-16_ogjzph.jpg 200w" sizes="(min-width: 1850px) calc( (100vw - 555px) / 3 )
       (min-width: 1251px) calc( (100vw - 530px) / 2 )
       (min-width: 1086px) calc(100vw - 480px)
       (min-width: 626px)  calc(100vw - 335px)
                           calc(100vw - 30px)" alt=""></figure>
我们的反应堆几乎准备好了。

## 用CSS3动画转动线圈
在钢铁人的弧形反应堆里，线圈不会移动，但它们会在我们的反应堆里移动。
我们将驱动线圈沿隧道旋转，并将使用CSS3动画实现，不使用JavaScript。
要创建动画，您需要知道要动画的对象的初始和最终状态。
我们在CSS中使用`@keyframes`按规则定义这些初始和最终状态：
```css 
@keyframes reactor-anim {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(360deg);
  }
}
```
我们希望元素在0度，使其动起来，直到它达到360度。我们把这个动画命名为`reactor-anim`。我们想要动画的元素是`.coil-contailer`注意，我们还没有定义要驱动的对象，我们只定义了动画的初始、最终状态和名称。我们需要将元素链接到动画中才能生效。我们通过给`.coil-container`使用动画名称属性值进行操作。
```css
.coil-container {
  position: relative;
  width: 100%;
  height: 100%;
  animation-name: reactor-anim;
  animation-duration: 3s;
}
```
注意，我们还使用`animation-duration`属性给出了动画的持续时间。
这定义了从使用`@keyframes `规则定义的“从”状态到“到”状态所需的时间。
<iframe id="cp_embed_GxKZee" src="//codepen.io/supersarkar/embed/GxKZee?height=415&amp;theme-id=1&amp;slug-hash=GxKZee&amp;default-tab=result&amp;user=supersarkar&amp;embed-version=2&amp;pen-title=Arc-Reactor-Ease-In" scrolling="no" frameborder="0" height="415" allowtransparency="true" allowfullscreen="true" name="CodePen Embed" title="Arc-Reactor-Ease-In" class="cp_embed_iframe " style="width: 100%; overflow: hidden; height: 100%;"></iframe>
我们需要在这里改变两件事：我们希望动画无限地进行，我们想要一个线性动画。你可以看到动画在开始是慢的，然后是快的，然后是慢的-这个行为是由动画的定时函数定义的。
让我们做以下修改：
```css
.coil-container {
  position: relative;
  width: 100%;
  height: 100%;
  animation-name: reactor-anim;
  animation-duration: 3s;
  animation-iteration-count: infinite;
  animation-timing-function: linear;
}
```
我们使用`animation-iteration-count`(动画迭代计数)属性将动画设置为无穷大，而`animation-timing-function`(动画定时函数)使动画线性化，`animation-timing-function`的默认值是`ease`。
<iframe id="cp_embed_vRBGwv" src="//codepen.io/supersarkar/embed/vRBGwv?height=410&amp;theme-id=1&amp;slug-hash=vRBGwv&amp;default-tab=result&amp;user=supersarkar&amp;embed-version=2&amp;pen-title=Arc-Reactor-Linear-Infinite" scrolling="no" frameborder="0" height="410" allowtransparency="true" allowfullscreen="true" name="CodePen Embed" title="Arc-Reactor-Linear-Infinite" class="cp_embed_iframe " style="width: 100%; overflow: hidden; height: 100%;"></iframe>
我们可以组合所有这些动画属性。...
```css
animation-name: reactor-anim;
animation-duration: 3s;
animation-iteration-count: infinite;
animation-timing-function: linear;
```
...缩写属性可以写成这样:

```css
animation: 3s infinite linear reactor-anim;
```
## 反应堆容器最后的绝技
我们的反应堆准备好了，现在让我们做一些`.reactor-container`最后的改变。
首先，我们需要反应堆后面的一个暗圈：
```HTML
<div class="fullpage-wrapper">
  <div class="reactor-container">
    <!-- dark circle behind the reactor -->
    <div class="reactor-container-inner circle abs-center"></div>
    <div class="tunnel circle abs-center"></div>
    <div class="core-wrapper circle abs-center"></div>
    <div class="core-outer circle abs-center"></div>
    <div class="core-inner circle abs-center"></div>
    <div class="coil-container">
      <div class="coil coil-1"></div>
      <div class="coil coil-2"></div>
      <div class="coil coil-3"></div>
      <div class="coil coil-4"></div>
      <div class="coil coil-5"></div>
      <div class="coil coil-6"></div>
      <div class="coil coil-7"></div>
      <div class="coil coil-8"></div>
    </div>
  </div>
</div>
```
让我们给一个黑暗的背景，并添加一些光影：
```css
.reactor-container-inner {
  height: 238px;
  width: 238px;
  background-color: rgb(22, 26, 27);;
  box-shadow: 0px 0px 4px 1px #52fefe;
}
```
<iframe id="result-iframe" sandbox="allow-forms allow-modals allow-pointer-lock allow-popups allow-same-origin allow-scripts" allow="geolocation; microphone; camera; midi; vr" src="https://s.codepen.io/supersarkar/fullembedgrid/wmwWwB?type=embed&amp;animations=run" allowtransparency="true" frameborder="0" scrolling="yes" allowpaymentrequest="true" allowfullscreen="true" name="CodePen Preview for Arc-Reactor-Semi-Final" title="CodePen Preview for Arc-Reactor-Semi-Final" data-src="https://s.codepen.io/supersarkar/fullembedgrid/wmwWwB?type=embed&amp;animations=run"></iframe>
看到黑暗的背景和光影是如何产生浮雕效果的吗？
接下来，让我们使`.rotator-container`转起来，并给它一些阴影和边框，然后我们完成了：
```css
.reactor-container {
  width: 300px;
  height: 300px;
  margin: auto;
  border: 1px dashed #888;
  position: relative;
  border-radius: 50%;
  background-color: #384c50;
  border: 1px solid rgb(18, 20, 20);
  box-shadow: 0px 0px 32px 8px rgb(18, 20, 20), 0px 0px 4px 1px rgb(18, 20, 20) inset;
}
```
<iframe id="cp_embed_QmLEWN" src="//codepen.io/supersarkar/embed/QmLEWN?height=425&amp;theme-id=1&amp;slug-hash=QmLEWN&amp;default-tab=result&amp;user=supersarkar&amp;embed-version=2&amp;pen-title=Iron%20Man's%20Arc%20Reactor" scrolling="no" frameborder="0" height="425" allowtransparency="true" allowfullscreen="true" name="CodePen Embed" title="Iron Man's Arc Reactor" class="cp_embed_iframe " style="width: 100%; overflow: hidden; height: 100%;"></iframe>
Cheers!我们的弧形反应堆已经准备好了，甚至还有一点动画作为额外的奖励。为了提高这一点，我们可以探索使用自定义属性为颜色和数字值创建可重用的变量，以便于维护。
类似地，我们可以使用预处理器--比如Sass、Less或PostCSS--来编写函数，为我们完成效率的提升。希望能在评论中看到这样的例子！


## 原文相关资料

#### Creating Yin and Yang Loaders On the Web
I came across a couple such animations a while ago and this gave me the idea of 


#### Creating a CSS Sliding Background Effect
The "trick" of sliding backgrounds in CSS is not new. In fact, the first time I 
              
#### The State of CSS Reflections
I recently saw this loader on CodePen, a pure CSS 3D rotating set of bars with a 



