<article id="post-270572" role="main" class="instapaper_body h-entry e-content">

    <header class="mega-header">

      <h1 class="p-name">
                CSS Environment Variables              </h1>

    </header>

    <p class="author-byline">

      <span class="author-and-date">
                By
        <a href="https://css-tricks.com/author/chriscoyier/">
                    <span class="p-author">
            Chris Coyier          </span>
        </a>
                <span class="slashes">On</span>
        <time datetime="2018-05-04" class="dt-published">
          May 4, 2018        </time>
      </span>

              <span class="byline-tags">
          <svg class="icon-tag" width="12px" height="12px"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#icon-tag"></use></svg><a href="https://css-tricks.com/tag/custom-properties/" rel="tag">custom properties</a>, <a href="https://css-tricks.com/tag/environment-variables/" rel="tag">environment variables</a>        </span>
      
    </p>

    <div class="article-content">

      
      <p>We were all introduced to the <code>env()</code> function in CSS when all that drama about <a href="https://css-tricks.com/the-notch-and-css/">"The Notch" and the iPhone X</a> was going down. The way that Apple landed on helping us move content away from those "unsafe" areas was to provide us essentially hard-coded variables to use:</p>
<pre rel="CSS" class=" language-css"><code class=" language-css"><span class="token property">padding</span><span class="token punctuation">:</span> 
  <span class="token function">env</span><span class="token punctuation">(</span>safe-area-inset-top<span class="token punctuation">)</span> 
  <span class="token function">env</span><span class="token punctuation">(</span>safe-area-inset-right<span class="token punctuation">)</span> 
  <span class="token function">env</span><span class="token punctuation">(</span>safe-area-inset-bottom<span class="token punctuation">)</span> 
  <span class="token function">env</span><span class="token punctuation">(</span>safe-area-inset-left<span class="token punctuation">)</span><span class="token punctuation">;</span></code></pre>
<p>Uh ok! Weird! Now, nine months later, <a href="https://drafts.csswg.org/css-env-1/">an "Unofficial Proposal Draft" for <code>env()</code></a> has landed. This is how specs work, as I understand it. Sometimes browser vendors push forward with stuff they need, and then it's standardized. It's not always waiting around for standards bodies to invent things and then browser vendors implementing those things.</p>
<p><span id="more-270572"></span></p>
<p>Are environment variables something to get excited about? Heck yeah! In a sense, they are like a more-limited version of <a href="https://css-tricks.com/guides/css-custom-properties/">CSS Custom Properties</a>, but that means they can be potentially used for <em>more things</em>. </p>
<twitterwidget class="twitter-tweet twitter-tweet-rendered" id="twitter-widget-1" style="position: static; visibility: visible; display: block; transform: rotate(0deg); max-width: 100%; width: 500px; min-width: 220px; margin-top: 10px; margin-bottom: 10px;" data-tweet-id="990569495432450048"></twitterwidget>
<twitterwidget class="twitter-tweet twitter-tweet-rendered" id="twitter-widget-2" style="position: static; visibility: visible; display: block; transform: rotate(0deg); max-width: 100%; width: 500px; min-width: 220px; margin-top: 10px; margin-bottom: 10px;" data-tweet-id="991088767522951168"></twitterwidget>
<p>Eric also points out some very awesome early thinking:</p>
<blockquote>
<p>ISSUE 4 - Define the full set of places <code>env()</code> can be used.</p>
<ul>
<li>Should be able to replace any subset of MQ syntax, for example.</li>
<li>Should be able to replace selectors, maybe?</li>
<li>Should it work on a rule level, so you can insert arbitrary stuff into a rule, like reusing a block of declarations?</li>
</ul>
</blockquote>
<p>Probably still changeable-with-JavaScript as well. I would think the main reason CSS Custom Properties <em>don't</em> work with media queries and selectors and such is because they <em>do</em> work with the cascade, which opens up some very strange infinite loop logic where it makes sense CSS doesn't want to tread.</p>
<p>If you're into the PostCSS thing, there is <a href="https://github.com/jonathantneal/postcss-env-function">a plugin</a>! But I'd warn... the <a href="https://css-tricks.com/issue-preprocessing-css-custom-properties/">same issues that befall preprocessing CSS Custom Properties</a> applies here (except the first one in that article). </p>
<p><script async="" src="https://platform.twitter.com/widgets.js" charset="utf-8"></script></p>

<div id="jp-relatedposts" class="jp-relatedposts">
  <h3 class="jp-relatedposts-headline has-header-link" id="article-header-id-0"><a class="article-headline-link" href="#article-header-id-0">#</a><em>Related</em></h3>
<div class="jp-relatedposts-items jp-relatedposts-items-visual jp-relatedposts-grid "><div class="jp-relatedposts-post jp-relatedposts-post0 jp-relatedposts-post-thumbs" data-post-id="260090" data-post-format="false"><a class="jp-relatedposts-post-a" href="https://css-tricks.com/the-notch-and-css/" title="&quot;The Notch&quot; and CSS

