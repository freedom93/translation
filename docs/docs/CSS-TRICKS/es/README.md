<article id="post-268736" role="main" class="instapaper_body h-entry e-content">
    <div data-element="head" er="" class="mega-header">
        <h1 class="p-name" id="
----------------iron-mans-arc-reactor-using-css3-transforms-and&nbsp;animations--------------">
Iron Man’s Arc Reactor Using CSS3 Transforms and&nbsp;Animations              </h1>
        <p class="author-byline">
            <span class="author-and-date">
By
<a href="https://css-tricks.com/author/kunalsarkar/" target="_blank">
<span class="p-author">
Kunal Sarkar          </span>
            </a>
            <span class="slashes">On</span>
            <time datetime="2018-04-02" class="dt-published">
                April 2, 2018 </time>
            </span>
            <span class="byline-tags">
<svg class="icon-tag" width="12px" height="12px"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#icon-tag"></use></svg><a href="https://css-tricks.com/tag/animation/" rel="tag" target="_blank">animation</a>, <a href="https://css-tricks.com/tag/transforms/" rel="tag" target="_blank">transforms</a>        </span>
        </p>
        <div class="article-content">
            <p>Alright Iron Man fans, fire up your code editors! We are going to make the Arc reactor from Iron Man’s suit in CSS. Here’s what the end result will look like:</p>
            <div class="cp_embed_wrapper resizable" style="height: 400px;">
                <iframe id="cp_embed_QmLEWN" src="//codepen.io/supersarkar/embed/QmLEWN?height=400&amp;theme-id=1&amp;slug-hash=QmLEWN&amp;default-tab=result&amp;user=supersarkar&amp;embed-version=2&amp;pen-title=Iron%20Man's%20Arc%20Reactor" scrolling="no" frameborder="0" height="400" allowtransparency="true" allowfullscreen="true" name="CodePen Embed" title="Iron Man's Arc Reactor" class="cp_embed_iframe " style="width: 100%; overflow: hidden; height: 100%;"></iframe>
                <div class="win-size-grip" style="touch-action: none;"></div>
                <div class="win-size-grip" style="touch-action: none;"></div>
            </div>
            <p><span id="more-268736"></span></p>
            <h3 id="article-header-id-0" class="has-header-link"><a class="article-headline-link" href="#article-header-id-0">#</a>The Full Page Wrapper</h3>
            <p>We will make our Arc reactor on a dark full-page background. Here’s our code to make a full page wrapper element:</p>
            <pre rel="CSS" class=" language-css"><code class="language-css"><span class="hljs-selector-tag">body</span> {
<span class="hljs-attribute">margin</span>: <span class="hljs-number">0</span>;
}

