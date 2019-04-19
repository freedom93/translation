# shape-outside

2017年8月19日,由ROBIN RENDLE最后更新 [原文地址](https://css-tricks.com/almanac/properties/s/shape-outside/)

标签：BASE-SHAPE、SHAPE-OUTSIDE

shape-outside属性控制内容将环绕一个浮动元素的限定框。通常这样文本可以回流形状成一个圆,椭圆或一个多边形:


```css
.element {
  float: left;
  shape-outside: circle(50%);
  width: 200px;
  height: 200px;
}
```
<figure id="post-203845" class="align-none media-203845"><img sizes="(min-width: 1850px) calc( (100vw - 555px) / 3 )
       (min-width: 1251px) calc( (100vw - 530px) / 2 )
       (min-width: 1086px) calc(100vw - 480px)
       (min-width: 626px)  calc(100vw - 335px)
                           calc(100vw - 30px)" srcset="https://cdn.css-tricks.com/wp-content/uploads/2015/06/shape-outside.png 1550w, https://cdn.css-tricks.com/wp-content/uploads/2015/06/shape-outside-300x135.png 300w, https://cdn.css-tricks.com/wp-content/uploads/2015/06/shape-outside-1024x460.png 1024w" src="//cdn.css-tricks.com/wp-content/uploads/2015/06/shape-outside.png" alt=""></figure>

重要的是，要注意这个属性只能在浮动元素中生效,尽管未来可能会改变。```shape-outside```属性也可以处理[transitions or animations](http://codepen.io/robinrendle/pen/4275e31f9e95882054d400741b010dc6?editors=110)。

# Values
<ul>
	<li><code>circle()</code>: 绘制圆形</li> 
    <li><code>ellipse()</code>: 绘制椭圆形</li> 
    <li><code>inset()</code>: 绘制方形</li> 
    <li><code>polygon()</code>: 绘制多边形</li> 
    <li><code>url()</code>: 制定文字环绕的图像路径</li> 
    <li><code>initial</code>: 默认值（？？the float area is unaffected.）</li> 
    <li><code>inherit</code>: 可以继承父标签的<code>shape-outside</code> 属性值</li> 
</ul>

以下[盒模型](https://css-tricks.com/the-css-box-model)的参考值应该用于定位形状:

<ul>
	<li><code>margin-box</code></li>
    <li><code>padding-box</code></li>
    <li><code>border-box</code></li>
</ul>

这些值应该附加到最后,例如:```shape-outside```: ```circle(50% at 0 0) padding-box```。默认使用 ```margin-box```。

# ellipse()

```css
.element {
  shape-outside: ellipse(150px 300px at 50% 50%);
}
```

<code>ellipse()</code>函数要求形状的半径值x,y轴的椭圆坐标位置在其边界框的中心。例如上面的示例将椭圆的中心位置在垂直和水平方向在```.element```div的中心:

<div class="cp_embed_wrapper resizable" style="height: 268px;">
<iframe id="cp_embed_7fa99015d63597648d5e312c5b73ac25" src="//codepen.io/css-tricks/embed/7fa99015d63597648d5e312c5b73ac25?height=268&amp;theme-id=1&amp;slug-hash=7fa99015d63597648d5e312c5b73ac25&amp;default-tab=result&amp;user=css-tricks" scrolling="no" frameborder="0" height="268" allowtransparency="true" allowfullscreen="true" allowpaymentrequest="true" name="CodePen Embed" title="CodePen Embed 6" class="cp_embed_iframe " style="width: 100%; overflow: hidden; height: 100%;"></iframe>
</div>

上述演示显示我们正在改变```div```的形状，但是如果我们添加边框和背景图像,我们会发现这个边界框实际上仍然矩形:

<div class="cp_embed_wrapper resizable" style="height: 268px;">
<iframe id="cp_embed_5e47a80626dfa27a42dd18a0e2b8450b" src="//codepen.io/css-tricks/embed/5e47a80626dfa27a42dd18a0e2b8450b?height=268&amp;theme-id=1&amp;slug-hash=5e47a80626dfa27a42dd18a0e2b8450b&amp;default-tab=result&amp;user=css-tricks" scrolling="no" frameborder="0" height="268" allowtransparency="true" allowfullscreen="true" allowpaymentrequest="true" name="CodePen Embed" title="CodePen Embed 5" class="cp_embed_iframe " style="width: 100%; overflow: hidden; height: 100%;"></iframe>
</div>

这样想可能更好:```shape-outside```属性改变元素与周围的其他元素之间的关系,而不是几何元素的本身。我们需要使用 ```shape-outside```与```clip-path()```属性修正它,比如在这个例子中:

<div class="cp_embed_wrapper resizable" style="height: 268px;">
<iframe id="cp_embed_4e5420d8c1a2766b25dd3c98f684bf9c" src="//codepen.io/css-tricks/embed/4e5420d8c1a2766b25dd3c98f684bf9c?height=268&amp;theme-id=1&amp;slug-hash=4e5420d8c1a2766b25dd3c98f684bf9c&amp;default-tab=result&amp;user=css-tricks" scrolling="no" frameborder="0" height="268" allowtransparency="true" allowfullscreen="true" allowpaymentrequest="true" name="CodePen Embed" title="CodePen Embed 4" class="cp_embed_iframe " style="width: 100%; overflow: hidden; height: 100%;"></iframe>
</div>

# circle()

```css
.element {
  shape-outside: circle(50%);
}
```

这个函数创建一个圆,在上面的代码示例中,将创建一个半径是```.element```一半高度和宽度的圆。```circle()```函数也可以使用相同的语法在内部定位形状。

# url()

```css
.element {
  shape-outside: url('circle.png');
}
```

在这个例子中,我们有两个浮动图像,每个边上有一个文本块。因为两张图片设置了```shape-outside```属性，然后下面的文本就会避免浮动。

<div class="cp_embed_wrapper resizable" style="height: 268px;">
<iframe id="cp_embed_fbe5379f499f072e55fa1e4fbab5c8d5" src="//codepen.io/css-tricks/embed/fbe5379f499f072e55fa1e4fbab5c8d5?height=268&amp;theme-id=1&amp;slug-hash=fbe5379f499f072e55fa1e4fbab5c8d5&amp;default-tab=result&amp;user=css-tricks" scrolling="no" frameborder="0" height="268" allowtransparency="true" allowfullscreen="true" allowpaymentrequest="true" name="CodePen Embed" title="CodePen Embed 3" class="cp_embed_iframe " style="width: 100%; overflow: hidden; height: 100%;"></iframe>
</div>

也可以设置```shape-image-threshold```属性告诉浏览器一个图片的像素阀值,浏览器根据其透明度创建一个形状。例如:

```css
.element {
  shape-outside: url('image.png');
  shape-image-threshold: 0.5;
}
```

在这个例子中根据唯一的像素阀值,创建上面的形状将会有50%的透明度。```shape-image-threshold```属性的值```0.0```(透明)到```1.0``(不透明)都是有效的。

# polygon()

```css
.element {
  shape-outside: polygon(0 0, 0 200px, 300px 600px);
}
```

这个函数创建任何有三个或三个以上顶点的形状,例如:

<div class="cp_embed_wrapper resizable" style="height: 268px;">
<iframe id="cp_embed_4e5420d8c1a2766b25dd3c98f684bf9c" src="//codepen.io/css-tricks/embed/4e5420d8c1a2766b25dd3c98f684bf9c?height=268&amp;theme-id=1&amp;slug-hash=4e5420d8c1a2766b25dd3c98f684bf9c&amp;default-tab=result&amp;user=css-tricks" scrolling="no" frameborder="0" height="268" allowtransparency="true" allowfullscreen="true" allowpaymentrequest="true" name="CodePen Embed" title="CodePen Embed 4" class="cp_embed_iframe " style="width: 100%; overflow: hidden; height: 100%;"></iframe>
</div>

需要注意的是,如果这个属性将是动画，当你声明动画状态时需要相同数量的顶点:

```css
.element {
  shape-outside: polygon(0 0, 100% 0, 100% 100%, 0 100%);
  transition: shape-outside 1s;
}
.element:hover {
	shape-outside: polygon(0 0, 100% 50%, 100% 50%, 0 100%);
}
```

# inset()

```css
.element {
  shape-outside: inset(100px 100px 100px 100px 10px);
  /* shape-outside: inset(top right bottom left border-radius); */
}
```

```inset()```是一个绘制方形形状的函数,它需要五个参数,但第五参数,```border-radius``` 是可选的。其他参数偏移量从 ```.element```的边缘向内:

<div class="cp_embed_wrapper resizable" style="height: 268px;">
<iframe id="cp_embed_b2da5018d8f20ac3a2ccc26edb724db6" src="//codepen.io/css-tricks/embed/b2da5018d8f20ac3a2ccc26edb724db6?height=268&amp;theme-id=1&amp;slug-hash=b2da5018d8f20ac3a2ccc26edb724db6&amp;default-tab=result&amp;user=css-tricks" scrolling="no" frameborder="0" height="268" allowtransparency="true" allowfullscreen="true" allowpaymentrequest="true" name="CodePen Embed" title="CodePen Embed 1" class="cp_embed_iframe " style="width: 100%; overflow: hidden; height: 100%;"></iframe>
</div>

上面有一个200px宽、200px高的元素,除了左边，我们在其他各个方向偏移50px。这种方式div虽然延伸到顶部,但上面的文本将围绕形状。

# Related properties
<ul>
 <li><a href="https://css-tricks.com/almanac/properties/c/clip/">clip-path</a></li>
</ul>

# Other resoutces
<ul>
 <li><a href="http://www.w3.org/TR/css-shapes/#funcdef-ellipse">CSS Shapes on W3C</a></li>
 <li><a href="https://developer.mozilla.org/en-US/docs/Web/CSS/shape-outside">shape-outside on MDN</a></li>
 <li><a href="http://www.html5rocks.com/en/tutorials/shapes/getting-started">Getting started with CSS Shapes</a></li>
 <li><a href="http://alistapart.com/article/css-shapes-101">CSS Shapes on A List Apart</a></li>
</ul>

# Browser support

浏览器支持数据来自[Caniuse](http://caniuse.com/#feat=css-shapes),那里有更多的细节。以下数据表明浏览器支持,版本和特性。

<div class="caniuse"><div class="caniuse-header"><h4 id="article-header-id-9" class="has-header-link"><a class="article-headline-link" href="#article-header-id-9">#</a>Desktop</h4><table class="browser-support-table"><thead><tr><th class="chrome"><span>Chrome</span></th><th class="opera"><span>Opera</span></th><th class="firefox"><span>Firefox</span></th><th class="ie"><span>IE</span></th><th class="edge"><span>Edge</span></th><th class="safari"><span>Safari</span></th></tr></thead><tbody><tr><td class="y yep" title="Chrome - " data-browser-name="Chrome"><span class="caniuse-agents-version version">37</span></td><td class="y yep" title="Opera - " data-browser-name="Opera"><span class="caniuse-agents-version version">24</span></td><td class="n nope" title="Firefox - " data-browser-name="Firefox"><span class="caniuse-agents-version version">No</span></td><td class="n nope" title="IE - " data-browser-name="IE"><span class="caniuse-agents-version version">No</span></td><td class="n nope" title="Edge - " data-browser-name="Edge"><span class="caniuse-agents-version version">No</span></td><td class="y yep" title="Safari - " data-browser-name="Safari"><span class="caniuse-agents-version version">7.1*</span></td></tr></tbody></table></div><div class="caniuse-section"><h4 id="article-header-id-10" class="has-header-link"><a class="article-headline-link" href="#article-header-id-10">#</a>Mobile / Tablet</h4><table class="browser-support-table"><thead><tr><th class="ios_saf"><span>iOS Safari</span></th><th class="op_mob"><span>Opera Mobile</span></th><th class="op_mini"><span>Opera Mini</span></th><th class="android"><span>Android</span></th><th class="and_chr"><span>Android Chrome</span></th><th class="and_ff"><span>Android Firefox</span></th></tr></thead><tbody><tr><td class="y yep" title="iOS Safari - " data-browser-name="iOS Safari"><span class="caniuse-agents-version version">8*</span></td><td class="y yep" title="Opera Mobile - " data-browser-name="Opera Mobile"><span class="caniuse-agents-version version">37</span></td><td class="n nope" title="Opera Mini - " data-browser-name="Opera Mini"><span class="caniuse-agents-version version">No</span></td><td class="y yep" title="Android - " data-browser-name="Android"><span class="caniuse-agents-version version">62</span></td><td class="y yep" title="Android Chrome - " data-browser-name="Android Chrome"><span class="caniuse-agents-version version">64</span></td><td class="n nope" title="Android Firefox - " data-browser-name="Android Firefox"><span class="caniuse-agents-version version">No</span></td></tr></tbody></table></div></div>












