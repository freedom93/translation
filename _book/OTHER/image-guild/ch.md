# [图像指南](https://images.guide)·基本图片优化

[原文地址](https://images.guide/)

![Performance](images/logo.svg)

作者：[Addy Osmani](https://twitter.com/addyosmani)

鸣谢: [Kornel Lesiński](https://twitter.com/kornelski), [Estelle Weyl](https://twitter.com/estellevw), [Jeremy Wagner](https://twitter.com/malchata), [Tim Kadlec](https://twitter.com/tkadlec), [Nolan O’Brien](https://twitter.com/NolanOBrien), [Pat Meenan](https://twitter.com/patmeenan), [Kristofer Baxter](https://twitter.com/kristoferbaxter), [Henri Helvetica](https://twitter.com/HenriHelvetica), [Houssein Djirdeh](https://twitter.com/hdjirdeh), [Una Kravets](https://twitter.com/una), [Elle Osmani](https://twitter.com/ARebelBelle) and [Ilya Grigorik](https://twitter.com/igrigorik).
感谢他们的帮助和评论。

## [摘要](https://images.guide/#the-tldr)

**我们都应该实现图像压缩的自动化。**

图像优化应该是自动化的。很容易忘记，最佳实践发生变化，而且不经过构建管道的内容很容易丢失。自动化：在构建过程中使用[Imagemin](https://github.com/imagemin/imagemin)或[libvip](https://github.com/jcupitt/libvips)。这些有许多替代方案。

大多数CDN(如[Akamai](https://www.akamai.com/us/en/solutions/why-akamai/image-management.jsp))和第三方解决方案，如[Cloudinary](https://cloudinary.com/)、[imgix](https://imgix.com/)、[Fastly’s Image Optimizer](https://www.fastly.com/io/)、[Instart Logic’s SmartVision](https://www.instartlogic.com/technology/machine-learning/smartvision)或[ImageOptim API](https://imageoptim.com/api)都提供了全面的自动图像优化解决方案。

在阅读博客文章和调整配置上花费的时间超过了服务的月费(Cloudinary有一个[免费](http://cloudinary.com/pricing)的层)。如果您不想关心这项工作外包的成本或延迟问题，那么上面的开源选项是可靠的。像[Imageflow](https://github.com/imazen/imageflow)或[Thumbor](https://github.com/thumbor/thumbor)这样的项目启用了自我托管的替代方案。

**每个人都应该高效地压缩自己的图像。**

至少：使用[ImageOptim](https://imageoptim.com/)。它可以显着地减小图像的大小，同时保持视觉质量。也可以使用Windows和Linux[替代方案](https://imageoptim.com/versions.html)。

更具体地说：通过[MozJPEG](https://github.com/mozilla/mozjpeg)运行JPEG(对于Web内容来说，Q=80或更低都没问题)并考虑[Progressive JPEG](http://cloudinary.com/blog/progressive_jpegs_and_green_martians)支持，PNGs通过[pngquant](https://pngquant.org/)，SVGS通过[SVGO](https://github.com/svg/svgo)。显式删除元数据(-带用于pngquant)以避免膨胀。代替超级巨大的GIF动画，提供[H.264](https://en.wikipedia.org/wiki/H.264/MPEG-4_AVC)视频(或为Chrome、Firefox和Opera提供[WebM](https://www.webmproject.org/))！如果你至少不能用[Giflossy](https://github.com/pornel/giflossy)。如果您可以节省额外的CPU周期，需要高于web的平均质量，并且对缓慢的编码时间没有问题：试试[Guetzli](https://research.googleblog.com/2017/03/announcing-guetzli-new-open-source-jpeg.html)。

一些浏览器通过接受请求头来宣布对图像格式的支持。这可以用于有条件地提供格式：例如，基于闪烁的浏览器(如Chrome)使用有损[WebP](https://developers.google.com/speed/webp/)，而对于其他浏览器则使用JPEG/PNG。

总是有很多你能做到的。存在生成和服务srcset断点的工具。在具有[客户端提示](https://developers.google.com/web/updates/2015/09/automating-resource-selection-with-client-hints)的基于闪烁的浏览器中，资源选择可以自动化，并且如果用户选择在浏览器中“保存数据”，那么可以通过遵从保存数据提示来减少字节数。

您可以使你的图像文件大小越小，您就可以为用户提供更好的网络体验-尤其是在移动平台上。在这篇文章中，我们将探讨通过现代压缩技术减少图像大小的方法，并将对图像质量的影响降到最低。

<details open>
    <summary style="display: block;"><h2>目录</h2></summary>
    <p></p>
    <ul>
        <li><a href="#">1.介绍</a></li>
        <li><a href="#">2.如何判断我的图像是否需要优化?</a></li>
        <li><a href="#">3.如何选择图像格式?</a></li>
        <li><a href="#">4.卑微的JPEG</a></li>
        <li><a href="#">5.JPEG压缩模式</a>
            <ul>
                <li><a href="#the-advantages-of-progressive-jpegs">渐进式JPEG的优点</a></li>
                <li><a href="#whos-using-progressive-jpegs-in-production">谁在生产中使用渐进式JPEG?</a></li>
                <li><a href="#the-disadvantages-of-progressive-jpegs">渐进式JPEGs的缺点</a></li>
                <li><a href="#how-to-create-progressive-jpegs">如何创建Progressive JPEGs?</a></li>
                <li><a href="#chroma-subsampling">色度(或颜色)二次采样</a></li>
                <li><a href="#how-far-have-we-come-from-the-jpeg">我们离JPEG还有多远?</a></li>
                <li><a href="#optimizing-jpeg-encoders">优化JPEG编码器</a></li>
                <li><a href="#what-is-mozjpeg">MozJPEG是什么?</a></li>
                <li><a href="#what-is-guetzli">Guetzli是什么?</a></li>
                <li><a href="#mozjpeg-vs-guetzli">MozJPEG与Guetzli相比如何?</a></li>
                <li><a href="#butteraugli">Butteraugli</a></li>
            </ul>
        </li>
        <li><a href="#">6.什么是WebP?</a>
            <ul>
                <li><a href="#how-does-webp-perform">WebP的性能如何?</a></li>
                <li><a href="#whos-using-webp-in-production">谁在生产中使用WebP?</a></li>
                <li><a href="#how-does-webp-encoding-work">WebP编码是如何工作的?</a></li>
                <li><a href="#webp-browser-support">WebP浏览器支持t</a></li>
                <li><a href="#how-do-i-convert-to-webp">我的图像如何转换成WebP?</a></li>
                <li><a href="#how-do-i-view-webp-on-my-os">如何查看我的操作系统上的WebP图像?</a></li>
                <li><a href="#how-do-i-serve-webp">我如何提供WebP?</a></li>
            </ul>
        </li>
        <li><a href="#">7.SVG优化</a></li>
        <li><a href="#">8.避免使用有损编解码器重新压缩图像</a></li>
        <li><a href="#">9.减少不必要的图像解码并调整成本</a>
            <ul>
                <li><a href="#delivering-hidpi-with-srcset">提供HiDPI图像使用<code>srcset</code></a></li>
                <li><a href="#art-direction">艺术指导</a></li>
            </ul>
        </li>
        <li><a href="">10.色彩管理</a></li>
        <li><a href="">11.图像精灵</a></li>
        <li><a href="">12.延迟加载非关键图像</a></li>
        <li><a href="">13.避免 <code>display: none;</code> 陷阱</a></li>
        <li><a href="">14.图像处理CDN对您有意义吗？</a></li>
        <li><a href="">15.缓存图像资源</a></li>
        <li><a href="">16.预加载关键图像资源</a></li>
        <li><a href="">17.图像的性能预算</a></li>
        <li><a href="">18.结束建议</a></li>
        <li><a href="">19.了解更多</a></li>
    </ul>
    <p></p>
</details>

## [介绍](https://images.guide/#introduction)

**图片仍然是造成网络膨胀的首要原因。**

图像占用了大量的互联网带宽，因为它们通常有较大的文件大小。根据[HTTP存档](http://httparchive.org/)，60%用于获取网页的数据是由JPEG、PNG和GIF组成的图像。截至2017年7月，图片在3.0MB平均站点加载的内容中占了[1.7MB](http://httparchive.org/interesting.php#bytesperpage)。

根据Tammy Everts，将图像添加到页面或使现有图像更大已被[证明](https://calendar.perfplanet.com/2014/images-are-king-an-image-optimization-checklist-for-everyone-in-your-organization/)可以提高转化率。图像不太可能消失，因此投资于有效的压缩策略以尽量减少膨胀变得非常重要。

每页图片越少，转换越多。

![Performance](images/Modern-Image00-large.jpg)

平均每页19幅图像的转换优于平均每页31幅图像。

根据Soasta/Google 2016年的研究，图片是第二大转换预测指标，最佳页面的图片数量减少了38%。

图像优化包含各种不同的方法，它们都可以减少图像的文件大小。这最终取决于你的图像所要求的视觉保真度。

![Performance](images/image-optimisation-large.jpeg)

图像优化：选择正确的格式，仔细压缩，并将关键图像优先于那些可能被延迟加载的图像。

常见的图像优化包括压缩，使用[``<picture>``](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/picture)/[``<img srcset>``](https://developer.mozilla.org/en-US/docs/Learn/HTML/Multimedia_and_embedding/Responsive_images)响应地根据屏幕大小为它们服务，以及调整它们的大小以降低图像解码成本。

潜在图像节省的直方图

![Performance](images/chart_naedwl-large.jpg)

根据HTTP存档，在第95百分位数(查看累积分布函数)的每幅图像节省的费用是30 KB！

有足够的空间让我们共同优化图像更好。

![Performance](images/image-optim-large.jpg)

ImageOptim在Mac上使用，已经压缩了50%以上的图像，这是免费的，可以通过现代压缩技术和剥离不必要的EXIF元数据来减少图像大小。

如果您是一个设计师，也有一个[Sketch的ImageOptim插件](https://github.com/ImageOptim/Sketch-plugin)，将优化您的资产导出。我发现它节省了很多时间。

## [如何判断我的图像是否需要优化?](https://images.guide/#do-my-images-need-optimization)

通过[WebPageTest.org](https://www.webpagetest.org/)执行站点审核，它将突出显示更好地优化图像的机会(参见“压缩图像”)。

![Performance](images/Modern-Image1-large.jpg)

网页测试报告中的“压缩图像”部分列出了可以更有效地压缩的图像以及这样做估计的文件大小节省。

![Performance](images/Modern-Image2-medium.jpg)

[Lighthouse](https://developers.google.com/web/tools/lighthouse/)是审核性能的最佳实践。它包括对图像优化的审核，并可以为可能被进一步压缩的图像提供建议，或者指出屏幕外的图像可能是延迟加载的。

从Chrome 60开始，Lighthouse现在为Chrome DevTools的[审核小组](https://developers.google.com/web/updates/2017/05/devtools-release-notes#lighthouse)提供力量：

![Performance](images/hbo-large.jpg)

Lighthouse可以审核Web性能，最佳实践和改进Web应用功能。

您也可能熟悉其他性能审核工具，如[PageSpeed](https://developers.google.com/speed/pagespeed/insights/)、[Insight](https://developers.google.com/speed/pagespeed/insights/)或通过Cloudinary的[Website Speed Test](https://webspeedtest.cloudinary.com/)，其中包括详细的图像分析审核。

## [如何选择图像格式?](https://images.guide/#choosing-an-image-format)

正如Ilya Grigorik在其出色的[图像优化指南](https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/image-optimization)中所指出的，图像的“正确格式”是所期望的视觉结果和功能需求的结合。你是在处理栅格图像还是矢量图像？

![Performance](images/rastervvector-small.png)

[光栅图形](https://en.wikipedia.org/wiki/Raster_graphics)通过对矩形像素网格内的每个像素的值进行编码来表示图像。 它们不是分辨率或独立缩放的。 WebP或广泛支持的格式（如JPEG或PNG）可以很好地处理这些图形，其中照片写实是必需的。 我们讨论过的Guetzli，MozJPEG和其他想法很适用于光栅图形。

[矢量图形](https://en.wikipedia.org/wiki/Vector_graphics)使用点，线和多边形来表示图像和格式，使用简单的几何形状（例如logo）提供高分辨率和像SVG一样的缩放处理这个用例更好。

错误的格式会使你付出代价。选择正确格式的逻辑流程可能充满风险，因此尝试其他格式可以在一定程度上节省费用。

Jeremy Wagner在他的图像优化演讲中谈到了在评估格式时值得考虑的[权衡](http://jlwagner.net/talks/these-images/#/2/2)问题。

## [卑微的JPEG](https://images.guide/#the-humble-jpeg)

[JPEG](https://en.wikipedia.org/wiki/JPEG)很可能是世界上使用最广泛的图像格式。如前所述，在HTTP Archive爬虫的站点上看到的图像中，有[45%是JPEG](https://httparchive.org/reports/state-of-the-web?start=latest)。你的手机，你的数码单反相机，旧的网络摄像头-一切都支持这个编解码器。它也很古老，可以追溯到1992年第一次发行的时候。在这段时间里，有大量的研究试图改进它所提供的东西。

JPEG是一种有损压缩算法，它为了节省空间而丢弃信息，并试图在尽量保持文件大小的同时保持视觉保真度。

**用例可以接受什么样的图像质量？**

JPEG等格式最适合具有多个颜色区域的照片或图像。 大多数优化工具将允许您设置您满意的压缩级别; 较高的压缩会减小文件大小，但会引入伪像，晕圈或块状降级。

![Performance](https://images.guide/images/book-images/Modern-Image5-large.jpg)

JPEG：当我们从最佳质量转换到最低质量时，可感知的JPEG压缩伪像会增加。 请注意，一个工具中的图像质量分数与另一个工具中的质量分数非常不同。

在选择要选择的质量设置时，请考虑您的图片属于哪个质量范畴：

+ **最好的质量**-当质量比带宽更重要的时候。这可能是因为图像在您的设计中具有很高的显着性，或者是以完全分辨率显示的。

+ **好的质量**-当你关心更小的文件大小时，但是不想对图像质量产生太大的负面影响。用户仍然关心某种程度的图像质量。

+ **低质量**-当你足够关心带宽，图像退化是可以的。这些图像适用于杂乱无章的网络环境。

+ **最低的质量**-带宽节约是最重要的。用户希望有一个不错的体验，但为了更快地加载页面，用户将接受相当降级的体验。

接下来，让我们谈谈JPEG的压缩模式，因为这些模式会对感知的性能产生很大的影响。

注意：我们有时可能高估了用户所需的图像质量。图像质量可以被认为是偏离理想的，非压缩源。这也可以是主观的。

## [JPEG压缩模式](https://images.guide/#jpeg-compression-modes)

JPEG图像格式有多种不同的[压缩模式](http://cs.haifa.ac.il/~nimrod/Compression/JPEG/J5mods2007.pdf)。流行的三种模式是基线(顺序)、渐进式JPEG(PJPEG)和无损。

基线(或顺序)JPEG和渐进式JPEG有什么不同？

基线JPEG(大多数图像编辑和优化工具默认的压缩模式)是以一种相对简单的方式编码和解码的：自上而下。当基线JPEG加载在缓慢或不稳定的连接上时，用户会看到图像的顶部，并将更多的图像显示为图像加载。与无损JPEG相似，但压缩比较小。

![Performance](https://images.guide/images/book-images/Modern-Image6-large.jpg)

基线JPEG加载从上到下的基线JPEG从上到下加载，而渐进式JPEG加载从模糊到锐利。渐进式JPEG将图像划分为多个扫描。第一次扫描显示图像在模糊或低质量设置和后续扫描提高图像质量。把这看作是“逐步”精炼它。每一幅图像的“扫描”都会增加更多的细节。当结合在一起，这创造了一个完整的质量形象。

![Performance](https://images.guide/images/book-images/Modern-Image7-large.jpg)

基线JPEG从上到下加载图像.PJPEG从低分辨率(模糊)到高分辨率加载图像。Pat Meenan还编写了一个交互式工具来测试和学习渐进式JPEG扫描。

通过把数码相机或编辑器添加的[EXIF数据删除](http://www.verexif.com/en/)，优化图像的[Huffman表](https://en.wikipedia.org/wiki/Huffman_coding)或重新扫描图像，都可以实现无损JPEG优化。 像[jpegtran](http://jpegclub.org/jpegtran/)这样的工具通过重新排列压缩数据而不会降低图像质量来实现无损压缩。 [jpegrescan](https://github.com/kud/jpegrescan)、[jpegoptim](https://github.com/tjko/jpegoptim)和[mozjpeg](https://github.com/mozilla/mozjpeg)（我们将在稍后介绍）也支持无损JPEG压缩。

<h3 id="the-advantages-of-progressive-jpegs"><a href="https://images.guide/#the-advantages-of-progressive-jpegs">渐进式JPEG的优点</a></h3>

PJPEG能够在加载图像时提供低分辨率的“预览”-用户可以感觉到与自适应图像相比，图像加载速度更快。

在较慢的3G连接上，当只接收到部分文件时，用户可以(粗略地)查看图像中的内容，并调用是否等待文件完全加载。这可能比基线JPEG提供的自上而下的图像显示更令人愉快。

![Performance](https://images.guide/images/book-images/pjpeg-graph-large.png)

2015年，[Facebook改用了PJPEG(用于iOS应用程序)](https://code.facebook.com/posts/857662304298232/faster-photos-in-facebook-for-ios/)，数据使用量减少了10%。他们能够显示一个高质量的图像比以前快15%，优化感知加载时间，如上图所示。

PJPEG可以提高压缩性能，与基线/简单JPEG相比，对10 kb以上的图像消耗[2-10%](http://www.bookofspeed.com/chapter5.html)的更少带宽。他们更高的压缩比是由于JPEG中的每一次扫描都能够有自己的专用的可选的[Huffman表](https://en.wikipedia.org/wiki/Huffman_coding)。现代JPEG编码器(如[libjpeg-turbo](http://libjpeg-turbo.virtualgl.org/)、MozJPEG等)利用PJPEG的灵活性更好地打包数据。

注：为什么PJPEG压缩更好？基线JPEG块一次编码一个。使用PJPEG，可以对多个块的相似[离散余弦变换](Discrete Cosine Transform)系数进行编码，从而获得更好的压缩效果。

<h3 id="whos-using-progressive-jpegs-in-production"><a href="https://images.guide/#whos-using-progressive-jpegs-in-production">谁在生产中使用渐进式JPEG？</a></h3>
+ [twitter.com推出了“渐进式JPEG”](推出了“渐进式JPEG”)以85%的质量为基准。他们测量了用户感知的延迟(第一次扫描的时间和总体的加载时间)，发现总的来说，PJPEG在满足低文件大小、可接受的代码转换和解码时间方面具有竞争力。

+ Facebook为其iOS应用程序发布了渐进式JPEG。他们发现它将数据使用减少了10%，并使他们能够提速15%显示高质量的图像。

+ Yelp转而使用渐进式JPEG，发现这在一定程度上是他们减少图像大小约4.5%的原因。他们还使用MozJPEG额外节省了13.8%。

许多其他多图像的网站，如Pinterest，也在生产中使用渐进式JPEG。

![Performance](https://images.guide/images/book-images/pinterest-loading-large.png)

Pinterest JPEG都是逐步编码的。这优化了用户体验，通过逐个扫描加载用户体验。

<h3 id="the-disadvantages-of-progressive-jpegs"><a href="https://images.guide/#the-disadvantages-of-progressive-jpegs">渐进式JPEG的缺点</a></h3>

PJPEG的解码速度可能比基线JPEG慢-有时需要3×3倍的时间。在拥有强大CPU的台式计算机上，这可能不是什么值得关注的问题，但在资源有限的移动设备上却不是如此。显示不完整的层需要工作是基本上是多次解码图像。这些多次传递会占用CPU周期。

渐进式JPEG也并不总是很小。对于非常小的图像(如缩略图)，渐进式JPEG可能比它们的基线对应的要大。然而，对于如此小的缩略图，渐进式渲染可能并没有提供太多的价值。

这意味着，在决定是否发布PJPEG时，您需要对文件大小、网络延迟和CPU周期的使用进行实验，并找到合适的平衡。

注意：PJPEG(和所有JPEG)有时可以在移动设备上进行硬件解码。它不会改善RAM的影响，但可以消除一些CPU问题。并非所有Android设备都支持硬件加速，但高端设备支持，所有iOS设备也都支持。

一些用户可能认为渐进加载是一个缺点，因为很难判断图像何时已经完成加载。由于这可能会对每个用户有很大的影响，所以请评估对您自己的用户有意义的内容。

<h3 id="the-disadvantages-of-progressive-jpegs"><a href="https://images.guide/#the-disadvantages-of-progressive-jpegs">如何创建渐进式JPEG?</a></h3>

像[ImageMagick](https://www.imagemagick.org/)、[libjpeg](http://libjpeg.sourceforge.net/)、[jpegtran](http://jpegclub.org/jpegtran/)、[jpeg-recompress](https://github.com/danielgtaylor/jpeg-archive)和[imagemin](https://github.com/imagemin/imagemin)这些工具和库都支持导出渐进式JPEG。如果您有一个现有的图像优化管道，添加渐进加载支持的可能性很大：

```javascript
const gulp = require('gulp');
const imagemin = require('gulp-imagemin');

gulp.task('images', function () {
    return gulp.src('images/*.jpg')
        .pipe(imagemin({
            progressive: true
        }))
        .pipe(gulp.dest('dist'));       
});
```

大多数图像编辑工具默认情况下将图像保存为基线JPEG文件。

![Performance](https://images.guide/images/book-images/photoshop-large.jpg)

大多数图像编辑工具默认将图像保存为基线JPEG文件。您可以将在Photoshop中创建的任何图像保存为渐进式JPEG，方法是点击File -> Export -> save for Web (legacy)，然后单击Progressive选项。Sketch也支持导出渐进式jpeg -导出为JPG，并在保存图像时选中“渐进式”复选框。

您可以将在Photoshop中创建的任何图像保存为渐进式JPEG，方法是点击File -> Export -> save for Web (legacy)，然后单击Progressive选项。
Sketch还支持导出渐进式jpeg -导出为JPG，并在保存图像时选中“渐进式”复选框。

<h3 id="chroma-subsampling"><a href="https://images.guide/#chroma-subsampling">色度(或颜色)二次采样</a></h3>

我们的眼睛对图像中颜色细节(色度)的丢失比亮度(简称luma——亮度的度量)更宽容。[色度二次采样](https://en.wikipedia.org/wiki/Chroma_subsampling)是一种压缩形式，它降低了有利于luma的信号中颜色的精度。这可以在不影响图像质量的情况下减少文件大小(在某些情况下减少[15-17%](https://calendar.perfplanet.com/2015/why-arent-your-images-using-chroma-subsampling/))，是JPEG图像的一种选择。二次采样还可以减少图像内存的使用。

![Performance](https://images.guide/images/book-images/luma-signal-large.jpg)

信号=色度+流明

由于对比度负责形成我们在图像中看到的形状，因此定义它的luma非常重要。
旧的或过滤过的黑白照片可能不包含颜色，但多亏了luma，它们可以像彩色照片一样详细。
色度(颜色)对视觉感知的影响较小。

![Performance](https://images.guide/images/book-images/no-subsampling-large.jpg)

JPEG支持许多不同的二次采样类型:none、horizontal、horizontal和vertical。
这张图表来自弗雷德里克·凯泽的[《马蹄蟹的jpeg》](http://frdx.free.fr/JPEG_for_the_horseshoe_crabs.pdf)。

在讨论子抽样时，有许多常见的样本。一般是4:4:4,4:2:2,4:2:0。但是这些代表什么呢?假设一个子样本的格式是a:B:C。A是一行中的像素数，对于jpeg，通常是4。B表示第一行的颜色量，C表示第二行的颜色量。

+ 4:4:4没有压缩，所以颜色和流明完全传输。
+ 4:2:2水平半采样，垂直全采样。
+ 4:2:0从第一行的一半像素中采样颜色，忽略第二行。

注:jpegtran和cjpeg支持亮度和色度的独立质量配置。可以添加-sample标志(例如-sample 2x1)。一些好的一般规则:二次采样(-sample 2x2)对于照片来说非常好。无二次采样(-采样1x1)是最好的截图，横幅和按钮。最后一个折衷(2x1)是你不确定用什么。通过减少色度组件中的像素，可以显著减少颜色组件的大小，最终减少字节大小。

通过减少色度组件中的像素，可以显著减少颜色组件的大小，最终减少字节大小。

![Performance](https://images.guide/images/book-images/subsampling-large.jpg)

Chrome二次采样配置的JPEG在质量80。

对于大多数类型的图像，色度二次采样是值得考虑的。它也有一些值得注意的例外:由于亚采样依赖于我们眼睛的局限性，它并不适用于压缩那些颜色细节可能与亮度同样重要的图像(例如医学图像)。

包含字体的图像也会受到影响，因为文本的次采样不好会降低其可读性。使用JPEG时，更锐利的边缘更难以压缩，因为JPEG的设计是为了更好地处理过渡柔和的照片场景。

![Performance](https://images.guide/images/book-images/Screen_Shot_2017-08-25_at_11.06.27_AM-large.jpg)

[理解JPEG](http://compress-or-die.com/Understanding-JPG/)推荐坚持4:4:4的二次抽样(1×1)在处理图像包含文本。

了解更多:在JPEG规范中没有指定色度二次采样的确切方法，因此不同的解码器处理它的方式不同。MozJPEG和libjpeg-turbo使用相同的缩放方法。旧版本的libjpeg使用了一种不同的方法，该方法以颜色添加边缘振荡效应。

注：Photoshop在使用“Save for web”功能时自动设置色度二次采样。当图像质量设置在51-100之间时，完全不使用子采样(4:4:4)。当质量低于此值时，将使用4:2:0子采样。这就是为什么在将质量从51切换到50时可以观察到更大的文件大小缩减。

注:在分抽样讨论中，经常提到[YCbCr](https://en.wikipedia.org/wiki/YCbCr)这个术语。这个模型可以表示经过伽玛校正的[RGB](https://en.wikipedia.org/wiki/RGB_color_model)颜色空间。Y为伽玛校正亮度，Cb为蓝色的色度分量，Cr为红色的色度分量。如果查看ExifData，您将看到YCbCr位于抽样级别的旁边。

有关色度子采样的进一步阅读，请参见[为什么您的图像不使用色度二次采样?](https://calendar.perfplanet.com/2015/why-arent-your-images-using-chroma-subsampling/)。

<h3 id="how-far-have-we-come-from-the-jpeg"><a href="https://images.guide/#how-far-have-we-come-from-the-jpeg">我们离JPEG还有多远?</a></h3>

以下是网络上图像格式的现状:

摘要——有很多碎片。我们经常需要有条件地为不同的浏览器提供不同的格式，以利用任何现代的东西。

![Performance](https://images.guide/images/book-images/format-comparison-large.jpg)

Different modern image formats (and optimizers) used to demonstrate what is possible at a target file-size of 26KB. We can compare quality using SSIM (structural similarity) or Butteraugli, which we’ll cover in more detail later.
JPEG 2000 (2000) – an improvement to JPEG switching from a discrete cosine based transform to a wavelet-based method. Browser support: Safari desktop + iOS
JPEG XR (2009) – alternative to JPEG and JPEG 2000 supporting HDR and wide gamut color spaces. Produces smaller files than JPEG at slightly slower encode/decode speeds. Browser support: Edge, IE.

不同的现代图像格式(和优化器)用于演示在目标文件大小为26KB时可以实现的功能。我们可以使用[SSIM](https://en.wikipedia.org/wiki/Structural_similarity)(结构相似性)或[Butteraugli](https://github.com/google/butteraugli)来比较质量，稍后我们将更详细地介绍这两种方法。

+ [JPEG 2000](https://en.wikipedia.org/wiki/JPEG_2000) **(2000)** - 从离散余弦变换到小波变换的改进。**浏览器支持:Safari桌面+ iOS**

+ [JPEG XR](https://en.wikipedia.org/wiki/JPEG_XR) **(2009)** - 替代JPEG和JPEG 2000支持[HDR]()http://wikivisually.com/wiki/High_dynamic_range_imaging和宽[色域](http://wikivisually.com/wiki/Gamut)空间。以稍慢的编码/解码速度生成比JPEG更小的文件。**浏览器支持:Edge, IE**。

+ [WebP](https://en.wikipedia.org/wiki/WebP) **(2010)** – 基于块预测的格式，由谷歌支持有损和无损压缩。通常用于提供与JPEG相关的字节节省和透明支持字节密集型png。缺乏色度二次采样配置和渐进加载。解码时间也比JPEG解码慢。**浏览器支持:Chrome, Opera。用Safari和火狐做过实验**。

+ [FLIF](https://en.wikipedia.org/wiki/Free_Lossless_Image_Format) **(2015)** – 无损图像格式声称优于PNG，无损WebP，无损BPG和无损jpeg2000的压缩比。**浏览器支持:没有。注意浏览器中有一个**[JS解码器](https://github.com/UprootLabs/poly-flif)。

+ **HEIF and BPG** 从压缩的角度来看，它们是相同的，但是有不同的包装:

+ [BPG](https://en.wikipedia.org/wiki/Better_Portable_Graphics) (2015) – 旨在基于HEVC([高效视频编码](http://wikivisually.com/wiki/High_Efficiency_Video_Coding))，更高效地替代JPEG。与MozJPEG和WebP相比，它提供了更好的文件大小。由于许可证问题，不太可能获得广泛关注。**浏览器支持:没有。注意浏览器中有一个**[JS解码器](https://bellard.org/bpg/)。

+ [HEIF](https://en.wikipedia.org/wiki/High_Efficiency_Image_File_Format) **(2015)** – 用于存储具有约束内部预测的hev编码图像的图像和图像序列的格式。苹果公司宣布在[WWDC](https://www.cnet.com/news/apple-ios-boosts-heif-photos-over-jpeg-wwdc/)他们会探索转向HEIF JPEG iOS,引用2×节省有14。**浏览器支持:编写本文时不支持。最后是Safari桌面和iOS 11**。

如果您比较直观，您可能会喜欢上面[这些](http://xooyoozoo.github.io/yolo-octo-bugfixes/#cologne-cathedral&jpg=s&webp=s)可视化比较工具中的[一种](https://people.xiph.org/~xiphmont/demo/daala/update1-tool2b.shtml)。

因此，**浏览器支持是分散的**，如果您希望利用上述任何一种支持，您可能需要有条件地为每个目标浏览器提供反馈。
在谷歌上，我们已经看到了WebP的一些承诺，所以我们将很快深入研究它。

You can also serve image formats (e.g. WebP, JPEG 2000) with a .jpg extension (or any other) as the browser can render an image it can decide the media type. This allows for server-side content-type negotiation to decide which image to send without needing to change the HTML at all. Services like Instart Logic use this approach when delivering images to their customers.

您还可以使用.jpg扩展名(或任何其他扩展名)提供图像格式(例如WebP、JPEG 2000)，因为浏览器可以呈现它可以决定媒体类型的图像。这允许服务器端[内容类型协商](https://www.igvita.com/2012/12/18/deploying-new-image-formats-on-the-web/)来决定发送哪个图像，而根本不需要更改HTML。像Instart Logic这样的服务在向客户交付图像时使用这种方法。

接下来，让我们讨论当您不能有条件地提供不同的图像格式时的一种选择:**优化JPEG编码器**。

<h3 id="optimizing-jpeg-encoders"><a href="https://images.guide/#optimizing-jpeg-encoders">优化JPEG编码器</a></h3>

现代JPEG编码器试图生成更小、更高保真度的JPEG文件，同时保持与现有浏览器和图像处理应用程序的兼容性。它们避免了在生态系统中引入新的图像格式或更改以实现压缩增益的需要。两个这样的编码器是MozJPEG和Guetzli。

tl;dr Which optimising JPEG Encoder should you use?

摘要：**你应该使用哪种优化的JPEG编码器**?

+ 通用web资源:MozJPEG
+ 质量是您主要关心的问题，您不介意长时间的编码:使用Guetzli
+ 如果你需要可配置性:
    - [JPEGRecompress](https://github.com/danielgtaylor/jpeg-archive)(在底层使用MozJPEG)
    - [JPEGMini](http://www.jpegmini.com/) 它类似于Guetzli -自动选择最好的质量。它在技术上没有Guetzli那么复杂，但速度更快，目标是更适合web的质量范围。
    - [ImageOptim API](https://imageoptim.com/api) (这里有免费的在线界面)-它在处理颜色方面是独一无二的。您可以选择颜色质量与整体质量分开。它会自动选择色度子采样级别，以在截图中保留高分辨率的颜色，但避免在自然照片的平滑颜色上浪费字节。

<h3 id="what-is-mozjpeg"><a href="https://images.guide/#what-is-mozjpeg">MozJPEG是什么?</a></h3>

Mozilla以[MozJPEG](https://github.com/mozilla/mozjpeg)的形式提供了一个现代化的JPEG编码器。它[声称](https://research.mozilla.org/2014/03/05/introducing-the-mozjpeg-project/)可以将JPEG文件减少10%。
使用MozJPEG压缩的文件可以跨浏览器工作，它的一些特性包括渐进式扫描优化、[网格量化](https://en.wikipedia.org/wiki/Trellis_quantization)(丢弃压缩最少的细节)和一些不错的[量化表预置](https://calendar.perfplanet.com/2014/mozjpeg-3-0/)，这些预置有助于创建更平滑的高dpi图像(尽管如果您愿意仔细研究XML配置，使用ImageMagick可以做到这一点)。

这两种[ImageOptim](https://github.com/ImageOptim/ImageOptim/issues/45)都支持MozJPEG，并且有一个相对可靠的[imagemin插件](https://github.com/imagemin/imagemin-mozjpeg)。
下面是一个带有Gulp的示例实现:

```javascript
const gulp = require('gulp');
const imagemin = require('gulp-imagemin');
const imageminMozjpeg = require('imagemin-mozjpeg');

gulp.task('mozjpeg', () =>
    gulp.src('src/*.jpg')
    .pipe(imagemin([imageminMozjpeg({
        quality: 85
    })]))
    .pipe(gulp.dest('dist'))
);
```

![Performance](https://images.guide/images/book-images/Modern-Image10-large.jpg)

![Performance](https://images.guide/images/book-images/Modern-Image11-large.jpg)

MozJPEG:文件大小和不同质量的视觉相似度得分的比较。

我使用[jpeg-archive](https://github.com/imagemin/imagemin-jpeg-recompress)项目中的[jpeg-compress](https://github.com/danielgtaylor/jpeg-archive)来计算源图像的SSIM(结构相似性)分数。SSIM是一种测量两幅图像之间相似度的方法，其中SSIM评分是一幅图像在另一幅图像被认为“完美”的情况下的质量度量。

根据我的经验，MozJPEG是一个很好的选择，它可以以高视觉质量压缩web图像，同时减少文件大小。对于中小型图像，我发现MozJPEG (at quality=80-85)在保持可接受的SSIM的同时，在文件大小上节省了30-40%，比jpeg-turbo提高了5-6%。它确实比基线JPEG的[编码成本要低](http://www.libjpeg-turbo.org/About/Mozjpeg)，但是您可能不会发现这是一个问题。

注:如果您需要一个支持MozJPEG的工具，该工具具有额外的配置支持和一些免费的图像比较实用工具，请查看[jpeg-recompress](https://github.com/danielgtaylor/jpeg-archive)。《Web Performance in Action》一书的作者Jeremy Wagner在使用[这种](https://twitter.com/malchata/status/884836650563579904)配置时取得了一些成功。

<h3 id="what-is-guetzli"><a href="https://images.guide/#what-is-guetzli">Guetzli是什么?</a></h3>

[Guetzli](https://github.com/google/guetzli)是一个很有前途的，虽然很慢，但是可以感知的JPEG编码器，它来自谷歌，它试图找到最小的JPEG，这种JPEG在感知上与人眼无法区分。它执行一系列的实验，为最终的JPEG生成一个建议，解释每个建议的心理视觉错误。其中，它选择得分最高的提案作为最终输出。

为了测量图像之间的差异，Guetzli使用[Butteraugli](https://github.com/google/butteraugli)，一种基于人类感知的图像差异测量模型(下文讨论)。
Guetzli可以考虑一些其他JPEG编码器所没有的视觉特性。例如，看到的绿光的数量和对蓝色的敏感度之间有关系，所以在绿色附近的蓝色变化可以不那么精确地编码。

注:图像文件大小更依赖于质量的选择，而不是编解码器的选择。与切换编解码器可能节省的文件大小相比，最低质量的jpeg和最高质量的jpeg之间的文件大小差异要大得多。使用最低可接受质量是非常重要的。不要把你的质量定得太高而不去注意它。

Guetzli[声称](https://research.googleblog.com/2017/03/announcing-guetzli-new-open-source-jpeg.html)，与其他压缩器相比，给定Butteraugli评分的图像数据大小可以减少20-30%。使用Guetzli需要注意的是，它非常非常慢，目前只适用于静态内容。从README可以看出，Guetzli需要大量的内存——每百万像素需要1分钟+ 200MB内存。在这个GitHub线程中有一个关于Guetzli的真实体验的很好的线程。当您将优化图像作为静态站点构建过程的一部分时，它是理想的，但是在按需执行时，它就不那么理想了。

注:Guetzli可能更适合在静态站点的构建过程中优化图像，或者在图像优化没有按需执行的情况下。
ImageOptim等工具支持Guetzli优化(在最新版本中)。

```javascript
const gulp = require('gulp');
const imagemin = require('gulp-imagemin');
const imageminGuetzli = require('imagemin-guetzli');

gulp.task('guetzli', () =>
    gulp.src('src/*.jpg')
    .pipe(imagemin([
        imageminGuetzli({
            quality: 85
        })
    ]))
    .pipe(gulp.dest('dist'))

);
```

![Performance](https://images.guide/images/book-images/Modern-Image12-large.jpg)

使用Guetzli对3x3mp图像进行编码几乎花费了7分钟(CPU使用率很高)，节省了大量的时间。对于存档高分辨率的照片，我可以看到这提供了一些价值。

![Performance](https://images.guide/images/book-images/Modern-Image13-large.jpg)

Guetzli：不同质量的文件大小和视觉相似度得分的比较。

注:建议在高质量的图像(例如未压缩的输入图像、PNG源或100%质量或关闭的jpeg)上运行Guetzli。虽然它可以用于其他图像(例如质量为84或更低的jpeg)，但效果可能更差。

虽然用Guetzli压缩图片非常(非常)耗时，而且会让你的粉丝旋转，但对于大图片来说，这是值得的。我看到过很多例子，在保持视觉保真度的情况下，它可以在任何地方节省40%的文件大小。
这使得它非常适合存档照片。在中小型图像上，我仍然看到了一些节省(在10-15KB范围内)，但是它们没有那么明显。Guetzli可以在压缩较小的图像时引入更多的流体式失真。

您可能还对Eric Portis研究感兴趣，将Guetzli与Cloudinary的自动压缩进行[比较](https://cloudinary.com/blog/a_closer_look_at_guetzli)，以获得有效的不同数据点。

### How does MozJPEG compare to Guetzli?
Comparing different JPEG encoders is complex – one needs to compare both the quality and fidelity of the compressed image as well as the final size. As image compression expert Kornel Lesiński notes, benchmarking one but not both of these aspects could lead to invalid conclusions.


<h3 id="mozjpeg-vs-guetzli"><a href="https://images.guide/#mozjpeg-vs-guetzli">MozJPEG与Guetzli相比如何?</a></h3>

比较不同的JPEG编码器是复杂的—需要比较压缩图像的质量和保真度以及最终大小。作为图像压缩专家Kornel Lesiński指出,基准测试的一个而不是两个这些方面可能会导致[无效](https://kornel.ski/faircomparison)的结论。

MozJPEG与Guetzli相比如何? – Kornel的观点:

+ Guetzli为高质量的图像进行了调优(butteraugli被认为是q=90+的最佳选择，MozJPEG的最佳点在q=75左右)
+ Guetzli的压缩速度要慢得多(两者都产生标准的jpeg，因此解码和往常一样快)
+ MozJPEG不会自动选择质量设置，但是您可以使用外部工具(例如[jpeg-archive](https://github.com/danielgtaylor/jpeg-archive))找到最优的质量

有许多方法可用于确定压缩图像在视觉上是否与源文件相似或在感知上是否相似。图像质量研究通常使用像[SSIM](https://en.wikipedia.org/wiki/Structural_similarity)(结构相似性)这样的方法。然而Guetzli对Butteraugli进行了优化。

Butteraugli is a project by Google that estimates the point when a person may notice visual image degradation (the psychovisual similarity) of two images. It gives a score for the images that is reliable in the domain of barely noticeable differences. Butteraugli not only gives a scalar score, but also computes a spatial map of the level of differences. While SSIM looks at the aggregate of errors from an image, Butteraugli looks at the worst part.

<h3 id="butterauglii"><a href="https://images.guide/#butterauglii">Butteraugli</a></h3>

[Butteraugli](https://github.com/google/butteraugli)是谷歌的一个项目，它估计一个人可能注意到两幅图像的视觉退化(心理视觉相似性)的时间点。它给那些在几乎没有明显差异的区域内可靠的图像打分。Butteraugli不仅给出了一个标量分数，而且还计算了差异级别的空间地图。当SSIM查看来自图像的错误集合时，Butteraugli查看最糟糕的部分。

![Performance](https://images.guide/images/book-images/Modern-Image14-medium.jpg)

上面的例子使用Butteraugli找到了JPEG质量阈值的最小值，而此时用户还没有注意到一些不清楚的地方。它使总文件大小减少了65%。

在实践中，您将为视觉质量定义一个目标目标，然后运行许多不同的图像优化策略，查看Butteraugli评分，然后选择最适合文件大小和级别的平衡。

![Performance](https://images.guide/images/book-images/Modern-Image15-large.jpg)

总之,我花了大约30分钟安装后启动本地Butteraugli和在我的MAC上正确的编译C++源码的构建。然后使用它相对简单:指定两个图像比较(源和压缩版),它会给你一个分数。

**Butteraugli与其他比较视觉相似性的方法有何不同?**

来自Guetzli项目成员的[评论](https://github.com/google/guetzli/issues/10#issuecomment-276295265)表明，Guetzli在Butteraugli上得分最高，在SSIM和MozJPEG上得分最低。这与我对自己的图像优化策略的研究是一致的。我在图像上运行Butteraugli和一个节点模块(如[img-ssim](https://www.npmjs.com/package/img-ssim))，将源代码与Guetzli和MozJPEG之前/之后的SSIM评分进行比较。

**结合编码器吗?**

对于较大的图像，我发现将Guetzli与MozJPEG中的**无损压缩**(jpegtran，而不是cjpeg，以避免丢弃Guetzli所做的工作)相结合，可以进一步减少10-15%的文件大小(总体减少55%)，而SSIM只减少很小的一部分。我想提醒大家的是，这需要实验和分析，但这一领域的其他人，如[Ariya Hidayat](https://ariya.io/2017/03/squeezing-jpeg-images-with-guetzli)，也曾尝试过，结果值得期待。

MozJPEG是一个对初学者友好的网络资产编码器，它的速度相对较快，可以生成高质量的图像。由于Guetzli是资源密集型的，最适合处理更大、质量更高的图像，所以我将它保留给中级到高级用户。