<span class="hljs-selector-class">.fullpage-wrapper</span> {
<span class="hljs-attribute">height</span>: <span class="hljs-number">100vh</span>;
<span class="hljs-attribute">background</span>: <span class="hljs-built_in">radial-gradient</span>(#353c44, #222931);
}</code></pre>
            <p>Why do we declare no margin on the body? The <code>&lt;body&gt;</code> element has some margin set to it by default in the user agent stylesheet. This prevents the elements inside the <code>&lt;body&gt;</code> to touch the edges of the screen. Since we want our wrapper to cover the entire screen, edge to edge, we removed that default margin on <code>&lt;body&gt;</code> element by setting it to <code>0</code>.</p>
            <p>We’ve given our <code>.fullpage-wrapper</code> the full height of the viewport. We don’t have to specify a width because a div is full width by default. We could have gone with another approach by setting both the width and height of the element to <code>100%</code> but that comes with some possible drawbacks as more elements are added to the screen. Using viewport units ensures our wrapper always occupies the full vertical space of the screen, regardless of what it is or what other elements are added to the layout.</p>
            <p>We also used a radial gradient on our wrapper using <a href="https://css-tricks.com/snippets/css/css-radial-gradient/" target="_blank"><code>radial-gradient()</code></a> CSS function. The parameters inside the function are the color start and end points. So, the center of the background will be more <code>#353c44</code> and more <code>#222931</code> towards the edges. It’s subtle, but a nice touch.</p>
            <figure id="post-268738" class="align-none media-268738"><img src="https://cdn.css-tricks.com/wp-content/uploads/2018/03/ironman-1.jpg" srcset="https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_714,f_auto,q_auto/v1521762064/ironman-1_o38vzq.jpg 714w, https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_200,f_auto,q_auto/v1521762064/ironman-1_o38vzq.jpg 200w" sizes="(min-width: 1850px) calc( (100vw - 555px) / 3 )
(min-width: 1251px) calc( (100vw - 530px) / 2 )
(min-width: 1086px) calc(100vw - 480px)
(min-width: 626px)  calc(100vw - 335px)
calc(100vw - 30px)" alt=""></figure>
            <h3 id="article-header-id-1" class="has-header-link"><a class="article-headline-link" href="#article-header-id-1">#</a>Centering the Reactor Container</h3>
            <p>Before we start creating our reactor, let’s create a container for it and center it:</p>
            <pre rel="CSS" class=" language-css"><code class="language-css"><span class="hljs-selector-class">.reactor-container</span> {
<span class="hljs-attribute">width</span>: <span class="hljs-number">300px</span>;
<span class="hljs-attribute">height</span>: <span class="hljs-number">300px</span>;
<span class="hljs-attribute">margin</span>: auto;
<span class="hljs-attribute">border</span>: <span class="hljs-number">1px</span> dashed <span class="hljs-number">#888</span>;
}</code></pre>
            <p>This gives us a <code>300px</code> x <code>300px</code> box with dashed border. The <code>margin: auto;</code> declaration ensures equal horizontal spacing.</p>
            <figure id="post-268739" class="align-none media-268739"><img src="https://cdn.css-tricks.com/wp-content/uploads/2018/03/ironman-2.jpg" srcset="https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_947,f_auto,q_auto/v1521762066/ironman-2_c7jsda.jpg 947w, https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_200,f_auto,q_auto/v1521762066/ironman-2_c7jsda.jpg 200w" sizes="(min-width: 1850px) calc( (100vw - 555px) / 3 )
(min-width: 1251px) calc( (100vw - 530px) / 2 )
(min-width: 1086px) calc(100vw - 480px)
(min-width: 626px)  calc(100vw - 335px)
calc(100vw - 30px)" alt=""></figure>
            <p>But why it doesn’t center it vertically?</p>
            <p>Per CSS2 specs, if we give auto margin to the left and right side, then the entire available space will be equally divided to left and right margin. This isn’t the same case for the top and bottom margin though. For top and bottom margin the <a href="https://www.w3.org/TR/CSS22/visudet.html#Computing_heights_and_margins" target="_blank">CSS2 spec</a> says:</p>
            <blockquote>
                <p>If <code>margin-top</code>, or <code>margin-bottom</code> are <code>auto</code>, their used value is <code>0</code>.</p>
            </blockquote>
            <p>However, we do have a good news. The flexbox layout follows new rules of alignment, and here’s what the <a href="https://www.w3.org/TR/css-flexbox-1/#auto-margins" target="_blank">Flexbox spec</a> has to say:</p>
            <blockquote>
                <p>Prior to alignment via justify-content and align-self, any positive free space is distributed to auto margins in that dimension.</p>
            </blockquote>
            <p>This means if the element in consideration is displayed as a flex item, then <code>margin: auto;</code> will work in both the directions. Let’s make our wrapper a flex container and its child elements flex items:</p>
            <pre rel="CSS" class=" language-css"><code class="language-css"><span class="hljs-selector-class">.fullpage-wrapper</span> {
<span class="hljs-attribute">width</span>: <span class="hljs-number">100%</span>;
<span class="hljs-attribute">height</span>: <span class="hljs-number">100vh</span>;
<span class="hljs-attribute">background</span>: <span class="hljs-built_in">radial-gradient</span>(#353c44, #222931);
<span class="hljs-attribute">display</span>: flex;
}</code></pre>
            <p>There, that’s much better:</p>
            <figure id="post-268740" class="align-none media-268740"><img src="https://cdn.css-tricks.com/wp-content/uploads/2018/03/ironman-3.jpg" srcset="https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_947,f_auto,q_auto/v1521762067/ironman-3_njqv2m.jpg 947w, https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_200,f_auto,q_auto/v1521762067/ironman-3_njqv2m.jpg 200w" sizes="(min-width: 1850px) calc( (100vw - 555px) / 3 )
(min-width: 1251px) calc( (100vw - 530px) / 2 )
(min-width: 1086px) calc(100vw - 480px)
(min-width: 626px)  calc(100vw - 335px)
calc(100vw - 30px)" alt=""></figure>
            <p>There are many other methods to center elements in HTML. There’s a <a href="https://css-tricks.com/centering-css-complete-guide/" target="_blank">detailed guide on centering</a> right here on CSS-Tricks to learn more.</p>
            <h3 id="article-header-id-2" class="has-header-link"><a class="article-headline-link" href="#article-header-id-2">#</a>The Reactor Core: Concentric Circles in CSS</h3>
            <p>We know that new elements in HTML are created from left to right (for left-to-right languages), or top to bottom. Elements never overlap, until you provide some negative margin.</p>
            <p>So, how are we going to display concentric circles? We will use absolute positioning. </p>
            <p>The default value of <a href="https://css-tricks.com/almanac/properties/p/position/" target="_blank"><code>position</code></a> property is <code>static</code>. Static and relative positioning follow the flow of top to bottom and left to right. However, an absolutely positioned element is not treated as a part of the document flow and can be positioned anywhere using the top, right, bottom and left properties.</p>
            <p>Let’s start by creating the smallest circle:</p>
            <pre rel="HTML" class=" language-markup"><code class="language-markup">&lt;div class="fullpage-wrapper"&gt;
&lt;div class="reactor-container"&gt;
&lt;!-- the smallest circle --&gt;
&lt;div class="core-inner"&gt;&lt;/div&gt;
&lt;/div&gt;
&lt;/div&gt;</code></pre>
            <pre rel="CSS" class=" language-css"><code class="language-css"><span class="hljs-selector-class">.core-inner</span> {
<span class="hljs-attribute">position</span>: absolute;
<span class="hljs-attribute">width</span>: <span class="hljs-number">70px</span>;
<span class="hljs-attribute">height</span>: <span class="hljs-number">70px</span>;
<span class="hljs-attribute">border-radius</span>: <span class="hljs-number">50%</span>;
<span class="hljs-attribute">border</span>: <span class="hljs-number">5px</span> solid <span class="hljs-number">#1b4e5f</span>;
<span class="hljs-attribute">background-color</span>: <span class="hljs-number">#fff</span>;
}</code></pre>
            <figure id="post-268741" class="align-none media-268741"><img src="https://cdn.css-tricks.com/wp-content/uploads/2018/03/ironman-4.jpg" srcset="https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_650,f_auto,q_auto/v1521762069/ironman-4_dpsgt6.jpg 650w, https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_200,f_auto,q_auto/v1521762069/ironman-4_dpsgt6.jpg 200w" sizes="(min-width: 1850px) calc( (100vw - 555px) / 3 )
(min-width: 1251px) calc( (100vw - 530px) / 2 )
(min-width: 1086px) calc(100vw - 480px)
(min-width: 626px)  calc(100vw - 335px)
calc(100vw - 30px)" alt=""></figure>
            <p>We need to center this div. You might be tempted to apply the same flexbox concept we used on the reactor element to center this circle as well. But, here’s what <a href="https://www.w3.org/TR/CSS22/visudet.html#abs-non-replaced-height" target="_blank">CSS2 spec</a> has to say about setting <code>margin: auto;</code> on <em>absolutely positioned</em> elements:</p>
            <blockquote>
                <p>If none of the three (<code>top</code>, <code>height</code>, and <code>bottom</code>) are <code>auto</code>: If both <code>margin-top</code> and <code>margin-bottom</code> are <code>auto</code>, solve the equation under the extra constraint that the two margins get equal values.</p>
            </blockquote>
            <p>This means if an absolutely positioned element has any value for <code>top</code>, <code>height</code> and <code>bottom</code> other than <code>auto</code>, then setting the top and bottom margin to <code>auto</code> will center the element vertically.</p>
            <p>Same case for horizontal centering: if an absolutely positioned element has any value for <code>left</code>, <code>width</code> and <code>right</code> other than <code>auto</code>, then setting the left and right margin to <code>auto</code> will center the element horizontally.</p>
            <p>That means we don’t need flexbox layout to center an absolutely positioned element with a known height and width. We just have to make sure that we give some value to <code>top</code>, <code>right</code>, <code>bottom</code> and <code>left</code> other than <code>auto</code>. So, we will use <code>0</code>:</p>
            <pre rel="CSS" class=" language-css"><code class="language-css"><span class="hljs-selector-class">.core-inner</span> {
<span class="hljs-attribute">position</span>: absolute;
<span class="hljs-attribute">width</span>: <span class="hljs-number">70px</span>;
<span class="hljs-attribute">height</span>: <span class="hljs-number">70px</span>;
<span class="hljs-attribute">top</span>: <span class="hljs-number">0</span>;
<span class="hljs-attribute">right</span>: <span class="hljs-number">0</span>;
<span class="hljs-attribute">bottom</span>: <span class="hljs-number">0</span>;
<span class="hljs-attribute">left</span>: <span class="hljs-number">0</span>;
<span class="hljs-attribute">margin</span>: auto;
<span class="hljs-attribute">border-radius</span>: <span class="hljs-number">50%</span>;
<span class="hljs-attribute">border</span>: <span class="hljs-number">5px</span> solid <span class="hljs-number">#1b4e5f</span>;
<span class="hljs-attribute">background-color</span>: <span class="hljs-number">#fff</span>;
}</code></pre>
            <p>We do not want to repeat these five lines for all the concentric circles we are going to have, so let’s create a separate class for this. We also don’t want to define <code>border-radius: 50%;</code> for all the divs that we want to display as circles, so we will create a class for that too:</p>
            <pre rel="CSS" class=" language-css"><code class="language-css"><span class="hljs-selector-class">.circle</span> {
<span class="hljs-attribute">border-radius</span>: <span class="hljs-number">50%</span>;
}

<span class="hljs-selector-class">.abs-center</span> {
<span class="hljs-attribute">position</span>: absolute;
<span class="hljs-attribute">top</span>: <span class="hljs-number">0</span>;
<span class="hljs-attribute">right</span>: <span class="hljs-number">0</span>;
<span class="hljs-attribute">bottom</span>: <span class="hljs-number">0</span>;
<span class="hljs-attribute">left</span>: <span class="hljs-number">0</span>;
<span class="hljs-attribute">margin</span>: auto;

}

<span class="hljs-selector-class">.core-inner</span> {
<span class="hljs-attribute">width</span>: <span class="hljs-number">70px</span>;
<span class="hljs-attribute">height</span>: <span class="hljs-number">70px</span>;
<span class="hljs-attribute">border</span>: <span class="hljs-number">5px</span> solid <span class="hljs-number">#1b4e5f</span>;
<span class="hljs-attribute">background-color</span>: <span class="hljs-number">#fff</span>;
}</code></pre>
            <p>Also, add these new classes to out <code>.core-inner</code> element:</p>
            <pre rel="HTML" class=" language-markup"><code class="language-markup">&lt;div class="fullpage-wrapper"&gt;
&lt;div class="reactor-container"&gt;
&lt;!-- the smallest circle --&gt;
&lt;div class="core-inner circle abs-center"&gt;&lt;/div&gt;
&lt;/div&gt;
&lt;/div&gt;</code></pre>
            <figure id="post-268742" class="align-none media-268742"><img src="https://cdn.css-tricks.com/wp-content/uploads/2018/03/ironman-5.jpg" srcset="https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_661,f_auto,q_auto/v1521762070/ironman-5_qfarjc.jpg 661w, https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_200,f_auto,q_auto/v1521762070/ironman-5_qfarjc.jpg 200w" sizes="(min-width: 1850px) calc( (100vw - 555px) / 3 )
(min-width: 1251px) calc( (100vw - 530px) / 2 )
(min-width: 1086px) calc(100vw - 480px)
(min-width: 626px)  calc(100vw - 335px)
calc(100vw - 30px)" alt=""></figure>
            <p>Okay, our concentric circle is centered. Let’s make it glow. </p>
            <p>But CSS doesn’t have any "glow" property.</p>
            <p>Don’t worry, we have the <a href="https://css-tricks.com/almanac/properties/b/box-shadow/" target="_blank"><code>box-shadow</code></a> property. Instead of giving the shadow a dark color, we will give it a bright color to make the shadow look like glow. Pretty clever, isn’t it? 😉 </p>
            <p>Let’s do this:</p>
            <pre rel="CSS" class=" language-css"><code class="language-css"><span class="hljs-selector-class">.core-inner</span> {
<span class="hljs-attribute">width</span>: <span class="hljs-number">70px</span>;
<span class="hljs-attribute">height</span>: <span class="hljs-number">70px</span>;
<span class="hljs-attribute">border</span>: <span class="hljs-number">5px</span> solid <span class="hljs-number">#1b4e5f</span>;
<span class="hljs-attribute">background-color</span>: <span class="hljs-number">#fff</span>;
<span class="hljs-attribute">box-shadow</span>: <span class="hljs-number">0px</span> <span class="hljs-number">0px</span> <span class="hljs-number">7px</span> <span class="hljs-number">5px</span> <span class="hljs-number">#52fefe</span>;
}</code></pre>
            <figure id="post-268743" class="align-none media-268743"><img src="https://cdn.css-tricks.com/wp-content/uploads/2018/03/ironman-6.jpg" srcset="https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_608,f_auto,q_auto/v1521762072/ironman-6_iu9spv.jpg 608w, https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_200,f_auto,q_auto/v1521762072/ironman-6_iu9spv.jpg 200w" sizes="(min-width: 1850px) calc( (100vw - 555px) / 3 )
(min-width: 1251px) calc( (100vw - 530px) / 2 )
(min-width: 1086px) calc(100vw - 480px)
(min-width: 626px)  calc(100vw - 335px)
calc(100vw - 30px)" alt=""></figure>
            <p>Let’s take a break and understand the syntax of <code>box-shadow</code> first because we will be using it a lot. Here are what those values for <code>box-shadow</code> mean in that order:</p>
            <ul>
                <li><code>x-offset</code>: how much we want to push the shadow on the right side (x-axis). Negative values will push the shadow to the left side.</li>
                <li><code>y-offset</code>: how much we want to push the shadow up or down (y-axis).</li>
                <li><code>blur-radius</code>: how blurry we want our shadow to be.</li>
                <li><code>spread-radius</code>: how much we want our shadow to spread.</li>
                <li><code>color</code>: color of the shadow.</li>
            </ul>
            <p>Play with these values a bit to see their effects in real time.</p>
            <p>In real life, shadows don’t drop only outside of an object. Shadows drop upon the objects too. Imagine a pit dug by a dog, it will have a shadow inside it, right?</p>
            <p>We can give a shadow inside an element using the <code>inset</code> keyword in the <code>box-sizing</code> property. To give an element both, outside and inside shadow, we simply separate them with a comma. Let’s do this to get an outside and inside glow to our reactor’s inner core:</p>
            <pre rel="CSS" class=" language-css"><code class="language-css"><span class="hljs-selector-class">.core-inner</span> {
<span class="hljs-attribute">width</span>: <span class="hljs-number">70px</span>;
<span class="hljs-attribute">height</span>: <span class="hljs-number">70px</span>;
<span class="hljs-attribute">border</span>: <span class="hljs-number">5px</span> solid <span class="hljs-number">#1B4e5f</span>;
<span class="hljs-attribute">background-color</span>: <span class="hljs-number">#fff</span>;
<span class="hljs-attribute">box-shadow</span>: <span class="hljs-number">0px</span> <span class="hljs-number">0px</span> <span class="hljs-number">7px</span> <span class="hljs-number">5px</span> <span class="hljs-number">#52fefe</span>, <span class="hljs-number">0px</span> <span class="hljs-number">0px</span> <span class="hljs-number">10px</span> <span class="hljs-number">10px</span> <span class="hljs-number">#52fefe</span> inset;
}</code></pre>
            <figure id="post-268744" class="align-none media-268744"><img src="https://cdn.css-tricks.com/wp-content/uploads/2018/03/ironman-7.jpg" srcset="https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_544,f_auto,q_auto/v1521762073/ironman-7_suolkp.jpg 544w, https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_200,f_auto,q_auto/v1521762073/ironman-7_suolkp.jpg 200w" sizes="(min-width: 1850px) calc( (100vw - 555px) / 3 )
(min-width: 1251px) calc( (100vw - 530px) / 2 )
(min-width: 1086px) calc(100vw - 480px)
(min-width: 626px)  calc(100vw - 335px)
calc(100vw - 30px)" alt=""></figure>
            <p>Now it’s starting to look sci-fi!</p>
            <p>Let’s create one more circle on top. We want the inner circle to display on top of the other circles, so we will add new circle divs *above* the inner-circle in code:</p>
            <pre rel="HTML" class=" language-markup"><code class="language-markup">&lt;div class="fullpage-wrapper"&gt;
&lt;div class="reactor-container"&gt;
&lt;!-- the second circle --&gt;
&lt;div class="core-outer circle abs-center"&gt;&lt;/div&gt;
&lt;!-- the smallest circle --&gt;
&lt;div class="core-inner circle abs-center"&gt;&lt;/div&gt;
&lt;/div&gt;
&lt;/div&gt;</code></pre>
            <p>The elements down in the code, are displayed above on the screen. If we put the core-outer below the core-inner in the code, then core-inner won’t be visible, because core-outer will cover it.</p>
            <p>Let’s give style to outer-code. The outer core will be a little bigger than the inner core and we will give an outer and inner glow to core-outer too:</p>
            <pre rel="CSS" class=" language-css"><code class="language-css"><span class="hljs-selector-class">.core-outer</span> {
<span class="hljs-attribute">width</span>: <span class="hljs-number">120px</span>;
<span class="hljs-attribute">height</span>: <span class="hljs-number">120px</span>;
<span class="hljs-attribute">border</span>: <span class="hljs-number">1px</span> solid <span class="hljs-number">#52fefe</span>;
<span class="hljs-attribute">background-color</span>: <span class="hljs-number">#fff</span>;
<span class="hljs-attribute">box-shadow</span>: <span class="hljs-number">0px</span> <span class="hljs-number">0px</span> <span class="hljs-number">2px</span> <span class="hljs-number">1px</span> <span class="hljs-number">#52fefe</span>, <span class="hljs-number">0px</span> <span class="hljs-number">0px</span> <span class="hljs-number">10px</span> <span class="hljs-number">5px</span> <span class="hljs-number">#52fefe</span> inset;
}</code></pre>
            <figure id="post-268745" class="align-none media-268745"><img src="https://cdn.css-tricks.com/wp-content/uploads/2018/03/ironman-8.jpg" srcset="https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_572,f_auto,q_auto/v1521762074/ironman-8_htenwe.jpg 572w, https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_200,f_auto,q_auto/v1521762074/ironman-8_htenwe.jpg 200w" sizes="(min-width: 1850px) calc( (100vw - 555px) / 3 )
(min-width: 1251px) calc( (100vw - 530px) / 2 )
(min-width: 1086px) calc(100vw - 480px)
(min-width: 626px)  calc(100vw - 335px)
calc(100vw - 30px)" alt=""></figure>
            <p>I want you to do one thing: look at the shadows (glow) and try to identify which one is of which circle. There are four shadows and two circles (until now).</p>
            <p>To finish designing the core, we will need one more circle that will wrap the inner and outer circles:</p>
            <pre rel="HTML" class=" language-markup"><code class="language-markup">&lt;div class="fullpage-wrapper"&gt;
&lt;div class="reactor-container"&gt;
&lt;!-- the third circle --&gt;
&lt;div class="core-wrapper circle abs-center"&gt;&lt;/div&gt;
&lt;!-- the second circle --&gt;
&lt;div class="core-outer circle abs-center"&gt;&lt;/div&gt;
&lt;!-- the smallest circle --&gt;
&lt;div class="core-inner circle abs-center"&gt;&lt;/div&gt;
&lt;/div&gt;
&lt;/div&gt;</code></pre>
            <p>This one will be a little bigger, and will again have same shadows, we will use a dark background for core-wrapper:</p>
            <pre rel="CSS" class=" language-css"><code class="language-css"><span class="hljs-selector-class">.core-wrapper</span> {
<span class="hljs-attribute">width</span>: <span class="hljs-number">180px</span>;
<span class="hljs-attribute">height</span>: <span class="hljs-number">180px</span>;
<span class="hljs-attribute">background-color</span>: <span class="hljs-number">#073c4b</span>;
<span class="hljs-attribute">box-shadow</span>: <span class="hljs-number">0px</span> <span class="hljs-number">0px</span> <span class="hljs-number">5px</span> <span class="hljs-number">4px</span> <span class="hljs-number">#52fefe</span>, <span class="hljs-number">0px</span> <span class="hljs-number">0px</span> <span class="hljs-number">6px</span> <span class="hljs-number">2px</span> <span class="hljs-number">#52fefe</span> inset;
}</code></pre>
            <figure id="post-268746" class="align-none media-268746"><img src="https://cdn.css-tricks.com/wp-content/uploads/2018/03/ironman-9.jpg" srcset="https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_541,f_auto,q_auto/v1521762076/ironman-9_nn86oe.jpg 541w, https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_200,f_auto,q_auto/v1521762076/ironman-9_nn86oe.jpg 200w" sizes="(min-width: 1850px) calc( (100vw - 555px) / 3 )
(min-width: 1251px) calc( (100vw - 530px) / 2 )
(min-width: 1086px) calc(100vw - 480px)
(min-width: 626px)  calc(100vw - 335px)
calc(100vw - 30px)" alt=""></figure>
            <h3 id="article-header-id-3" class="has-header-link"><a class="article-headline-link" href="#article-header-id-3">#</a>Creating Reactor Coils and Rotating with CSS3 Transforms</h3>
            <p>We have the core of the reactor, now we need a tunnel around the core. Actually, we can create an illusion of a round tunnel by drawing just one more circle little bigger than the <code>core-wrapper</code>. Let’s do it:</p>
            <pre rel="HTML" class=" language-markup"><code class="language-markup">&lt;div class="fullpage-wrapper"&gt;
&lt;div class="reactor-container"&gt;
&lt;!-- the largest circle --&gt;
&lt;div class="tunnel circle abs-center"&gt;&lt;/div&gt;
&lt;!-- the third circle --&gt;
&lt;div class="core-wrapper circle abs-center"&gt;&lt;/div&gt;
&lt;!-- the second circle --&gt;
&lt;div class="core-outer circle abs-center"&gt;&lt;/div&gt;
&lt;!-- the smallest circle --&gt;
&lt;div class="core-inner circle abs-center"&gt;&lt;/div&gt;
&lt;/div&gt;
&lt;/div&gt;</code></pre>
            <p>...a little wider and add same glow to the tunnel:</p>
            <pre rel="CSS" class=" language-css"><code class="language-css"><span class="hljs-selector-class">.tunnel</span> {
<span class="hljs-attribute">width</span>: <span class="hljs-number">220px</span>;
<span class="hljs-attribute">height</span>: <span class="hljs-number">220px</span>;
<span class="hljs-attribute">background-color</span>: <span class="hljs-number">#fff</span>;
<span class="hljs-attribute">box-shadow</span>: <span class="hljs-number">0px</span> <span class="hljs-number">0px</span> <span class="hljs-number">5px</span> <span class="hljs-number">1px</span> <span class="hljs-number">#52fefe</span>, <span class="hljs-number">0px</span> <span class="hljs-number">0px</span> <span class="hljs-number">5px</span> <span class="hljs-number">4px</span> <span class="hljs-number">#52fefe</span> inset;
}</code></pre>
            <figure id="post-268747" class="align-none media-268747"><img src="https://cdn.css-tricks.com/wp-content/uploads/2018/03/ironman-10.jpg" srcset="https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_586,f_auto,q_auto/v1521762077/ironman-10_cytty9.jpg 586w, https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_200,f_auto,q_auto/v1521762077/ironman-10_cytty9.jpg 200w" sizes="(min-width: 1850px) calc( (100vw - 555px) / 3 )
(min-width: 1251px) calc( (100vw - 530px) / 2 )
(min-width: 1086px) calc(100vw - 480px)
(min-width: 626px)  calc(100vw - 335px)
calc(100vw - 30px)" alt=""></figure>
            <p>Our tunnel is ready. </p>
            <p>Make sure you do not just copy paste the code. Have a look at the glows of the circles and identify which glow is of which circle, whether it is outside glow or inset glow.</p>
            <p>Now, we need eight coils on this tunnel. The coils are simple rectangles, but the major challenge is that we need the coils to run along the round path of the tunnel; not in straight line.</p>
            <p>One way to do this would be to create eight small rectangles, shift their center to the center of the reactor, and rotate each coil by an increasing angle (in multiples of <code>45deg</code>). </p>
            <p>Let’s not complicate it and make one rectangle coil at a time:</p>
            <pre rel="HTML" class=" language-markup"><code class="language-markup">&lt;div class="fullpage-wrapper"&gt;
&lt;div class="reactor-container"&gt;
&lt;div class="tunnel circle abs-center"&gt;&lt;/div&gt;
&lt;div class="core-wrapper circle abs-center"&gt;&lt;/div&gt;
&lt;div class="core-outer circle abs-center"&gt;&lt;/div&gt;
&lt;div class="core-inner circle abs-center"&gt;&lt;/div&gt;
&lt;div class="coil-1"&gt;&lt;/div&gt;
&lt;/div&gt;
&lt;/div&gt;</code></pre>
            <pre rel="CSS" class=" language-css"><code class="language-css"><span class="hljs-selector-class">.coil-1</span> {
<span class="hljs-attribute">position</span>: absolute;
<span class="hljs-attribute">width</span>: <span class="hljs-number">30px</span>;
<span class="hljs-attribute">height</span>: <span class="hljs-number">26px</span>;
<span class="hljs-attribute">background-color</span>: <span class="hljs-number">#073c4b</span>;
<span class="hljs-attribute">box-shadow</span>: <span class="hljs-number">0px</span> <span class="hljs-number">0px</span> <span class="hljs-number">5px</span> <span class="hljs-number">#52fefe</span> inset;
}</code></pre>
            <figure id="post-268748" class="align-none media-268748"><img src="https://cdn.css-tricks.com/wp-content/uploads/2018/03/ironman-11.jpg" srcset="https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_602,f_auto,q_auto/v1521762079/ironman-11_uqldm1.jpg 602w, https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_200,f_auto,q_auto/v1521762079/ironman-11_uqldm1.jpg 200w" sizes="(min-width: 1850px) calc( (100vw - 555px) / 3 )
(min-width: 1251px) calc( (100vw - 530px) / 2 )
(min-width: 1086px) calc(100vw - 480px)
(min-width: 626px)  calc(100vw - 335px)
calc(100vw - 30px)" alt=""></figure>
            <p>Now, we want to place this coil in the center at top of the tunnel. Like this:</p>
            <figure id="post-268749" class="align-none media-268749"><img src="https://cdn.css-tricks.com/wp-content/uploads/2018/03/ironman-12.jpg" srcset="https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_631,f_auto,q_auto/v1521762080/ironman-12_xjfnzm.jpg 631w, https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_389,f_auto,q_auto/v1521762080/ironman-12_xjfnzm.jpg 389w, https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_200,f_auto,q_auto/v1521762080/ironman-12_xjfnzm.jpg 200w" sizes="(min-width: 1850px) calc( (100vw - 555px) / 3 )
(min-width: 1251px) calc( (100vw - 530px) / 2 )
(min-width: 1086px) calc(100vw - 480px)
(min-width: 626px)  calc(100vw - 335px)
calc(100vw - 30px)" alt=""></figure>
            <p>Our reactor-container is <code>300px</code> x <code>300px</code>, so the center is at <code>150px</code> from top and left. The tunnel is <code>220px</code> wide, so its radius will be <code>110px</code>. This gives us the top offset of the coil: <code>150px - 110px</code>. </p>
            <p>We can keep left of the coil to <code>150px</code>, but since our coil is <code>30px</code> wide, it will shift the middle of the coil by <code>15px</code> to right, that’s why we need to subtract <code>15px</code> from <code>150px</code> to get the left offset of the coil.</p>
            <p>We can either calculate these ourselves and put the value, or we can use the CSS <code>calc()</code> function. Let’s use the CSS <code>calc()</code> function to calculate the top and left properties of the coil:</p>
            <pre rel="CSS" class=" language-css"><code class="language-css"><span class="hljs-selector-class">.coil-1</span> {
<span class="hljs-attribute">position</span>: absolute;
<span class="hljs-attribute">width</span>: <span class="hljs-number">30px</span>;
<span class="hljs-attribute">height</span>: <span class="hljs-number">20px</span>;
<span class="hljs-attribute">top</span>: <span class="hljs-built_in">calc</span>(50% - 110px);
<span class="hljs-attribute">left</span>: <span class="hljs-built_in">calc</span>(50% - 15px);
<span class="hljs-attribute">background-color</span>: <span class="hljs-number">#073c4b</span>;
<span class="hljs-attribute">box-shadow</span>: <span class="hljs-number">0px</span> <span class="hljs-number">0px</span> <span class="hljs-number">5px</span> <span class="hljs-number">#52fefe</span> inset;
}</code></pre>
            <figure id="post-268750" class="align-none media-268750"><img src="https://cdn.css-tricks.com/wp-content/uploads/2018/03/ironman-13.jpg" srcset="https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_558,f_auto,q_auto/v1521762082/ironman-13_o8lf3m.jpg 558w, https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_200,f_auto,q_auto/v1521762082/ironman-13_o8lf3m.jpg 200w" sizes="(min-width: 1850px) calc( (100vw - 555px) / 3 )
(min-width: 1251px) calc( (100vw - 530px) / 2 )
(min-width: 1086px) calc(100vw - 480px)
(min-width: 626px)  calc(100vw - 335px)
calc(100vw - 30px)" alt=""></figure>
            <p>As you can see, the <code>calc()</code> function takes a mathematical expression as its argument and solves it.</p>
            <p>Now we need eight such coils but they must lie on the tunnel. To do that, as discussed, we can simply place the eight coils at this same place, then transform their origin to the center of the reactor, and rotate each coil by an increment of 45 degrees.</p>
            <p>We need to update the coil’s origin because by default it is set to the center of the coil; we want it at center of the reactor:</p>
            <figure id="post-268751" class="align-none media-268751"><img src="https://cdn.css-tricks.com/wp-content/uploads/2018/03/ironman-14.jpg" srcset="https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_648,f_auto,q_auto/v1521762084/ironman-14_abhfxu.jpg 648w, https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_486,f_auto,q_auto/v1521762084/ironman-14_abhfxu.jpg 486w, https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_200,f_auto,q_auto/v1521762084/ironman-14_abhfxu.jpg 200w" sizes="(min-width: 1850px) calc( (100vw - 555px) / 3 )
(min-width: 1251px) calc( (100vw - 530px) / 2 )
(min-width: 1086px) calc(100vw - 480px)
(min-width: 626px)  calc(100vw - 335px)
calc(100vw - 30px)" alt=""></figure>
            <p>We will use <code>transform-origin</code> property to set the origin of the coil:</p>
            <pre rel="CSS" class=" language-css"><code class="language-css"><span class="hljs-selector-class">.coil-1</span> {
<span class="hljs-attribute">position</span>: absolute;
<span class="hljs-attribute">width</span>: <span class="hljs-number">30px</span>;
<span class="hljs-attribute">height</span>: <span class="hljs-number">20px</span>;
<span class="hljs-attribute">top</span>: <span class="hljs-built_in">calc</span>(50% - 110px);
<span class="hljs-attribute">left</span>: <span class="hljs-built_in">calc</span>(50% - 15px);
<span class="hljs-attribute">transform-origin</span>: <span class="hljs-number">15px</span> <span class="hljs-number">110px</span>;
<span class="hljs-attribute">background-color</span>: <span class="hljs-number">#073c4b</span>;
<span class="hljs-attribute">box-shadow</span>: <span class="hljs-number">0px</span> <span class="hljs-number">0px</span> <span class="hljs-number">5px</span> <span class="hljs-number">#52fefe</span> inset;
}</code></pre>
            <p>The first value, <code>15px</code>, in <code>transform-origin</code> is the <code>x-offset</code> (horizontal distance) from the top-left corner of the element, and the second value, <code>110px</code>, is the <code>y-offset</code> (vertical distance) from the top-left corner of the element.</p>
            <p>The coil’s origin is now at the center of the reactor, let’s rotate it by 45 degrees using the CSS3 transform property and see what happens:</p>
            <pre rel="CSS" class=" language-css"><code class="language-css"><span class="hljs-selector-class">.coil-1</span> {
<span class="hljs-attribute">position</span>: absolute;
<span class="hljs-attribute">width</span>: <span class="hljs-number">30px</span>;
<span class="hljs-attribute">height</span>: <span class="hljs-number">20px</span>;
<span class="hljs-attribute">top</span>: <span class="hljs-built_in">calc</span>(50% - 110px);
<span class="hljs-attribute">left</span>: <span class="hljs-built_in">calc</span>(50% - 15px);
<span class="hljs-attribute">transform-origin</span>: <span class="hljs-number">15px</span> <span class="hljs-number">110px</span>;
<span class="hljs-attribute">transform</span>: <span class="hljs-built_in">rotate</span>(45deg);
<span class="hljs-attribute">background-color</span>: <span class="hljs-number">#073c4b</span>;
<span class="hljs-attribute">box-shadow</span>: <span class="hljs-number">0px</span> <span class="hljs-number">0px</span> <span class="hljs-number">5px</span> <span class="hljs-number">#52fefe</span> inset;
}</code></pre>
            <figure id="post-268752" class="align-none media-268752"><img src="https://cdn.css-tricks.com/wp-content/uploads/2018/03/ironman-15.jpg" srcset="https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_537,f_auto,q_auto/v1521762085/ironman-15_uvlysy.jpg 537w, https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_200,f_auto,q_auto/v1521762085/ironman-15_uvlysy.jpg 200w" sizes="(min-width: 1850px) calc( (100vw - 555px) / 3 )
(min-width: 1251px) calc( (100vw - 530px) / 2 )
(min-width: 1086px) calc(100vw - 480px)
(min-width: 626px)  calc(100vw - 335px)
calc(100vw - 30px)" alt=""></figure>
            <p>Great! That’s exactly what we want.</p>
            <p>Before creating all the eight coils, let’s create a coil container div that will contain all the eight coils:</p>
            <pre rel="HTML" class=" language-markup"><code class="language-markup">&lt;div class="fullpage-wrapper"&gt;
&lt;div class="reactor-container"&gt;
&lt;div class="tunnel circle abs-center"&gt;&lt;/div&gt;
&lt;div class="core-wrapper circle abs-center"&gt;&lt;/div&gt;
&lt;div class="core-outer circle abs-center"&gt;&lt;/div&gt;
&lt;div class="core-inner circle abs-center"&gt;&lt;/div&gt;
&lt;!-- the coil container --&gt;
&lt;div class="coil-container"&gt;
&lt;div class="coil coil-1"&gt;&lt;/div&gt;
&lt;/div&gt;
&lt;/div&gt;
&lt;/div&gt;</code></pre>
            <p>You will notice we also added a class "coil" to the "coil-1" element. We will keep all the common styles for coils in the "coil" class, and the individual coil element classes will only have their angle of rotation:</p>
            <pre rel="CSS" class=" language-css"><code class="language-css"><span class="hljs-selector-class">.coil-container</span> {
<span class="hljs-attribute">position</span>: relative;
<span class="hljs-attribute">width</span>: <span class="hljs-number">100%</span>;
<span class="hljs-attribute">height</span>: <span class="hljs-number">100%</span>;
}

<span class="hljs-selector-class">.coil</span> {
<span class="hljs-attribute">position</span>: absolute;
<span class="hljs-attribute">width</span>: <span class="hljs-number">30px</span>;
<span class="hljs-attribute">height</span>: <span class="hljs-number">20px</span>;
<span class="hljs-attribute">top</span>: <span class="hljs-built_in">calc</span>(50% - 110px);
<span class="hljs-attribute">left</span>: <span class="hljs-built_in">calc</span>(50% - 15px);
<span class="hljs-attribute">transform-origin</span>: <span class="hljs-number">15px</span> <span class="hljs-number">110px</span>;
<span class="hljs-attribute">background-color</span>: <span class="hljs-number">#073c4b</span>;
<span class="hljs-attribute">box-shadow</span>: <span class="hljs-number">0px</span> <span class="hljs-number">0px</span> <span class="hljs-number">5px</span> <span class="hljs-number">#52fefe</span> inset;
}

<span class="hljs-selector-class">.coil-1</span> {
<span class="hljs-attribute">transform</span>: <span class="hljs-built_in">rotate</span>(45deg);
}</code></pre>
            <p>The output will remain same.</p>
            <p>Now, let’s make all the eight coils inside <code>.coil-container</code>:</p>
            <pre rel="HTML" class=" language-markup"><code class="language-markup">&lt;div class="fullpage-wrapper"&gt;
&lt;div class="reactor-container"&gt;
&lt;div class="tunnel circle abs-center"&gt;&lt;/div&gt;
&lt;div class="core-wrapper circle abs-center"&gt;&lt;/div&gt;
&lt;div class="core-outer circle abs-center"&gt;&lt;/div&gt;
&lt;div class="core-inner circle abs-center"&gt;&lt;/div&gt;
&lt;!-- the coil container --&gt;
&lt;div class="coil-container"&gt;
&lt;div class="coil coil-1"&gt;&lt;/div&gt;
&lt;div class="coil coil-2"&gt;&lt;/div&gt;
&lt;div class="coil coil-3"&gt;&lt;/div&gt;
&lt;div class="coil coil-4"&gt;&lt;/div&gt;
&lt;div class="coil coil-5"&gt;&lt;/div&gt;
&lt;div class="coil coil-6"&gt;&lt;/div&gt;
&lt;div class="coil coil-7"&gt;&lt;/div&gt;
&lt;div class="coil coil-8"&gt;&lt;/div&gt;
&lt;/div&gt;
&lt;/div&gt;
&lt;/div&gt;</code></pre>
            <p>...and give different rotations to all the coils (in increment of 45 degrees):</p>
            <pre rel="CSS" class=" language-css"><code class="language-css"><span class="hljs-selector-class">.coil</span> {
<span class="hljs-attribute">position</span>: absolute;
<span class="hljs-attribute">width</span>: <span class="hljs-number">30px</span>;
<span class="hljs-attribute">height</span>: <span class="hljs-number">20px</span>;
<span class="hljs-attribute">top</span>: <span class="hljs-built_in">calc</span>(50% - 110px);
<span class="hljs-attribute">left</span>: <span class="hljs-built_in">calc</span>(50% - 15px);
<span class="hljs-attribute">transform-origin</span>: <span class="hljs-number">15px</span> <span class="hljs-number">110px</span>;
<span class="hljs-attribute">background-color</span>: <span class="hljs-number">#073c4b</span>;
<span class="hljs-attribute">box-shadow</span>: <span class="hljs-number">0px</span> <span class="hljs-number">0px</span> <span class="hljs-number">5px</span> <span class="hljs-number">#52fefe</span> inset;
}

<span class="hljs-selector-class">.coil-1</span> {
<span class="hljs-attribute">transform</span>: <span class="hljs-built_in">rotate</span>(0deg);
}

<span class="hljs-selector-class">.coil-2</span> {
<span class="hljs-attribute">transform</span>: <span class="hljs-built_in">rotate</span>(45deg);
}

<span class="hljs-selector-class">.coil-3</span> {
<span class="hljs-attribute">transform</span>: <span class="hljs-built_in">rotate</span>(90deg);
}

<span class="hljs-selector-class">.coil-4</span> {
<span class="hljs-attribute">transform</span>: <span class="hljs-built_in">rotate</span>(135deg);
}

<span class="hljs-selector-class">.coil-5</span> {
<span class="hljs-attribute">transform</span>: <span class="hljs-built_in">rotate</span>(180deg);
}

<span class="hljs-selector-class">.coil-6</span> {
<span class="hljs-attribute">transform</span>: <span class="hljs-built_in">rotate</span>(225deg);
}

<span class="hljs-selector-class">.coil-7</span> {
<span class="hljs-attribute">transform</span>: <span class="hljs-built_in">rotate</span>(270deg);
}

<span class="hljs-selector-class">.coil-8</span> {
<span class="hljs-attribute">transform</span>: <span class="hljs-built_in">rotate</span>(315deg);
}</code></pre>
            <figure id="post-268753" class="align-none media-268753"><img src="https://cdn.css-tricks.com/wp-content/uploads/2018/03/ironman-16.jpg" srcset="https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_543,f_auto,q_auto/v1521762086/ironman-16_ogjzph.jpg 543w, https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_200,f_auto,q_auto/v1521762086/ironman-16_ogjzph.jpg 200w" sizes="(min-width: 1850px) calc( (100vw - 555px) / 3 )
(min-width: 1251px) calc( (100vw - 530px) / 2 )
(min-width: 1086px) calc(100vw - 480px)
(min-width: 626px)  calc(100vw - 335px)
calc(100vw - 30px)" alt=""></figure>
            <p>Our reactor is almost ready.</p>
            <h3 id="article-header-id-4" class="has-header-link"><a class="article-headline-link" href="#article-header-id-4">#</a>Animating the Coils With CSS3 Animations</h3>
            <p>In Iron Man’s Arc reactor, the coils don’t move but they will in our reactor. We will animate the coils to rotate along the tunnel and will use CSS3 animations for this—no JavaScript.</p>
            <p>To create an animation, you need to know the initial and final states of the object you are going to animate. We define these initial and final states in CSS by using <code>@keyframes</code> at-rule:</p>
            <pre rel="CSS" class=" language-css"><code class="language-css">@<span class="hljs-keyword">keyframes</span> reactor-anim {
<span class="hljs-selector-tag">from</span> {
<span class="hljs-attribute">transform</span>: <span class="hljs-built_in">rotate</span>(0deg);
}
<span class="hljs-selector-tag">to</span> {
<span class="hljs-attribute">transform</span>: <span class="hljs-built_in">rotate</span>(360deg);
}
}</code></pre>
            <p>We want the element to be at 0 degrees and animate it until it reaches 360 degrees. And we named this animation as "reactor-anim."</p>
            <p>The element we want to animate is <code>.coil-contailer</code>. Notice, we didn’t define which object to animate yet, we have only defined the initial and the final state and name of the animation. </p>
            <p>We need to link the element to the animation in order to take effect. We do it by using <code>animation-name</code> property on <code>.coil-container</code>:</p>
            <pre rel="CSS" class=" language-css"><code class="language-css"><span class="hljs-selector-class">.coil-container</span> {
<span class="hljs-attribute">position</span>: relative;
<span class="hljs-attribute">width</span>: <span class="hljs-number">100%</span>;
<span class="hljs-attribute">height</span>: <span class="hljs-number">100%</span>;
<span class="hljs-attribute">animation-name</span>: reactor-anim;
<span class="hljs-attribute">animation-duration</span>: <span class="hljs-number">3s</span>;
}</code></pre>
            <p>Notice, we also gave the duration of animation using <code>animation-duration</code> property. This defines how much time it should take to go from the “from” state to the “to” state defined using the <code>@keyframes</code> at-rule.</p>
            <div class="cp_embed_wrapper resizable" style="height: 415px;">
                <iframe id="cp_embed_GxKZee" src="//codepen.io/supersarkar/embed/GxKZee?height=415&amp;theme-id=1&amp;slug-hash=GxKZee&amp;default-tab=result&amp;user=supersarkar&amp;embed-version=2&amp;pen-title=Arc-Reactor-Ease-In" scrolling="no" frameborder="0" height="415" allowtransparency="true" allowfullscreen="true" name="CodePen Embed" title="Arc-Reactor-Ease-In" class="cp_embed_iframe " style="width: 100%; overflow: hidden; height: 100%;"></iframe>
                <div class="win-size-grip" style="touch-action: none;"></div>
                <div class="win-size-grip" style="touch-action: none;"></div>
            </div>
            <p>We need to change two things here: we want the animation to go on infinitely and we want a linear animation. You can see the animation is slow at the beginning, then fast, then again slow at the end—this behavior is defined by the timing function of an animation.</p>
            <p>Let’s make these changes:</p>
            <pre rel="CSS" class=" language-css"><code class="language-css"><span class="hljs-selector-class">.coil-container</span> {
<span class="hljs-attribute">position</span>: relative;
<span class="hljs-attribute">width</span>: <span class="hljs-number">100%</span>;
<span class="hljs-attribute">height</span>: <span class="hljs-number">100%</span>;
<span class="hljs-attribute">animation-name</span>: reactor-anim;
<span class="hljs-attribute">animation-duration</span>: <span class="hljs-number">3s</span>;
<span class="hljs-attribute">animation-iteration-count</span>: infinite;
<span class="hljs-attribute">animation-timing-function</span>: linear;
}</code></pre>
            <p>We used <code>animation-iteration-count</code> property to set the animation to <code>infinite</code>, and <code>animation-timing-function</code> to make the animation <code>linear</code>, the default value of <code>animation-timing-function</code> is <code>ease</code>.</p>
            <div class="cp_embed_wrapper resizable" style="height: 410px;">
                <iframe id="cp_embed_vRBGwv" src="//codepen.io/supersarkar/embed/vRBGwv?height=410&amp;theme-id=1&amp;slug-hash=vRBGwv&amp;default-tab=result&amp;user=supersarkar&amp;embed-version=2&amp;pen-title=Arc-Reactor-Linear-Infinite" scrolling="no" frameborder="0" height="410" allowtransparency="true" allowfullscreen="true" name="CodePen Embed" title="Arc-Reactor-Linear-Infinite" class="cp_embed_iframe " style="width: 100%; overflow: hidden; height: 100%;"></iframe>
                <div class="win-size-grip" style="touch-action: none;"></div>
                <div class="win-size-grip" style="touch-action: none;"></div>
            </div>
            <p>We can combine all of these animation properties...</p>
            <pre rel="CSS" class=" language-css"><code class="language-css"><span class="hljs-selector-tag">animation-name</span>: <span class="hljs-selector-tag">reactor-anim</span>;
<span class="hljs-selector-tag">animation-duration</span>: 3<span class="hljs-selector-tag">s</span>;
<span class="hljs-selector-tag">animation-iteration-count</span>: <span class="hljs-selector-tag">infinite</span>;
<span class="hljs-selector-tag">animation-timing-function</span>: <span class="hljs-selector-tag">linear</span>;</code></pre>
            <p>...into one shorthand property like this:</p>
            <pre rel="CSS" class=" language-css"><code class="language-css"><span class="hljs-selector-tag">animation</span>: 3<span class="hljs-selector-tag">s</span> <span class="hljs-selector-tag">infinite</span> <span class="hljs-selector-tag">linear</span> <span class="hljs-selector-tag">reactor-anim</span>;</code></pre>
            <h3 id="article-header-id-5" class="has-header-link"><a class="article-headline-link" href="#article-header-id-5">#</a>Final Touches to the Reactor Container</h3>
            <p>Our reactor is ready, now let’s make some final changes to the <code>.reactor-container</code>. First, we will need one dark circle behind the reactor:</p>
            <pre rel="HTML" class=" language-markup"><code class="language-markup">&lt;div class="fullpage-wrapper"&gt;
&lt;div class="reactor-container"&gt;
&lt;!-- dark circle behind the reactor --&gt;
&lt;div class="reactor-container-inner circle abs-center"&gt;&lt;/div&gt;
&lt;div class="tunnel circle abs-center"&gt;&lt;/div&gt;
&lt;div class="core-wrapper circle abs-center"&gt;&lt;/div&gt;
&lt;div class="core-outer circle abs-center"&gt;&lt;/div&gt;
&lt;div class="core-inner circle abs-center"&gt;&lt;/div&gt;
&lt;div class="coil-container"&gt;
&lt;div class="coil coil-1"&gt;&lt;/div&gt;
&lt;div class="coil coil-2"&gt;&lt;/div&gt;
&lt;div class="coil coil-3"&gt;&lt;/div&gt;
&lt;div class="coil coil-4"&gt;&lt;/div&gt;
&lt;div class="coil coil-5"&gt;&lt;/div&gt;
&lt;div class="coil coil-6"&gt;&lt;/div&gt;
&lt;div class="coil coil-7"&gt;&lt;/div&gt;
&lt;div class="coil coil-8"&gt;&lt;/div&gt;
&lt;/div&gt;
&lt;/div&gt;
&lt;/div&gt;</code></pre>
            <p>Let’s give a dark background and add some glow to it:</p>
            <pre rel="CSS" class=" language-css"><code class="language-css">.reactor-container-inner {
height: 238px;
width: 238px;
background-color: rgb(22, 26, 27);;
box-shadow: 0px 0px 4px 1px #52fefe;
}</code></pre>
            <div class="cp_embed_wrapper resizable" style="height: 420px;">
                <iframe id="cp_embed_wmwWwB" src="//codepen.io/supersarkar/embed/wmwWwB?height=420&amp;theme-id=1&amp;slug-hash=wmwWwB&amp;default-tab=result&amp;user=supersarkar&amp;embed-version=2&amp;pen-title=Arc-Reactor-Semi-Final" scrolling="no" frameborder="0" height="420" allowtransparency="true" allowfullscreen="true" name="CodePen Embed" title="Arc-Reactor-Semi-Final" class="cp_embed_iframe " style="width: 100%; overflow: hidden; height: 100%;"></iframe>
                <div class="win-size-grip" style="touch-action: none;"></div>
                <div class="win-size-grip" style="touch-action: none;"></div>
            </div>
            <p>See how the dark background and the glow creates an emboss effect?</p>
            <p>Next, let’s make the <code>.rotator-container</code> round and give it some shadow and border, then we are done:</p>
            <pre rel="CSS" class=" language-css"><code class="language-css"><span class="hljs-selector-class">.reactor-container</span> {
<span class="hljs-attribute">width</span>: <span class="hljs-number">300px</span>;
<span class="hljs-attribute">height</span>: <span class="hljs-number">300px</span>;
<span class="hljs-attribute">margin</span>: auto;
<span class="hljs-attribute">border</span>: <span class="hljs-number">1px</span> dashed <span class="hljs-number">#888</span>;
<span class="hljs-attribute">position</span>: relative;
<span class="hljs-attribute">border-radius</span>: <span class="hljs-number">50%</span>;
<span class="hljs-attribute">background-color</span>: <span class="hljs-number">#384c50</span>;
<span class="hljs-attribute">border</span>: <span class="hljs-number">1px</span> solid <span class="hljs-built_in">rgb</span>(18, 20, 20);
<span class="hljs-attribute">box-shadow</span>: <span class="hljs-number">0px</span> <span class="hljs-number">0px</span> <span class="hljs-number">32px</span> <span class="hljs-number">8px</span> <span class="hljs-built_in">rgb</span>(18, 20, 20), <span class="hljs-number">0px</span> <span class="hljs-number">0px</span> <span class="hljs-number">4px</span> <span class="hljs-number">1px</span> <span class="hljs-built_in">rgb</span>(18, 20, 20) inset;
}</code></pre>
            <div class="cp_embed_wrapper resizable" style="height: 425px;">
                <iframe id="cp_embed_QmLEWN" src="//codepen.io/supersarkar/embed/QmLEWN?height=425&amp;theme-id=1&amp;slug-hash=QmLEWN&amp;default-tab=result&amp;user=supersarkar&amp;embed-version=2&amp;pen-title=Iron%20Man's%20Arc%20Reactor" scrolling="no" frameborder="0" height="425" allowtransparency="true" allowfullscreen="true" name="CodePen Embed" title="Iron Man's Arc Reactor" class="cp_embed_iframe " style="width: 100%; overflow: hidden; height: 100%;"></iframe>
                <div class="win-size-grip" style="touch-action: none;"></div>
                <div class="win-size-grip" style="touch-action: none;"></div>
            </div>
            <p>Cheers! Our Arc Reactor is ready and even with a little animation as an added bonus. To level this up, we could explore using <a href="https://css-tricks.com/making-custom-properties-css-variables-dynamic/" target="_blank">custom properties</a> to create reusable variables for our color and number values for easier maintenance. Similarly, we could look into using a preprocessor—like Sass, Less or PostCSS—to write functions that do the mathematical lifting for us. Would love to see examples like that in the comments!</p>
            <div id="jp-relatedposts" class="jp-relatedposts">
                <h3 class="jp-relatedposts-headline has-header-link" id="article-header-id-6"><a class="article-headline-link" href="#article-header-id-6">#</a><em>Related</em></h3>
                <div class="jp-relatedposts-items jp-relatedposts-items-visual jp-relatedposts-grid ">
                    <div class="jp-relatedposts-post jp-relatedposts-post0 jp-relatedposts-post-nothumbs" data-post-id="255079" data-post-format="false"><a class="jp-relatedposts-post-a jp-relatedposts-post-aoverlay" href="https://css-tricks.com/creating-yin-yang-loaders-web/" title="Creating Yin and Yang Loaders On the Web

I came across a couple such animations a while ago and this gave me the idea of creating my own versions with as little code as possible, no external libraries, using various methods, some of which take advantage of more recent features we can use these days, such as CSS…" rel="nofollow" data-origin="268736" data-position="0" target="_blank"></a>
                        <h4 class="jp-relatedposts-post-title" id="creating-yin-and-yang-loaders-on-the-web"><a class="jp-relatedposts-post-a" href="https://css-tricks.com/creating-yin-yang-loaders-web/" title="Creating Yin and Yang Loaders On the Web

I came across a couple such animations a while ago and this gave me the idea of creating my own versions with as little code as possible, no external libraries, using various methods, some of which take advantage of more recent features we can use these days, such as CSS…" rel="nofollow" data-origin="268736" data-position="0" target="_blank">Creating Yin and Yang Loaders On the Web</a></h4>
                        <p class="jp-relatedposts-post-excerpt" style="max-height: 7.5em;">I came across a couple such animations a while ago and this gave me the idea of creating my own versions with as little code as possible, no external libraries, using various methods, some of which take advantage of more recent features we can use these days, such as CSS…</p>
                        <p class="jp-relatedposts-post-date" style="display: block;">June 6, 2017</p>
                        <p class="jp-relatedposts-post-context">In "Article"</p>
                    </div>
                    <div class="jp-relatedposts-post jp-relatedposts-post1 jp-relatedposts-post-nothumbs" data-post-id="209064" data-post-format="false"><a class="jp-relatedposts-post-a jp-relatedposts-post-aoverlay" href="https://css-tricks.com/creating-a-css-sliding-background-effect/" title="Creating a CSS Sliding Background Effect

The &quot;trick&quot; of sliding backgrounds in CSS is not new. In fact, the first time I came across it might have been a couple of years ago on the Valio Con site (the current design doesn't have it anymore). I happened to notice it on a couple of new sites…" rel="nofollow" data-origin="268736" data-position="1" target="_blank"></a>
                        <h4 class="jp-relatedposts-post-title" id="creating-a-css-sliding-background-effect"><a class="jp-relatedposts-post-a" href="https://css-tricks.com/creating-a-css-sliding-background-effect/" title="Creating a CSS Sliding Background Effect

The &quot;trick&quot; of sliding backgrounds in CSS is not new. In fact, the first time I came across it might have been a couple of years ago on the Valio Con site (the current design doesn't have it anymore). I happened to notice it on a couple of new sites…" rel="nofollow" data-origin="268736" data-position="1" target="_blank">Creating a CSS Sliding Background Effect</a></h4>
                        <p class="jp-relatedposts-post-excerpt" style="max-height: 7.5em;">The "trick" of sliding backgrounds in CSS is not new. In fact, the first time I came across it might have been a couple of years ago on the Valio Con site (the current design doesn't have it anymore). I happened to notice it on a couple of new sites…</p>
                        <p class="jp-relatedposts-post-date" style="display: block;">October 9, 2015</p>
                        <p class="jp-relatedposts-post-context">In "Article"</p>
                    </div>
                    <div class="jp-relatedposts-post jp-relatedposts-post2 jp-relatedposts-post-nothumbs" data-post-id="244009" data-post-format="false"><a class="jp-relatedposts-post-a jp-relatedposts-post-aoverlay" href="https://css-tricks.com/state-css-reflections/" title="The State of CSS Reflections

I recently saw this loader on CodePen, a pure CSS 3D rotating set of bars with a fading reflection. It's done by using an element for each bar, then duplicating each and every one of these elements to create the reflection and finally adding a gradient cover to create the…" rel="nofollow" data-origin="268736" data-position="2" target="_blank"></a>
                        <h4 class="jp-relatedposts-post-title" id="the-state-of-css-reflections"><a class="jp-relatedposts-post-a" href="https://css-tricks.com/state-css-reflections/" title="The State of CSS Reflections

I recently saw this loader on CodePen, a pure CSS 3D rotating set of bars with a fading reflection. It's done by using an element for each bar, then duplicating each and every one of these elements to create the reflection and finally adding a gradient cover to create the…" rel="nofollow" data-origin="268736" data-position="2" target="_blank">The State of CSS Reflections</a></h4>
                        <p class="jp-relatedposts-post-excerpt" style="max-height: 7.5em;">I recently saw this loader on CodePen, a pure CSS 3D rotating set of bars with a fading reflection. It's done by using an element for each bar, then duplicating each and every one of these elements to create the reflection and finally adding a gradient cover to create the…</p>
                        <p class="jp-relatedposts-post-date" style="display: block;">July 29, 2016</p>
                        <p class="jp-relatedposts-post-context">In "Article"</p>
                    </div>
                </div>
            </div>
        </div>
    </div>
</article>