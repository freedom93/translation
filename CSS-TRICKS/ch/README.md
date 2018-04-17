# 使用CSS变换和动画实现钢铁侠电弧反应堆

Kunal Sarkar 2018.4.2  动画 变换

钢铁侠粉丝们好，发动你的代码编辑！ 我们将使用CSS实现钢铁侠套装的弧形反应堆。 以下是最终结果的样子：

<div class="cp_embed_wrapper resizable" style="height: 400px;">
    <iframe id="cp_embed_QmLEWN" src="//codepen.io/supersarkar/embed/QmLEWN?height=400&amp;theme-id=1&amp;slug-hash=QmLEWN&amp;default-tab=result&amp;user=supersarkar&amp;embed-version=2&amp;pen-title=Iron%20Man's%20Arc%20Reactor" scrolling="no" frameborder="0" height="400" allowtransparency="true" allowfullscreen="true" name="CodePen Embed" title="Iron Man's Arc Reactor" class="cp_embed_iframe " style="width: 100%; overflow: hidden; height: 100%;"></iframe>
</div>

## 满屏wrapper

我们把弧形反应堆放在一个黑色背景的满屏页上。 这是我们的代码来制作一个完整的页面wrapper元素：

 ```css
 body {
  margin: 0;
}

.fullpage-wrapper {
  height: 100vh;
  background: radial-gradient(#353c44, #222931);
}
```

为什么我们要声明没有外边距的body？ 默认情况下，#body元素在用户代理样式表中设置了一些外边距。 这可以防止<body>内的元素接触屏幕的边缘。由于我们希望我们的wrapper覆盖整个屏幕，所以我们通过将<body>元素的默认边距设置为0来移除它的外边距。

我们设置.fullpage-wrapper类为视口的整个高度。 我们不必指定宽度，因为默认情况下div是全宽度。通过将元素的宽度和高度都设置为100％，我们可以采用另一种方法，但随着更多元素添加到屏幕中，这会带来一些可能的缺点。使用视口单位可确保我们的wrapper始终占据屏幕的整个垂直空间，而不管它是什么或添加了什么元素到布局上。

我们在wrapper上还使用CSS函数radial-gradient()实现径向渐变效果。 函数内部的参数是颜色的起点和终点。 因此，背景的中心将从＃353c44往＃222931渐变。 这是微妙的，也是个不错的尝试。

 <figure id="post-268738" class="align-none media-268738"><img src="https://cdn.css-tricks.com/wp-content/uploads/2018/03/ironman-1.jpg" srcset="https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_714,f_auto,q_auto/v1521762064/ironman-1_o38vzq.jpg 714w, https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_200,f_auto,q_auto/v1521762064/ironman-1_o38vzq.jpg 200w" sizes="(min-width: 1850px) calc( (100vw - 555px) / 3 )
(min-width: 1251px) calc( (100vw - 530px) / 2 )
(min-width: 1086px) calc(100vw - 480px)
(min-width: 626px)  calc(100vw - 335px)
calc(100vw - 30px)" alt=""></figure>


##反应堆容器居中

在我们开始创建反应堆之前，为它创建一个居中的容器：

```css
.reactor-container {
  width: 300px;
  height: 300px;
  margin: auto;
  border: 1px dashed #888;
}
```

我们给出一个带虚线的300px x 300px框。 声明margin外边距值为auto; 确保水平方向居中。

<figure id="post-268739" class="align-none media-268739"><img src="https://cdn.css-tricks.com/wp-content/uploads/2018/03/ironman-2.jpg" srcset="https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_947,f_auto,q_auto/v1521762066/ironman-2_c7jsda.jpg 947w, https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_200,f_auto,q_auto/v1521762066/ironman-2_c7jsda.jpg 200w" sizes="(min-width: 1850px) calc( (100vw - 555px) / 3 )
(min-width: 1251px) calc( (100vw - 530px) / 2 )
(min-width: 1086px) calc(100vw - 480px)
(min-width: 626px)  calc(100vw - 335px)
calc(100vw - 30px)" alt=""></figure>

但是它为什么不垂直方向居中呢？
根据CSS2规范，如果我们给左边和右边的自动外边距，那么整个可用空间将平分为左右边距。 尽管如此，顶部和底部边缘的情况并非如此。 对于顶部和底部外边距，CSS2规范说：

```
If margin-top, or margin-bottom are auto, their used value is 0.
```
如果上外边距和下外边距的值是auto，它们会认为值是0.

然而，我们确实还有一个好消息。 Flexbox布局遵循新的对齐规则，以下是Flexbox规范的说明：

```
Prior to alignment via justify-content and align-self, any positive free space is distributed to auto margins in that dimension.
```

