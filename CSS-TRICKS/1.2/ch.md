# shape-outside

2017年8月19日,由ROBIN RENDLE最后更新 [原文地址](https://css-tricks.com/almanac/properties/s/shape-outside/)

标签：BASE-SHAPE、SHAPE-OUTSIDE

The shape-outside property controls how content will wrap around a floated element’s bounding-box. Typically this is so that text can reflow over a shape such as a circle, ellipse or a polygon:

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

It’s important to note that this property will only work on floated elements for now, although this is likely to change in the future. The ```shape-outside``` property can also be manipulated with [transitions or animations].

# Values
<ul>
	<li><code>circle()</code>: for making circular shapes.</li> 
    <li><code>ellipse()</code>: for making elliptical shapes.</li> 
    <li><code>inset()</code>: for making rectangular shapes.</li> 
    <li><code>polygon()</code>: for creating any shape with 3 or more vertices.</li> 
    <li><code>url()</code>: identifies which image should be used to wrap text around.</li> 
    <li><code>initial</code>: the float area is unaffected.</li> 
    <li><code>inherit</code>: inherits <code>shape-outside</code> value from parent.</li> 
</ul>

The following values identify which reference of [the box model] should be used for positioning the shape within:

<ul>
	<li><code>margin-box</code></li>
    <li><code>padding-box</code></li>
    <li><code>border-box</code></li>
</ul>

These values should be appended to the end, for instance: ```shape-outside```: ```circle(50% at 0 0) padding-box```. By default the ```margin-box``` reference will be used.

# ellipse()

```css
.element {
  shape-outside: ellipse(150px 300px at 50% 50%);
}
```

The ```ellipse()``` function requires the radii values for the x, y axis of the ellipse followed by the coordinates to position the center of the shape within its bounding box. For instance the example above will position the center of the ellipse in the vertical and horizontal center of the ```.element``` div:

<div class="cp_embed_wrapper resizable" style="height: 268px;">
<iframe id="cp_embed_7fa99015d63597648d5e312c5b73ac25" src="//codepen.io/css-tricks/embed/7fa99015d63597648d5e312c5b73ac25?height=268&amp;theme-id=1&amp;slug-hash=7fa99015d63597648d5e312c5b73ac25&amp;default-tab=result&amp;user=css-tricks" scrolling="no" frameborder="0" height="268" allowtransparency="true" allowfullscreen="true" allowpaymentrequest="true" name="CodePen Embed" title="CodePen Embed 6" class="cp_embed_iframe " style="width: 100%; overflow: hidden; height: 100%;"></iframe>
</div>

Although the demo above may suggest that we’re changing the shape of the ```div``` itself, if we add borders and a background-image we’ll find that the bounding box is in fact still rectangular:

<div class="cp_embed_wrapper resizable" style="height: 268px;">
<iframe id="cp_embed_5e47a80626dfa27a42dd18a0e2b8450b" src="//codepen.io/css-tricks/embed/5e47a80626dfa27a42dd18a0e2b8450b?height=268&amp;theme-id=1&amp;slug-hash=5e47a80626dfa27a42dd18a0e2b8450b&amp;default-tab=result&amp;user=css-tricks" scrolling="no" frameborder="0" height="268" allowtransparency="true" allowfullscreen="true" allowpaymentrequest="true" name="CodePen Embed" title="CodePen Embed 5" class="cp_embed_iframe " style="width: 100%; overflow: hidden; height: 100%;"></iframe>
</div>

It might be better to think of it this way: with the ```shape-outside``` property we’re changing the relationship of other elements around an element, not the geometry of the element itself. To fix that we’ll need to use ```shape-outside``` alongside the ```clip-path()``` property, such as in this example:

<div class="cp_embed_wrapper resizable" style="height: 268px;">
<iframe id="cp_embed_4e5420d8c1a2766b25dd3c98f684bf9c" src="//codepen.io/css-tricks/embed/4e5420d8c1a2766b25dd3c98f684bf9c?height=268&amp;theme-id=1&amp;slug-hash=4e5420d8c1a2766b25dd3c98f684bf9c&amp;default-tab=result&amp;user=css-tricks" scrolling="no" frameborder="0" height="268" allowtransparency="true" allowfullscreen="true" allowpaymentrequest="true" name="CodePen Embed" title="CodePen Embed 4" class="cp_embed_iframe " style="width: 100%; overflow: hidden; height: 100%;"></iframe>
</div>

# circle()

```css
.element {
  shape-outside: circle(50%);
}
```
This function creates a circle, and in the code example above it will create a circle with a radius that is half the height and width of ```.element```. The ```circle()``` function can also use the same syntax for positioning the shape within.

# url()

```css
.element {
  shape-outside: url('circle.png');
}
```
In this instance, we have two floated images, one on either side of a block of text. Since both images have the ```shape-outside``` property set then the text beneath will avoid those two floats.

<div class="cp_embed_wrapper resizable" style="height: 268px;">
<iframe id="cp_embed_fbe5379f499f072e55fa1e4fbab5c8d5" src="//codepen.io/css-tricks/embed/fbe5379f499f072e55fa1e4fbab5c8d5?height=268&amp;theme-id=1&amp;slug-hash=fbe5379f499f072e55fa1e4fbab5c8d5&amp;default-tab=result&amp;user=css-tricks" scrolling="no" frameborder="0" height="268" allowtransparency="true" allowfullscreen="true" allowpaymentrequest="true" name="CodePen Embed" title="CodePen Embed 3" class="cp_embed_iframe " style="width: 100%; overflow: hidden; height: 100%;"></iframe>
</div>

It’s also possible to set the ```shape-image-threshold``` property which will inform the browser which pixels, depending on their transparency, should create the shape. For example:

```css
.element {
  shape-outside: url('image.png');
  shape-image-threshold: 0.5;
}
```

In this example the only pixels that will create the shape must have 50% transparency and above. Values from ```0.0``` (transparent) to ```1.0``` (opaque) are valid.

# polygon()

```css
.element {
  shape-outside: polygon(0 0, 0 200px, 300px 600px);
}
```
This function creates any shape that has three or more vertices, for example:

<div class="cp_embed_wrapper resizable" style="height: 268px;">
<iframe id="cp_embed_4e5420d8c1a2766b25dd3c98f684bf9c" src="//codepen.io/css-tricks/embed/4e5420d8c1a2766b25dd3c98f684bf9c?height=268&amp;theme-id=1&amp;slug-hash=4e5420d8c1a2766b25dd3c98f684bf9c&amp;default-tab=result&amp;user=css-tricks" scrolling="no" frameborder="0" height="268" allowtransparency="true" allowfullscreen="true" allowpaymentrequest="true" name="CodePen Embed" title="CodePen Embed 4" class="cp_embed_iframe " style="width: 100%; overflow: hidden; height: 100%;"></iframe>
</div>

It’s important to note that if this property is going to be animated it requires the same number of vertices when you declare the animated state:

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
```inset()``` is a function for making rectangular shapes, it takes five parameters but the fifth, for ```border-radius``` is optional. The other arguments are offsets inwards from edge of ```.element```:

<div class="cp_embed_wrapper resizable" style="height: 268px;">
<iframe id="cp_embed_b2da5018d8f20ac3a2ccc26edb724db6" src="//codepen.io/css-tricks/embed/b2da5018d8f20ac3a2ccc26edb724db6?height=268&amp;theme-id=1&amp;slug-hash=b2da5018d8f20ac3a2ccc26edb724db6&amp;default-tab=result&amp;user=css-tricks" scrolling="no" frameborder="0" height="268" allowtransparency="true" allowfullscreen="true" allowpaymentrequest="true" name="CodePen Embed" title="CodePen Embed 1" class="cp_embed_iframe " style="width: 100%; overflow: hidden; height: 100%;"></iframe>
</div>

Above we have an element that is 200px wide by 200px tall and we’re offsetting the shape within to 50px in every direction except the left side. This way the text will wrap above the shape even though the div extends to the top.

# Related properties
<ul>
	<li>[clip-path]()</li>
</ul>

# Other resoutces
<ul>
	<li>[CSS Shapes on W3C]()</li>
	<li>[shape-outside on MDN]()</li>
	<li>[Getting started with CSS Shapes]()</li>
	<li>[CSS Shapes on A List Apart]()</li>
</ul>

# Browser support
This browser support data is from [Caniuse](http://caniuse.com/#feat=css-shapes), which has more detail. A number indicates that browser supports the feature at that version and up.

<div class="caniuse"><div class="caniuse-header"><h4 id="article-header-id-9" class="has-header-link"><a class="article-headline-link" href="#article-header-id-9">#</a>Desktop</h4><table class="browser-support-table"><thead><tr><th class="chrome"><span>Chrome</span></th><th class="opera"><span>Opera</span></th><th class="firefox"><span>Firefox</span></th><th class="ie"><span>IE</span></th><th class="edge"><span>Edge</span></th><th class="safari"><span>Safari</span></th></tr></thead><tbody><tr><td class="y yep" title="Chrome - " data-browser-name="Chrome"><span class="caniuse-agents-version version">37</span></td><td class="y yep" title="Opera - " data-browser-name="Opera"><span class="caniuse-agents-version version">24</span></td><td class="n nope" title="Firefox - " data-browser-name="Firefox"><span class="caniuse-agents-version version">No</span></td><td class="n nope" title="IE - " data-browser-name="IE"><span class="caniuse-agents-version version">No</span></td><td class="n nope" title="Edge - " data-browser-name="Edge"><span class="caniuse-agents-version version">No</span></td><td class="y yep" title="Safari - " data-browser-name="Safari"><span class="caniuse-agents-version version">7.1*</span></td></tr></tbody></table></div><div class="caniuse-section"><h4 id="article-header-id-10" class="has-header-link"><a class="article-headline-link" href="#article-header-id-10">#</a>Mobile / Tablet</h4><table class="browser-support-table"><thead><tr><th class="ios_saf"><span>iOS Safari</span></th><th class="op_mob"><span>Opera Mobile</span></th><th class="op_mini"><span>Opera Mini</span></th><th class="android"><span>Android</span></th><th class="and_chr"><span>Android Chrome</span></th><th class="and_ff"><span>Android Firefox</span></th></tr></thead><tbody><tr><td class="y yep" title="iOS Safari - " data-browser-name="iOS Safari"><span class="caniuse-agents-version version">8*</span></td><td class="y yep" title="Opera Mobile - " data-browser-name="Opera Mobile"><span class="caniuse-agents-version version">37</span></td><td class="n nope" title="Opera Mini - " data-browser-name="Opera Mini"><span class="caniuse-agents-version version">No</span></td><td class="y yep" title="Android - " data-browser-name="Android"><span class="caniuse-agents-version version">62</span></td><td class="y yep" title="Android Chrome - " data-browser-name="Android Chrome"><span class="caniuse-agents-version version">64</span></td><td class="n nope" title="Android Firefox - " data-browser-name="Android Firefox"><span class="caniuse-agents-version version">No</span></td></tr></tbody></table></div></div>












