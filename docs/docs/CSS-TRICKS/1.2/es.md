<article id="post-203844"> 
   <h1 class="screen-reader">shape-outside</h1> 
   <header class="mega-header breadcrumbs-header breadcrumbs-last-updated"> 
    <span><span xmlns:v="http://rdf.data-vocabulary.org/#"><span typeof="v:Breadcrumb"><a href="https://css-tricks.com/" rel="v:url" property="v:title">Home</a> &raquo; <span rel="v:child" typeof="v:Breadcrumb"><a href="https://css-tricks.com/almanac/" rel="v:url" property="v:title">CSS Almanac</a> &raquo; <span rel="v:child" typeof="v:Breadcrumb"><a href="https://css-tricks.com/almanac/properties/" rel="v:url" property="v:title">Properties</a> &raquo; <span rel="v:child" typeof="v:Breadcrumb"><a href="https://css-tricks.com/almanac/properties/s/" rel="v:url" property="v:title">S</a> &raquo; <span class="breadcrumb_last">shape-outside</span></span></span></span></span></span></span> 
   </header> 
   <p class="author-byline"> By <a href="https://css-tricks.com/author/robinrendle/"> <span class="p-author"> Robin Rendle </span> </a> Last Updated On <time datetime="2015-06-17" class="dt-published"> August 19, 2017 </time> <span class="byline-tags"> 
     <svg class="icon-tag" width="12px" height="12px">
      <use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#icon-tag"></use>
     </svg><a href="https://css-tricks.com/tag/basic-shapes/" rel="tag">basic shapes</a>, <a href="https://css-tricks.com/tag/shape-outside/" rel="tag">shape-outside</a> </span> </p> 
   <div class="article-content"> 
    <p>The <code>shape-outside</code> property controls how content will wrap around a floated element’s bounding-box. Typically this is so that text can reflow over a shape such as a circle, ellipse or a polygon:</p> 
    <pre rel="CSS" class=" language-css"><code class=" language-css"><span class="token selector"><span class="token class">.element</span> </span><span class="token punctuation">{</span>  
  <span class="token property">float</span><span class="token punctuation">:</span> left<span class="token punctuation">;</span>
  <span class="token property">shape-outside</span><span class="token punctuation">:</span> <span class="token function">circle</span><span class="token punctuation">(</span><span class="token number">50%</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
  <span class="token property">width</span><span class="token punctuation">:</span> <span class="token number">200</span>px<span class="token punctuation">;</span>
  <span class="token property">height</span><span class="token punctuation">:</span> <span class="token number">200</span>px<span class="token punctuation">;</span>
<span class="token punctuation">}</span></code></pre> 
    <figure id="post-203845" class="align-none media-203845">
     <img sizes="(min-width: 1850px) calc( (100vw - 555px) / 3 )
       (min-width: 1251px) calc( (100vw - 530px) / 2 )
       (min-width: 1086px) calc(100vw - 480px)
       (min-width: 626px)  calc(100vw - 335px)
                           calc(100vw - 30px)" srcset="https://cdn.css-tricks.com/wp-content/uploads/2015/06/shape-outside.png 1550w, https://cdn.css-tricks.com/wp-content/uploads/2015/06/shape-outside-300x135.png 300w, https://cdn.css-tricks.com/wp-content/uploads/2015/06/shape-outside-1024x460.png 1024w" src="//cdn.css-tricks.com/wp-content/uploads/2015/06/shape-outside.png" alt="" />
    </figure> 
    <p>It’s important to note that this property will only work on floated elements for now, although this is likely to change in the future. The <code>shape-outside</code> property can also be manipulated with <a href="http://codepen.io/robinrendle/pen/4275e31f9e95882054d400741b010dc6?editors=110">transitions or animations</a>.</p> 
    <h3 id="article-header-id-0" class="has-header-link"><a class="article-headline-link" href="#article-header-id-0">#</a>Values</h3> 
    <ul> 
     <li><code>circle()</code>: for making circular shapes.</li> 
     <li><code>ellipse()</code>: for making elliptical shapes.</li> 
     <li><code>inset()</code>: for making rectangular shapes.</li> 
     <li><code>polygon()</code>: for creating any shape with 3 or more vertices.</li> 
     <li><code>url()</code>: identifies which image should be used to wrap text around.</li> 
     <li><code>initial</code>: the float area is unaffected.</li> 
     <li><code>inherit</code>: inherits <code>shape-outside</code> value from parent.</li> 
    </ul> 
    <p>The following values identify which reference of <a href="https://css-tricks.com/the-css-box-model">the box model</a> should be used for positioning the shape within:</p> 
    <ul> 
     <li><code>margin-box</code></li> 
     <li><code>padding-box</code></li> 
     <li><code>border-box</code></li> 
    </ul> 
    <p>These values should be appended to the end, for instance: <code>shape-outside: circle(50% at 0 0) padding-box</code>. By default the <code>margin-box</code> reference will be used.</p> 
    <h3 id="article-header-id-1" class="has-header-link"><a class="article-headline-link" href="#article-header-id-1">#</a>ellipse()</h3> 
    <pre rel="CSS" class=" language-css"><code class=" language-css"><span class="token selector"><span class="token class">.element</span> </span><span class="token punctuation">{</span>
  <span class="token property">shape-outside</span><span class="token punctuation">:</span> <span class="token function">ellipse</span><span class="token punctuation">(</span><span class="token number">150</span>px <span class="token number">300</span>px at <span class="token number">50%</span> <span class="token number">50%</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span></code></pre> 
    <p>The <code>ellipse()</code> function requires the radii values for the x, y axis of the ellipse followed by the coordinates to position the center of the shape within its bounding box. For instance the example above will position the center of the ellipse in the vertical and horizontal center of the <code>.element</code> div:</p> 
    <div class="cp_embed_wrapper resizable" style="height: 268px;">
     <iframe id="cp_embed_7fa99015d63597648d5e312c5b73ac25" src="//codepen.io/css-tricks/embed/7fa99015d63597648d5e312c5b73ac25?height=268&amp;theme-id=1&amp;slug-hash=7fa99015d63597648d5e312c5b73ac25&amp;default-tab=result&amp;user=css-tricks" scrolling="no" frameborder="0" height="268" allowtransparency="true" allowfullscreen="true" allowpaymentrequest="true" name="CodePen Embed" title="CodePen Embed 6" class="cp_embed_iframe " style="width: 100%; overflow: hidden; height: 100%;"></iframe>
     <div class="win-size-grip" style="touch-action: none;"></div>
    </div> 
    <p>Although the demo above may suggest that we’re changing the shape of the <code>div</code> itself, if we add borders and a background-image we’ll find that the bounding box is in fact still rectangular:</p> 
    <div class="cp_embed_wrapper resizable" style="height: 268px;">
     <iframe id="cp_embed_5e47a80626dfa27a42dd18a0e2b8450b" src="//codepen.io/css-tricks/embed/5e47a80626dfa27a42dd18a0e2b8450b?height=268&amp;theme-id=1&amp;slug-hash=5e47a80626dfa27a42dd18a0e2b8450b&amp;default-tab=result&amp;user=css-tricks" scrolling="no" frameborder="0" height="268" allowtransparency="true" allowfullscreen="true" allowpaymentrequest="true" name="CodePen Embed" title="CodePen Embed 5" class="cp_embed_iframe " style="width: 100%; overflow: hidden; height: 100%;"></iframe>
     <div class="win-size-grip" style="touch-action: none;"></div>
    </div> 
    <p>It might be better to think of it this way: with the <code>shape-outside</code> property we’re changing the relationship of other elements around an element, not the geometry of the element itself. To fix that we’ll need to use <code>shape-outside</code> alongside the <code>clip-path()</code> property, such as in this example:</p> 
    <div class="cp_embed_wrapper resizable" style="height: 268px;">
     <iframe id="cp_embed_4e5420d8c1a2766b25dd3c98f684bf9c" src="//codepen.io/css-tricks/embed/4e5420d8c1a2766b25dd3c98f684bf9c?height=268&amp;theme-id=1&amp;slug-hash=4e5420d8c1a2766b25dd3c98f684bf9c&amp;default-tab=result&amp;user=css-tricks" scrolling="no" frameborder="0" height="268" allowtransparency="true" allowfullscreen="true" allowpaymentrequest="true" name="CodePen Embed" title="CodePen Embed 4" class="cp_embed_iframe " style="width: 100%; overflow: hidden; height: 100%;"></iframe>
     <div class="win-size-grip" style="touch-action: none;"></div>
    </div> 
    <h3 id="article-header-id-2" class="has-header-link"><a class="article-headline-link" href="#article-header-id-2">#</a>circle()</h3> 
    <pre rel="CSS" class=" language-css"><code class=" language-css"><span class="token selector"><span class="token class">.element</span> </span><span class="token punctuation">{</span>
  <span class="token property">shape-outside</span><span class="token punctuation">:</span> <span class="token function">circle</span><span class="token punctuation">(</span><span class="token number">50%</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span></code></pre> 
    <p>This function creates a circle, and in the code example above it will create a circle with a radius that is half the height and width of <code>.element</code>. The <code>circle()</code> function can also use the same syntax for positioning the shape within.</p> 
    <h3 id="article-header-id-3" class="has-header-link"><a class="article-headline-link" href="#article-header-id-3">#</a>url()</h3> 
    <pre rel="CSS" class=" language-css"><code class=" language-css"><span class="token selector"><span class="token class">.element</span> </span><span class="token punctuation">{</span>
  <span class="token property">shape-outside</span><span class="token punctuation">:</span> <span class="token url">url('circle.png')</span><span class="token punctuation">;</span> 
<span class="token punctuation">}</span></code></pre> 
    <p>In this instance, we have two floated images, one on either side of a block of text. Since both images have the <code>shape-outside</code> property set then the text beneath will avoid those two floats.</p> 
    <div class="cp_embed_wrapper resizable" style="height: 268px;">
     <iframe id="cp_embed_fbe5379f499f072e55fa1e4fbab5c8d5" src="//codepen.io/css-tricks/embed/fbe5379f499f072e55fa1e4fbab5c8d5?height=268&amp;theme-id=1&amp;slug-hash=fbe5379f499f072e55fa1e4fbab5c8d5&amp;default-tab=result&amp;user=css-tricks" scrolling="no" frameborder="0" height="268" allowtransparency="true" allowfullscreen="true" allowpaymentrequest="true" name="CodePen Embed" title="CodePen Embed 3" class="cp_embed_iframe " style="width: 100%; overflow: hidden; height: 100%;"></iframe>
     <div class="win-size-grip" style="touch-action: none;"></div>
    </div> 
    <p>It’s also possible to set the <code>shape-image-threshold</code> property which will inform the browser which pixels, depending on their transparency, should create the shape. For example:</p> 
    <pre rel="CSS" class=" language-css"><code class=" language-css"><span class="token selector"><span class="token class">.element</span> </span><span class="token punctuation">{</span>  
  <span class="token property">shape-outside</span><span class="token punctuation">:</span> <span class="token url">url('image.png')</span><span class="token punctuation">;</span> 
  <span class="token property">shape-image-threshold</span><span class="token punctuation">:</span> <span class="token number">0.5</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span></code></pre> 
    <p>In this example the only pixels that will create the shape must have 50% transparency and above. Values from <code>0.0</code> (transparent) to <code>1.0</code> (opaque) are valid.</p> 
    <h3 id="article-header-id-4" class="has-header-link"><a class="article-headline-link" href="#article-header-id-4">#</a>polygon()</h3> 
    <pre rel="CSS" class=" language-css"><code class=" language-css"><span class="token selector"><span class="token class">.element</span> </span><span class="token punctuation">{</span>
  <span class="token property">shape-outside</span><span class="token punctuation">:</span> <span class="token function">polygon</span><span class="token punctuation">(</span><span class="token number">0</span> <span class="token number">0</span>, <span class="token number">0</span> <span class="token number">200</span>px, <span class="token number">300</span>px <span class="token number">600</span>px<span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span></code></pre> 
    <p>This function creates any shape that has three or more vertices, for example:</p> 
    <div class="cp_embed_wrapper resizable" style="height: 268px;">
     <iframe id="cp_embed_22b25bc2fdbcf4f1adf6f3822ff28156" src="//codepen.io/css-tricks/embed/22b25bc2fdbcf4f1adf6f3822ff28156?height=268&amp;theme-id=1&amp;slug-hash=22b25bc2fdbcf4f1adf6f3822ff28156&amp;default-tab=result&amp;user=css-tricks" scrolling="no" frameborder="0" height="268" allowtransparency="true" allowfullscreen="true" allowpaymentrequest="true" name="CodePen Embed" title="CodePen Embed 2" class="cp_embed_iframe " style="width: 100%; overflow: hidden; height: 100%;"></iframe>
     <div class="win-size-grip" style="touch-action: none;"></div>
    </div> 
    <p>It’s important to note that if this property is going to be animated it requires the same number of vertices when you declare the animated state: </p> 
    <pre rel="CSS" class=" language-css"><code class=" language-css"><span class="token selector"><span class="token class">.element</span> </span><span class="token punctuation">{</span>  
  <span class="token property">shape-outside</span><span class="token punctuation">:</span> <span class="token function">polygon</span><span class="token punctuation">(</span><span class="token number">0</span> <span class="token number">0</span>, <span class="token number">100%</span> <span class="token number">0</span>, <span class="token number">100%</span> <span class="token number">100%</span>, <span class="token number">0</span> <span class="token number">100%</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
  <span class="token property">transition</span><span class="token punctuation">:</span> shape-outside <span class="token number">1</span>s<span class="token punctuation">;</span>
<span class="token punctuation">}</span>
<span class="token selector"><span class="token class">.element</span><span class="token pseudo-class">:hover</span> </span><span class="token punctuation">{</span>  
    <span class="token property">shape-outside</span><span class="token punctuation">:</span> <span class="token function">polygon</span><span class="token punctuation">(</span><span class="token number">0</span> <span class="token number">0</span>, <span class="token number">100%</span> <span class="token number">50%</span>, <span class="token number">100%</span> <span class="token number">50%</span>, <span class="token number">0</span> <span class="token number">100%</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span></code></pre> 
    <h3 id="article-header-id-5" class="has-header-link"><a class="article-headline-link" href="#article-header-id-5">#</a>inset()</h3> 
    <pre rel="CSS" class=" language-css"><code class=" language-css"><span class="token selector"><span class="token class">.element</span> </span><span class="token punctuation">{</span>
  <span class="token property">shape-outside</span><span class="token punctuation">:</span> <span class="token function">inset</span><span class="token punctuation">(</span><span class="token number">100</span>px <span class="token number">100</span>px <span class="token number">100</span>px <span class="token number">100</span>px <span class="token number">10</span>px<span class="token punctuation">)</span><span class="token punctuation">;</span>
  <span class="token comment" spellcheck="true">/* shape-outside: inset(top right bottom left border-radius); */</span>
<span class="token punctuation">}</span></code></pre> 
    <p><code>inset()</code> is a function for making rectangular shapes, it takes five parameters but the fifth, for <code>border-radius</code> is optional. The other arguments are offsets inwards from edge of <code>.element</code>:</p> 
    <div class="cp_embed_wrapper resizable" style="height: 268px;">
     <iframe id="cp_embed_b2da5018d8f20ac3a2ccc26edb724db6" src="//codepen.io/css-tricks/embed/b2da5018d8f20ac3a2ccc26edb724db6?height=268&amp;theme-id=1&amp;slug-hash=b2da5018d8f20ac3a2ccc26edb724db6&amp;default-tab=result&amp;user=css-tricks" scrolling="no" frameborder="0" height="268" allowtransparency="true" allowfullscreen="true" allowpaymentrequest="true" name="CodePen Embed" title="CodePen Embed 1" class="cp_embed_iframe " style="width: 100%; overflow: hidden; height: 100%;"></iframe>
     <div class="win-size-grip" style="touch-action: none;"></div>
    </div> 
    <p>Above we have an element that is 200px wide by 200px tall and we’re offsetting the shape within to 50px in every direction except the left side. This way the text will wrap above the shape even though the div extends to the top.</p> 
    <h3 id="article-header-id-6" class="has-header-link"><a class="article-headline-link" href="#article-header-id-6">#</a>Related properties</h3> 
    <ul> 
     <li><a href="https://css-tricks.com/almanac/properties/c/clip/">clip-path</a></li> 
    </ul> 
    <h3 id="article-header-id-7" class="has-header-link"><a class="article-headline-link" href="#article-header-id-7">#</a>Other resources</h3> 
    <ul> 
     <li><a href="http://www.w3.org/TR/css-shapes/#funcdef-ellipse">CSS Shapes on W3C</a></li> 
     <li><a href="https://developer.mozilla.org/en-US/docs/Web/CSS/shape-outside">shape-outside on MDN</a></li> 
     <li><a href="http://www.html5rocks.com/en/tutorials/shapes/getting-started">Getting started with CSS Shapes</a></li> 
     <li><a href="http://alistapart.com/article/css-shapes-101">CSS Shapes on A List Apart</a></li> 
    </ul> 
    <h3 id="browser-support" class="has-header-link"><a class="article-headline-link" href="#browser-support">#</a>Browser support</h3> 
    <div class="caniuse">
     <div class="caniuse-header">
      <p>This browser support data is from <a href="http://caniuse.com/#feat=css-shapes">Caniuse</a>, which has more detail. A number indicates that browser supports the feature at that version and up.</p>
     </div>
     <div class="caniuse-section">
      <h4 id="article-header-id-9" class="has-header-link"><a class="article-headline-link" href="#article-header-id-9">#</a>Desktop</h4>
      <table class="browser-support-table">
       <thead>
        <tr>
         <th class="chrome"><span>Chrome</span></th>
         <th class="opera"><span>Opera</span></th>
         <th class="firefox"><span>Firefox</span></th>
         <th class="ie"><span>IE</span></th>
         <th class="edge"><span>Edge</span></th>
         <th class="safari"><span>Safari</span></th>
        </tr>
       </thead>
       <tbody>
        <tr>
         <td class="y yep" title="Chrome - " data-browser-name="Chrome"><span class="caniuse-agents-version version">37</span></td>
         <td class="y yep" title="Opera - " data-browser-name="Opera"><span class="caniuse-agents-version version">24</span></td>
         <td class="n nope" title="Firefox - " data-browser-name="Firefox"><span class="caniuse-agents-version version">No</span></td>
         <td class="n nope" title="IE - " data-browser-name="IE"><span class="caniuse-agents-version version">No</span></td>
         <td class="n nope" title="Edge - " data-browser-name="Edge"><span class="caniuse-agents-version version">No</span></td>
         <td class="y yep" title="Safari - " data-browser-name="Safari"><span class="caniuse-agents-version version">7.1*</span></td>
        </tr>
       </tbody>
      </table>
     </div>
     <div class="caniuse-section">
      <h4 id="article-header-id-10" class="has-header-link"><a class="article-headline-link" href="#article-header-id-10">#</a>Mobile / Tablet</h4>
      <table class="browser-support-table">
       <thead>
        <tr>
         <th class="ios_saf"><span>iOS Safari</span></th>
         <th class="op_mob"><span>Opera Mobile</span></th>
         <th class="op_mini"><span>Opera Mini</span></th>
         <th class="android"><span>Android</span></th>
         <th class="and_chr"><span>Android Chrome</span></th>
         <th class="and_ff"><span>Android Firefox</span></th>
        </tr>
       </thead>
       <tbody>
        <tr>
         <td class="y yep" title="iOS Safari - " data-browser-name="iOS Safari"><span class="caniuse-agents-version version">8*</span></td>
         <td class="y yep" title="Opera Mobile - " data-browser-name="Opera Mobile"><span class="caniuse-agents-version version">37</span></td>
         <td class="n nope" title="Opera Mini - " data-browser-name="Opera Mini"><span class="caniuse-agents-version version">No</span></td>
         <td class="y yep" title="Android - " data-browser-name="Android"><span class="caniuse-agents-version version">62</span></td>
         <td class="y yep" title="Android Chrome - " data-browser-name="Android Chrome"><span class="caniuse-agents-version version">64</span></td>
         <td class="n nope" title="Android Firefox - " data-browser-name="Android Firefox"><span class="caniuse-agents-version version">No</span></td>
        </tr>
       </tbody>
      </table>
     </div>
    </div> 
   </div> 
  </article>