通过justify-content和align-self进行对齐之前，任何可用d的自由空间都将分配给该维度中的自动外边距。

这意味着如果考虑的元素显示为弹性布局，则margin：auto; 将在水平和垂直两个方向上生效。 让我们将wrapper设置为一个弹性容器，其子元素形成弹性布局：

```css
.fullpage-wrapper {
  width: 100%;
  height: 100vh;
  background: radial-gradient(#353c44, #222931);
  display: flex;
}
```

然后，这就好多了：

![avatar](//cdn.css-tricks.com/wp-content/uploads/2018/03/ironman-3.jpg)

还有许多其他方法可以将元素集中在HTML中。 这是一个详细的可以了解更多关于让元素居中的CSS技巧指南。

## The Reactor Core: Concentric Circles in CSS
We know that new elements in HTML are created from left to right (for left-to-right languages), or top to bottom. Elements never overlap, until you provide some negative margin.

So, how are we going to display concentric circles? We will use absolute positioning.

The default value of position property is static. Static and relative positioning follow the flow of top to bottom and left to right. However, an absolutely positioned element is not treated as a part of the document flow and can be positioned anywhere using the top, right, bottom and left properties.

Let’s start by creating the smallest circle:

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
![avatar](//cdn.css-tricks.com/wp-content/uploads/2018/03/ironman-4.jpg)


We need to center this div. You might be tempted to apply the same flexbox concept we used on the reactor element to center this circle as well. But, here’s what CSS2 spec has to say about setting margin: auto; on absolutely positioned elements:

```
If none of the three (top, height, and bottom) are auto: If both margin-top and margin-bottom are auto, solve the equation under the extra constraint that the two margins get equal values.
```

This means if an absolutely positioned element has any value for top, height and bottom other than auto, then setting the top and bottom margin to auto will center the element vertically.

Same case for horizontal centering: if an absolutely positioned element has any value for left, width and right other than auto, then setting the left and right margin to auto will center the element horizontally.

That means we don’t need flexbox layout to center an absolutely positioned element with a known height and width. We just have to make sure that we give some value to top, right, bottom and left other than auto. So, we will use 0:

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

We do not want to repeat these five lines for all the concentric circles we are going to have, so let’s create a separate class for this. We also don’t want to define border-radius: 50%; for all the divs that we want to display as circles, so we will create a class for that too:


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

Also, add these new classes to out .core-inner element:

```HTML
<div class="fullpage-wrapper">
  <div class="reactor-container">
    <!-- the smallest circle -->
    <div class="core-inner circle abs-center"></div>
  </div>
</div>
```

![avatar](//cdn.css-tricks.com/wp-content/uploads/2018/03/ironman-5.jpg)

Okay, our concentric circle is centered. Let’s make it glow.

But CSS doesn’t have any "glow" property.

Don’t worry, we have the box-shadow property. Instead of giving the shadow a dark color, we will give it a bright color to make the shadow look like glow. Pretty clever, isn’t it? 😉

Let’s do this:

```css
.core-inner {
  width: 70px;
  height: 70px;
  border: 5px solid #1b4e5f;
  background-color: #fff;
  box-shadow: 0px 0px 7px 5px #52fefe;
}
```

![avatar](//cdn.css-tricks.com/wp-content/uploads/2018/03/ironman-6.jpg)

Let’s take a break and understand the syntax of box-shadow first because we will be using it a lot. Here are what those values for box-shadow mean in that order:

x-offset: how much we want to push the shadow on the right side (x-axis). Negative values will push the shadow to the left side.
y-offset: how much we want to push the shadow up or down (y-axis).
blur-radius: how blurry we want our shadow to be.
spread-radius: how much we want our shadow to spread.
color: color of the shadow.
Play with these values a bit to see their effects in real time.

In real life, shadows don’t drop only outside of an object. Shadows drop upon the objects too. Imagine a pit dug by a dog, it will have a shadow inside it, right?

We can give a shadow inside an element using the inset keyword in the box-sizing property. To give an element both, outside and inside shadow, we simply separate them with a comma. Let’s do this to get an outside and inside glow to our reactor’s inner core:


```css
.core-inner {
  width: 70px;
  height: 70px;
  border: 5px solid #1B4e5f;
  background-color: #fff;
  box-shadow: 0px 0px 7px 5px #52fefe, 0px 0px 10px 10px #52fefe inset;
}
```

![avatar](//cdn.css-tricks.com/wp-content/uploads/2018/03/ironman-7.jpg)


Now it’s starting to look sci-fi!

Let’s create one more circle on top. We want the inner circle to display on top of the other circles, so we will add new circle divs *above* the inner-circle in code:


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

The elements down in the code, are displayed above on the screen. If we put the core-outer below the core-inner in the code, then core-inner won’t be visible, because core-outer will cover it.

Let’s give style to outer-code. The outer core will be a little bigger than the inner core and we will give an outer and inner glow to core-outer too:

```css
.core-outer {
  width: 120px;
  height: 120px;
  border: 1px solid #52fefe;
  background-color: #fff;
  box-shadow: 0px 0px 2px 1px #52fefe, 0px 0px 10px 5px #52fefe inset;
}
```

![avatar](//cdn.css-tricks.com/wp-content/uploads/2018/03/ironman-8.jpg)


I want you to do one thing: look at the shadows (glow) and try to identify which one is of which circle. There are four shadows and two circles (until now).

To finish designing the core, we will need one more circle that will wrap the inner and outer circles:

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


This one will be a little bigger, and will again have same shadows, we will use a dark background for core-wrapper:

```css
.core-wrapper {
  width: 180px;
  height: 180px;
  background-color: #073c4b;
  box-shadow: 0px 0px 5px 4px #52fefe, 0px 0px 6px 2px #52fefe inset;
}
```

![avatar](//cdn.css-tricks.com/wp-content/uploads/2018/03/ironman-9.jpg)


##Creating Reactor Coils and Rotating with CSS3 Transforms


We have the core of the reactor, now we need a tunnel around the core. Actually, we can create an illusion of a round tunnel by drawing just one more circle little bigger than the core-wrapper. Let’s do it:

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

...a little wider and add same glow to the tunnel:


```css
.tunnel {
  width: 220px;
  height: 220px;
  background-color: #fff;
  box-shadow: 0px 0px 5px 1px #52fefe, 0px 0px 5px 4px #52fefe inset;
}
```

![avatar](//cdn.css-tricks.com/wp-content/uploads/2018/03/ironman-10.jpg)

Our tunnel is ready.

Make sure you do not just copy paste the code. Have a look at the glows of the circles and identify which glow is of which circle, whether it is outside glow or inset glow.

Now, we need eight coils on this tunnel. The coils are simple rectangles, but the major challenge is that we need the coils to run along the round path of the tunnel; not in straight line.

One way to do this would be to create eight small rectangles, shift their center to the center of the reactor, and rotate each coil by an increasing angle (in multiples of 45deg).

Let’s not complicate it and make one rectangle coil at a time:


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

![avatar](//cdn.css-tricks.com/wp-content/uploads/2018/03/ironman-11.jpg)

Now, we want to place this coil in the center at top of the tunnel. Like this:


![avatar](//cdn.css-tricks.com/wp-content/uploads/2018/03/ironman-12.jpg)

Our reactor-container is 300px x 300px, so the center is at 150px from top and left. The tunnel is 220px wide, so its radius will be 110px. This gives us the top offset of the coil: 150px - 110px.

We can keep left of the coil to 150px, but since our coil is 30px wide, it will shift the middle of the coil by 15px to right, that’s why we need to subtract 15px from 150px to get the left offset of the coil.

We can either calculate these ourselves and put the value, or we can use the CSS calc() function. Let’s use the CSS calc() function to calculate the top and left properties of the coil:

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

![avatar](//cdn.css-tricks.com/wp-content/uploads/2018/03/ironman-13.jpg)


As you can see, the calc() function takes a mathematical expression as its argument and solves it.

Now we need eight such coils but they must lie on the tunnel. To do that, as discussed, we can simply place the eight coils at this same place, then transform their origin to the center of the reactor, and rotate each coil by an increment of 45 degrees.

We need to update the coil’s origin because by default it is set to the center of the coil; we want it at center of the reactor:


![avatar](//cdn.css-tricks.com/wp-content/uploads/2018/03/ironman-14.jpg)


We will use transform-origin property to set the origin of the coil:


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


The first value, 15px, in transform-origin is the x-offset (horizontal distance) from the top-left corner of the element, and the second value, 110px, is the y-offset (vertical distance) from the top-left corner of the element.

The coil’s origin is now at the center of the reactor, let’s rotate it by 45 degrees using the CSS3 transform property and see what happens:

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

![avatar](//cdn.css-tricks.com/wp-content/uploads/2018/03/ironman-15.jpg)


Great! That’s exactly what we want.

Before creating all the eight coils, let’s create a coil container div that will contain all the eight coils:

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

You will notice we also added a class "coil" to the "coil-1" element. We will keep all the common styles for coils in the "coil" class, and the individual coil element classes will only have their angle of rotation:

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

The output will remain same.

Now, let’s make all the eight coils inside .coil-container:


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

...and give different rotations to all the coils (in increment of 45 degrees):

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

![avatar](//cdn.css-tricks.com/wp-content/uploads/2018/03/ironman-16.jpg)


Our reactor is almost ready.

## Animating the Coils With CSS3 Animations

In Iron Man’s Arc reactor, the coils don’t move but they will in our reactor. We will animate the coils to rotate along the tunnel and will use CSS3 animations for this—no JavaScript.

To create an animation, you need to know the initial and final states of the object you are going to animate. We define these initial and final states in CSS by using @keyframes at-rule:

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

We want the element to be at 0 degrees and animate it until it reaches 360 degrees. And we named this animation as "reactor-anim."

The element we want to animate is .coil-contailer. Notice, we didn’t define which object to animate yet, we have only defined the initial and the final state and name of the animation.

We need to link the element to the animation in order to take effect. We do it by using animation-name property on .coil-container:


```css
.coil-container {
  position: relative;
  width: 100%;
  height: 100%;
  animation-name: reactor-anim;
  animation-duration: 3s;
}
```

Notice, we also gave the duration of animation using animation-duration property. This defines how much time it should take to go from the “from” state to the “to” state defined using the @keyframes at-rule.

<iframe id="cp_embed_GxKZee" src="//codepen.io/supersarkar/embed/GxKZee?height=415&amp;theme-id=1&amp;slug-hash=GxKZee&amp;default-tab=result&amp;user=supersarkar&amp;embed-version=2&amp;pen-title=Arc-Reactor-Ease-In" scrolling="no" frameborder="0" height="415" allowtransparency="true" allowfullscreen="true" name="CodePen Embed" title="Arc-Reactor-Ease-In" class="cp_embed_iframe " style="width: 100%; overflow: hidden; height: 100%;"></iframe>


We need to change two things here: we want the animation to go on infinitely and we want a linear animation. You can see the animation is slow at the beginning, then fast, then again slow at the end—this behavior is defined by the timing function of an animation.

Let’s make these changes:

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

We used animation-iteration-count property to set the animation to infinite, and animation-timing-function to make the animation linear, the default value of animation-timing-function is ease.

<iframe id="cp_embed_vRBGwv" src="//codepen.io/supersarkar/embed/vRBGwv?height=410&amp;theme-id=1&amp;slug-hash=vRBGwv&amp;default-tab=result&amp;user=supersarkar&amp;embed-version=2&amp;pen-title=Arc-Reactor-Linear-Infinite" scrolling="no" frameborder="0" height="410" allowtransparency="true" allowfullscreen="true" name="CodePen Embed" title="Arc-Reactor-Linear-Infinite" class="cp_embed_iframe " style="width: 100%; overflow: hidden; height: 100%;"></iframe>

We can combine all of these animation properties...

```css
animation-name: reactor-anim;
animation-duration: 3s;
animation-iteration-count: infinite;
animation-timing-function: linear;
```

...into one shorthand property like this:

```css
animation: 3s infinite linear reactor-anim;
```

##Final Touches to the Reactor Container

Our reactor is ready, now let’s make some final changes to the .reactor-container. First, we will need one dark circle behind the reactor:


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

Let’s give a dark background and add some glow to it:


```css
.reactor-container-inner {
  height: 238px;
  width: 238px;
  background-color: rgb(22, 26, 27);;
  box-shadow: 0px 0px 4px 1px #52fefe;
}
```

<iframe id="result-iframe" sandbox="allow-forms allow-modals allow-pointer-lock allow-popups allow-same-origin allow-scripts" allow="geolocation; microphone; camera; midi; vr" src="https://s.codepen.io/supersarkar/fullembedgrid/wmwWwB?type=embed&amp;animations=run" allowtransparency="true" frameborder="0" scrolling="yes" allowpaymentrequest="true" allowfullscreen="true" name="CodePen Preview for Arc-Reactor-Semi-Final" title="CodePen Preview for Arc-Reactor-Semi-Final" data-src="https://s.codepen.io/supersarkar/fullembedgrid/wmwWwB?type=embed&amp;animations=run"></iframe>


See how the dark background and the glow creates an emboss effect?

Next, let’s make the .rotator-container round and give it some shadow and border, then we are done:

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


Cheers! Our Arc Reactor is ready and even with a little animation as an added bonus. To level this up, we could explore using custom properties to create reusable variables for our color and number values for easier maintenance. Similarly, we could look into using a preprocessor—like Sass, Less or PostCSS—to write functions that do the mathematical lifting for us. Would love to see examples like that in the comments!


## Related

#### Creating Yin and Yang Loaders On the Web
I came across a couple such animations a while ago and this gave me the idea of 


#### Creating a CSS Sliding Background Effect
The "trick" of sliding backgrounds in CSS is not new. In fact, the first time I 
              
#### The State of CSS Reflections
I recently saw this loader on CodePen, a pure CSS 3D rotating set of bars with a 