Apple's iPhone X has a screen that covers the entire face of the phone, save for a &quot;notch&quot; to make space for a camera and other various components. The result is some awkward situations for screen design, like constraining websites to a &quot;safe area&quot; and having white bars on the…" rel="nofollow" data-origin="270572" data-position="0"><img class="jp-relatedposts-post-img" src="https://i0.wp.com/css-tricks.com/wp-content/uploads/2017/09/iphonex-safari.png?resize=350%2C200&amp;ssl=1" width="350" alt="" the="" notch"="" and="" css"=""></a><h4 class="jp-relatedposts-post-title"><a class="jp-relatedposts-post-a" href="https://css-tricks.com/the-notch-and-css/" title="&quot;The Notch&quot; and CSS

Apple's iPhone X has a screen that covers the entire face of the phone, save for a &quot;notch&quot; to make space for a camera and other various components. The result is some awkward situations for screen design, like constraining websites to a &quot;safe area&quot; and having white bars on the…" rel="nofollow" data-origin="270572" data-position="0">"The Notch" and CSS</a></h4><p class="jp-relatedposts-post-excerpt">Apple's iPhone X has a screen that covers the entire face of the phone, save for a "notch" to make space for a camera and other various components. The result is some awkward situations for screen design, like constraining websites to a "safe area" and having white bars on the…</p><p class="jp-relatedposts-post-date" style="display: block;">September 16, 2017</p><p class="jp-relatedposts-post-context">In "Article"</p></div><div class="jp-relatedposts-post jp-relatedposts-post1 jp-relatedposts-post-nothumbs" data-post-id="241610" data-post-format="false"><a class="jp-relatedposts-post-a jp-relatedposts-post-aoverlay" href="https://css-tricks.com/intro-bedrock-wordpress/" title="An Intro to Bedrock for WordPress

The following is a guest post by Alessandro Vendruscolo, who wrote to me excited to write a guest post about a WordPress tool that I didn't know much about: Bedrock. It's not a theme, it's a way to install, configure, and manage WordPress with security and modern development practices in…" rel="nofollow" data-origin="270572" data-position="1"></a><h4 class="jp-relatedposts-post-title"><a class="jp-relatedposts-post-a" href="https://css-tricks.com/intro-bedrock-wordpress/" title="An Intro to Bedrock for WordPress

The following is a guest post by Alessandro Vendruscolo, who wrote to me excited to write a guest post about a WordPress tool that I didn't know much about: Bedrock. It's not a theme, it's a way to install, configure, and manage WordPress with security and modern development practices in…" rel="nofollow" data-origin="270572" data-position="1">An Intro to Bedrock for WordPress</a></h4><p class="jp-relatedposts-post-excerpt" style="max-height: 7.5em;">The following is a guest post by Alessandro Vendruscolo, who wrote to me excited to write a guest post about a WordPress tool that I didn't know much about: Bedrock. It's not a theme, it's a way to install, configure, and manage WordPress with security and modern development practices in…</p><p class="jp-relatedposts-post-date" style="display: block;">May 17, 2016</p><p class="jp-relatedposts-post-context">In "Article"</p></div><div class="jp-relatedposts-post jp-relatedposts-post2 jp-relatedposts-post-thumbs" data-post-id="255312" data-post-format="false"><a class="jp-relatedposts-post-a" href="https://css-tricks.com/browserlist-good-idea/" title="Browserslist is a Good Idea

As front-end developers, we're well aware that different browsers (and versions) support different web platform features. We make choices based on the support of those features balanced with what analytics tell us about what browsers our users use. For example, if our Google Analytics tell us only 0.01% of users…" rel="nofollow" data-origin="270572" data-position="2"><img class="jp-relatedposts-post-img" src="https://i1.wp.com/css-tricks.com/wp-content/uploads/2017/05/browserlist-logo.png?resize=350%2C200&amp;ssl=1" width="350" alt="Browserslist is a Good Idea"></a><h4 class="jp-relatedposts-post-title"><a class="jp-relatedposts-post-a" href="https://css-tricks.com/browserlist-good-idea/" title="Browserslist is a Good Idea

As front-end developers, we're well aware that different browsers (and versions) support different web platform features. We make choices based on the support of those features balanced with what analytics tell us about what browsers our users use. For example, if our Google Analytics tell us only 0.01% of users…" rel="nofollow" data-origin="270572" data-position="2">Browserslist is a Good Idea</a></h4><p class="jp-relatedposts-post-excerpt">As front-end developers, we're well aware that different browsers (and versions) support different web platform features. We make choices based on the support of those features balanced with what analytics tell us about what browsers our users use. For example, if our Google Analytics tell us only 0.01% of users…</p><p class="jp-relatedposts-post-date" style="display: block;">May 30, 2017</p><p class="jp-relatedposts-post-context">In "Article"</p></div></div></div>
    </div>

  </article>