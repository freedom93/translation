## [WebP是什么?](https://images.guide/#what-is-webp)

[WebP](https://developers.google.com/speed/webp/)是来自谷歌的一种最新的图像格式，旨在提供更小的文件大小，在可接受的视觉质量下进行无损和有损压缩。它包括对alpha通道透明度和动画的支持。

在过去的一年中，WebP在有损和无损模式下的压缩性能比传统的压缩性能提高了几个百分点，而在速度方面，该算法的解压缩性能提高了10%，速度提高了一倍。WebP不是一个用于所有目的的工具，但是它在图像压缩社区中有一定的地位和不断增长的用户基础。让我们看看这是为什么。

![Performance](https://images.guide/images/book-images/Modern-Image16-large.jpg)

WebP:比较文件大小和不同质量下的视觉相似度得分。

<h3 id="how-does-webp-perform"><a href="https://images.guide/#how-does-webp-perform">WebP的性能如何?</a></h3>

**有损压缩**

使用VP8或VP9视频关键帧编码变体的WebP有损文件平均被WebP团队引用为比JPEG文件小25-34%。

在低质量范围(0-50)，WebP比JPEG有很大的优势，因为它可以模糊掉难看的块状工件。中等质量的设置(- m4 - q75)是默认的平衡速度/文件大小。在较高的范围(80-99)，WebP的优势缩小。建议在速度比质量更重要的地方使用WebP。

**无损压缩**

[WebP无损文件比PNG文件小26%](https://developers.google.com/speed/webp/docs/webp_lossless_alpha_study)。与PNG相比，无损加载时间减少了3%。也就是说，您通常不希望在web上为用户提供无损的服务。无损边缘和锐边(如非jpeg)是有区别的。无损的WebP可能更适合存档内容。

**透明度**

WebP有一个无损的8位透明通道，仅比PNG多22%的字节。它还支持有损RGB透明性，这是WebP独有的特性。

**元数据**

WebP文件格式支持EXIF照片元数据和XMP数字文档元数据。它还包含ICC颜色配置文件。

WebP提供了更好的压缩，但代价是CPU更密集。早在2013年,WebP的压缩速度比JPEG慢了大约10×，但现在可以忽略不计(一些图片可能2×慢)。对于作为构建的一部分进行处理的静态图像，这应该不是一个大问题。动态生成的映像可能会造成可感知的CPU开销，您需要对其进行评估。

注:WebP有损质量设置不能与JPEG直接比较。“70%质量”的JPEG与“70%质量”的WebP图像将大不相同，因为WebP通过丢弃更多的数据来实现更小的文件大小。

<h3 id="whos-using-webp-in-production"><a href="https://images.guide/#whos-using-webp-in-production">谁在生产中使用WebP?</a></h3>

许多大公司在生产中使用WebP来降低成本和减少网页加载时间。

谷歌报告说，使用WebP比其他有损压缩方案节省30-35%，每天处理430亿张图像请求，其中26%是无损压缩。这是大量的请求和大量的节省。如果[浏览器支持](http://caniuse.com/#search=webp)更好、更广泛，节省的成本无疑会更大。谷歌也在谷歌Play和YouTube等制作网站上使用。

Netflix、Amazon、Quora、Yahoo、Walmart、Ebay、The Guardian、Fortune和USA Today都使用WebP为支持它的浏览器压缩和提供图像。VoxMedia为Chrome用户切换到WebP，将Verge的[加载时间缩短了1-3秒](https://product.voxmedia.com/2015/8/13/9143805/performance-update-2-electric-boogaloo)。在切换到为Chrome用户提供服务时，[500px](https://iso.500px.com/500px-color-profiles-file-formats-and-you/)的图像文件大小平均减少了25%，图像质量接近或更好。

这个样本列表中指出的公司里还有不少其他公司支持WebP。

![Performance](https://images.guide/images/book-images/webp-conversion-large.jpg)

Google的WebP使用：每天在YouTube，Google Play，Chrome数据保护程序和G +上提供每天430亿次WebP图像请求。

<h3 id="how-does-webp-encoding-work"><a href="https://images.guide/#how-does-webp-encoding-work">WebP编码是如何工作的?</a></h3>

WebP的有损编码针对与JPEG静止图像相比。WebP有损编码有三个关键阶段:

**Macro-blocking**——把图像分解为16×16(宏观)亮度像素的小块和两个8×8色像素的小块。这听起来很熟悉jpeg进行颜色空间转换、色度通道下采样和图像细分的想法。

![Performance](https://images.guide/images/book-images/Modern-Image18-medium.png)

**Prediction**——每一个4×4宏模块的子块都有预测模型应用,有效过滤。它定义了一个块周围的两组像素——a(它上面的行)和L(它左边的列)。使用这两个编码器测试块填满4×4像素和确定哪些创建值最接近原来的块。
Colt McAnlis更深入地讨论了[WebP有损模式的工作方式](https://medium.com/@duhroach/how-webp-works-lossly-mode-33bd2b1d0670)。

![Performance](https://images.guide/images/book-images/Modern-Image19-small.png)

应用离散余弦变换（DCT），其步骤类似于JPEG编码。 关键的区别在于使用[算术压缩器](https://www.youtube.com/watch?v=FdMoL3PzmSA&index=7&list=PLOU2XLYxmsIJGErt5rrCqaSGTMyyqNt2H)和JPEG的霍夫曼。

如果您想深入了解，Google Developer的文章[WebP Compression Techniques](https://developers.google.com/speed/webp/docs/compression)将深入探讨这一主题。

<h3 id="webp-browser-support"><a href="https://images.guide/#webp-browser-support">WebP浏览器支持</a></h3>

并不是所有的浏览器都支持WebP，但是[根据CanIUse.com的数据](http://caniuse.com/webp)，全球用户支持率约为74%。Chrome和Opera都支持它。Safari、Edge和Firefox都曾试用过，但尚未正式发布。这通常将获取WebP图像的任务不是留给用户，而留给web开发人员。稍后将对此进行详细介绍。

以下是主要的浏览器和支持信息:

+ Chrome: Chrome在23版本开始全面支持。

+ Android版Chrome:从Chrome 50开始

+ Android: 自Android 4.2开始

+ Opera: 12.1

+ Opera Mini: 所有版本

+ Firefox: 一些测试版支持

+ Edge: 一些测试版支持

+ Internet Explorer: 不支持

+ Safari: 一些测试版支持

WebP也有它的缺点。它缺乏全分辨率的颜色空间选项，不支持渐进式解码。也就是说，WebP的工具是不错的，并且支持浏览器，尽管在编写本文时仅限于Chrome和Opera，但它可能已经覆盖了足够多的用户，因此值得考虑使用一个后备工具。

<h3 id="how-do-i-convert-to-webp"><a href="https://images.guide/#how-do-i-convert-to-webp">我如何把图像转成WebP?</a></h3>

一些商业和开源的图像编辑和处理包支持WebP。一个特别有用的应用程序是XnConvert: 一个免费的、跨平台的批处理图像转换器。

注意：避免将低质量或平均质量的JPEG转换为WebP非常重要。 这是一个常见错误，可以使用JPEG压缩工件生成WebP图像。 这可能导致WebP效率降低，因为它必须保存图像和JPEG添加的失真，导致您在质量上损失两次。 Feed转换应用程序是可用的最佳质量源文件，最好是原始文件。

<h4><a href="http://www.xnview.com/en/xnconvert/">XnConvert</a></h4>

XnConvert支持批处理图像，兼容500多种图像格式。您可以组合80多个单独的操作以多种方式转换或编辑图像。

![Performance](https://images.guide/images/book-images/Modern-Image20-large.png)

XnConvert支持批处理图像优化，允许直接从源文件转换为WebP和其他格式。除了压缩，XnConvert还可以帮助进行元数据剥离、裁剪、颜色深度定制和其他转换。xnview网站上列出的一些选项包括:

+ 元数据: 编辑

+ 变换: 旋转，裁剪，调整大小

+ 调整: 亮度，对比度，饱和度

+ 滤镜: 模糊，浮雕，锐化

+ 效果: 掩蔽，水印，渐晕

操作的结果可以导出到大约70种不同的文件格式，包括WebP。XnConvert对于Linux、Mac和Windows是免费的。强烈推荐使用XnConvert，特别是对于小型企业。

**Node modules**

[Imagemin](https://github.com/imagemin/imagemin)是一个流行的图像缩小模块，它还有一个将图像转换为WebP的附加组件([Imagemin-WebP](https://github.com/imagemin/imagemin-webp))。它同时支持有损和无损模式。

安装imagemin和imagemin-webp运行:

```> npm install --save imagemin imagemin-webp```

然后，我们可以在两个模块中都require()，并在项目目录中的任何图像(例如jpeg)上运行它们。下面我们使用有损编码与WebP编码器质量为60:

```
const imagemin = require('imagemin');
const imageminWebp = require('imagemin-webp');

imagemin(['images/*.{jpg}'], 'images', {
    use: [
        imageminWebp({quality: 60})
    ]
}).then(() => {
    console.log(‘Images optimized’);
});
```

Similar to JPEGs, it’s possible to notice compression artefacts in our output. Evaluate what quality setting makes sense for your own images. Imagemin-webp can also be used to encode lossless quality WebP images (supporting 24-bit color and full transparency) by passing lossless: true to options:

与jpeg类似，可以在输出中注意到压缩构件。
评估什么样的质量设置对您自己的图像有意义。
Imagemin-webp还可以通过传递无损:true to options来编码无损质量的WebP图像(支持24位颜色和完全透明):

const imagemin = require('imagemin');
const imageminWebp = require('imagemin-webp');

imagemin(['images/*.{jpg,png}'], 'build/images', {
    use: [
        imageminWebp({lossless: true})
    ]
}).then(() => {
    console.log(‘Images optimized’);
});

A WebP plugin for Gulp by Sindre Sorhus built on imagemin-webp and a WebP loader for WebPack are also available. The Gulp plugin accepts any options the imagemin add-on does:
由Sindre Sorhus在imagemin-webp上构建的用于Gulp的WebP插件和用于WebPack的WebP加载器也可用。
Gulp插件接受imagemin插件的所有选项:

const gulp = require('gulp');
const webp = require('gulp-webp');

gulp.task('webp', () =>
    gulp.src('src/*.jpg')
    .pipe(webp({
        quality: 80,
        preset: 'photo',
        method: 6
    }))
    .pipe(gulp.dest('dist'))
);

Or lossless:
或无损耗:

const gulp = require('gulp');
const webp = require('gulp-webp');

gulp.task('webp-lossless', () =>
    gulp.src('src/*.jpg')
    .pipe(webp({
        lossless: true
    }))
    .pipe(gulp.dest('dist'))
);

Batch image optimization using Bash
批处理图像优化使用Bash

XNConvert supports batch image compression, but if you would prefer to avoid using an app or a build system, bash and image optimization binaries keep things fairly simple.
XNConvert支持批处理图像压缩，但是如果您希望避免使用应用程序或构建系统，bash和图像优化二进制文件可以使事情相当简单。

You can bulk convert your images to WebP using cwebp:
你可以批量转换您的图像到WebP使用cwebp:

find ./ -type f -name '*.jpg' -exec cwebp -q 70 {} -o {}.webp \;
Or bulk optimize your image sources with MozJPEG using jpeg-recompress:
或批量优化您的图像源与MozJPEG使用jpeg-recompress:

find ./ -type f -name '*.jpg' -exec jpeg-recompress {} {} \;
and trim those SVGs down using svgo (which we’ll cover later on):
并使用svgo(我们将在后面介绍)来削减这些SVGs:

find ./ -type f -name '*.svg' -exec svgo {} \;
Jeremy Wagner has a more comprehensive post on image optimization using Bash and another on doing this work in parallel worth reading.
Jeremy Wagner有一篇关于使用Bash进行图像优化的更全面的文章，还有一篇关于并行完成这项工作的文章，值得一读。

Other WebP image processing and editing apps include:
其他WebP图像处理和编辑应用包括:

Leptonica — An entire website of open source image processing and analysis Apps.
Sketch supports outputting directly to WebP
GIMP — Free, open source Photoshop alternative. Image editor.
ImageMagick — Create, compose, convert, or edit bitmap images. Free. Command-Line app.
Pixelmator — Commercial image editor for Mac.
Photoshop WebP Plugin — Free. Image import and export. From Google.
Android: You can convert existing BMP, JPG, PNG or static GIF images to WebP format using Android Studio. For more information, see Create WebP Images Using Android Studio.
Leptonica—一个完整的开源图像处理和分析应用程序网站。
草图支持直接输出到WebP
免费的，开放源码的Photoshop替代品。
图像编辑器。
ImageMagick -创建、组合、转换或编辑位图图像。
免费的。
命令行应用程序。
Pixelmator - Mac的商业图像编辑器。
Photoshop WebP插件-免费。
图像导入和导出。
从谷歌。
Android:您可以使用Android Studio将现有的BMP、JPG、PNG或静态GIF图像转换为WebP格式。
有关更多信息，请参见使用Android Studio创建WebP图像。

How do I view WebP images on my OS?
While you can drag and drop WebP images to Blink-based browsers (Chrome, Opera, Brave) to preview them, you can also preview them directly from your OS using an add-on for either Mac or Windows.
我如何查看我的操作系统上的WebP图像?
虽然你可以拖拽WebP图片到基于flash的浏览器(Chrome, Opera, Brave)来预览它们，但你也可以使用Mac或Windows的附加组件直接从你的操作系统中预览它们。

Facebook experimented with WebP a few years ago and found that users who tried to right-click on photos and save them to disk noticed they wouldn’t be displayed outside their browser due to them being in WebP. There were three key problems here:
几年前，Facebook尝试使用WebP，发现那些试图右键单击照片并将其保存到磁盘的用户注意到，由于照片在WebP中，它们不会显示在浏览器之外。
这里有三个关键问题:

"Save as" but unable to view WebP files locally. This was fixed by Chrome registering itself as a ".webp" handler.
"Save as" then attaching the image to an email and sharing with someone without Chrome. Facebook solved this by introducing a prominent "download" button in their UI and returning a JPEG when users requested the download.
Right click > copy URL -> share URL on the web. This was solved by content-type negotiation.
These issues might matter less to your users, but is an interesting note on social shareability in passing. Thankfully today, utilities exist for viewing and working with WebP on different operating systems.
“另存为”，但无法在本地查看WebP文件。
这是固定的Chrome注册自己为“。
webp”处理程序。
“另存为”，然后将图片附加到电子邮件中，与没有Chrome的人分享。
Facebook解决了这个问题，它在用户界面中引入了一个突出的“下载”按钮，并在用户请求下载时返回一个JPEG。
右击>复制URL ->在web上共享URL。
这是通过内容类型协商解决的。
这些问题对您的用户来说可能不那么重要，但是顺便提一下，这是一个关于社交可共享性的有趣说明。
值得庆幸的是，现在有一些实用程序可以在不同的操作系统上查看和使用WebP。

On Mac, try the Quick Look plugin for WebP (qlImageSize). It works pretty well:
在Mac上，试试WebP的Quick Look插件(qlImageSize)。
它工作得很好:

Desktop on a mac showing a WebP file previewed using the Quick Look plugin for WebP files
On Windows, you can also download the WebP codec package allowing WebP images to be previewed in the File Explorer and Windows Photo Viewer.
在mac电脑的桌面显示一个WebP文件预览使用快速浏览插件的WebP文件
在Windows上，您还可以下载WebP编解码器包，允许在文件管理器和Windows照片查看器中预览WebP图像。

How do I serve WebP?
Browsers without WebP support can end up not displaying an image at all, which isn’t ideal. To avoid this there are a few strategies we can use for conditionally serving WebP based on browser support.
我如何提供WebP?
没有WebP支持的浏览器最终可能根本不显示图像，这是不理想的。
为了避免这种情况，我们可以使用一些策略来基于浏览器支持有条件地提供WebP。

The Chrome DevTools Network panel displaying the waterfall for the Play Store in Chrome, where WebP is served.
The Chrome DevTools Network panel highlighting WebP files being conditionally served to Blink-based browsers under the ‘Type’ column.
While the Play store delivers WebP to Blink, it falls back to JPEGs for browsers like Firefox.
While the Play store delivers WebP to Blink, it falls back to JPEGs for browsers like Firefox.
Here are some of the options for getting WebP images from your server to your user:
Chrome开发工具网络面板显示瀑布的播放商店在Chrome，其中WebP服务。
Chrome DevTools网络面板的“Type”列下，有条件地为基于blink的浏览器提供WebP文件的高亮显示。
当Play store向Blink提供WebP时，它又回到了Firefox等浏览器的jpeg模式。
当Play store向Blink提供WebP时，它又回到了Firefox等浏览器的jpeg模式。
下面是一些从服务器获取WebP图像到用户的选项:

Using .htaccess to Serve WebP Copies

Here’s how to use a .htaccess file to serve WebP files to supported browsers when a matching .webp version of a JPEG/PNG file exists on the server.

使用。htaccess提供WebP副本

下面是当服务器上存在匹配的. WebP版本的JPEG/PNG文件时，如何使用.htaccess文件向支持的浏览器提供WebP文件。

Vincent Orback recommended this approach:

Browsers can signal WebP support explicitly via an Accept header. If you control your backend, you can return a WebP version of an image if it exists on disk rather than formats like JPEG or PNG. This isn’t always possible however (e.g. for static hosts like GitHub pages or S3) so be sure to check before considering this option.

Vincent Orback推荐这种方法:

浏览器可以通过Accept头显式地发出WebP支持的信号。
如果您控制后端，则可以返回存在于磁盘上的图像的WebP版本，而不是JPEG或PNG等格式。
但是这并不总是可能的(例如，对于静态主机，如GitHub pages或S3)，所以在考虑这个选项之前一定要检查一下。

Here is a sample .htaccess file for the Apache web server:
下面是Apache web服务器的.htaccess文件示例:

<IfModule mod_rewrite.c>

  RewriteEngine On

  # Check if browser support WebP images
  RewriteCond %{HTTP_ACCEPT} image/webp

  # Check if WebP replacement image exists
  RewriteCond %{DOCUMENT_ROOT}/$1.webp -f

  # Serve WebP image instead
  RewriteRule (.+)\.(jpe?g|png)$ $1.webp [T=image/webp,E=accept:1]

</IfModule>

<IfModule mod_headers.c>

    Header append Vary Accept env=REDIRECT_accept

</IfModule>

AddType  image/webp .webp
If there are issues with the .webp images appearing on the page, make sure that the image/webp MIME type is enabled on your server.
如果页面上出现的.webp图像有问题，请确保在服务器上启用了image/webp MIME类型。

Apache: add the following code to your .htaccess file:

AddType image/webp .webp
Nginx: add the following code to your mime.types file:

image/webp webp;
Note: Vincent Orback has a sample htaccess config for serving WebP for reference and Ilya Grigorik maintains a collection of configuration scripts for serving WebP that can be useful.
注意:Vincent Orback有一个用于服务WebP的htaccess配置示例供参考，Ilya Grigorik维护了一组用于服务WebP的配置脚本，这些脚本可能很有用。
Using the ``<picture>`` Tag

The browser itself is capable of choosing which image format to display through the use of the ``<picture>`` tag. The ``<picture>`` tag utilizes multiple ``<source>`` elements, with one ``<img>`` tag, which is the actual DOM element which contains the image. The browser cycles through the sources and retrieves the first match. If the ``<picture>`` tag isn’t supported in the user’s browser, a ``<div>`` is rendered and the ``<img>`` tag is used.
浏览器本身可以通过使用``<picture>``标记来选择要显示的图像格式。
``<picture>``标签使用多个``<source>``元素，其中一个``<img>``标签是包含图像的实际DOM元素。
浏览器循环遍历源并检索第一个匹配项。
如果用户浏览器中不支持``<picture>``标记，则呈现``<div>``并使用``<img>``标记。

Note: Be careful with the position of ``<source> ``as order matters. Don’t place image/webp sources after legacy formats, but instead put them before. Browsers that understand it will use them and those that don’t will move onto more widely supported frameworks. You can also place your images in order of file size if they’re all the same physical size (when not using the media attribute). Generally this is the same order as putting legacy last.
Here is some sample HTML:
注意:注意``<source>``的位置，因为顺序关系。
不要将图像/webp源放在遗留格式之后，而是将它们放在前面。
理解它的浏览器将使用它们，不理解它的浏览器将转移到更广泛支持的框架上。
如果图像的物理大小相同(不使用media属性时)，也可以将它们按文件大小排序。
通常，这与将遗留放在最后的顺序相同。
下面是一些HTML示例:

``
<picture>
  <source srcset="/path/to/image.webp" type="image/webp">
  <img src="/path/to/image.jpg" alt="">
</picture>

<picture>   
    <source srcset='paul_irish.jxr' type='image/vnd.ms-photo'>  
    <source srcset='paul_irish.jp2' type='image/jp2'>
    <source srcset='paul_irish.webp' type='image/webp'>
    <img src='paul_irish.jpg' alt='paul'>
</picture>

<picture>
   <source srcset="photo.jxr" type="image/vnd.ms-photo">
   <source srcset="photo.jp2" type="image/jp2">
   <source srcset="photo.webp" type="image/webp">
   <img src="photo.jpg" alt="My beautiful face">
</picture>
``
Automatic CDN conversion to WebP

Some CDNs support automated conversion to WebP and can use client hints to serve up WebP images whenever possible. Check with your CDN to see if WebP support is included in their service. You may have an easy solution just waiting for you.

自动CDN转换为WebP

一些CDNs支持自动转换到WebP，并可以使用客户端提示，随时提供WebP图像。
检查您的CDN，看看他们的服务中是否包含WebP支持。
你可能有一个简单的解决方案在等着你。

WordPress WebP support

Jetpack — Jetpack, a popular WordPress plugin, includes a CDN image service called Photon. With Photon you get seamless WebP image support. The Photon CDN is included in Jetpack's free level, so this is a good value and a hands-off implementation. The drawback is that Photon resizes your image, puts a query string in your URL and there is an extra DNS lookup required for each image.

WordPress WebP支持

Jetpack - Jetpack是一个非常流行的WordPress插件，包括一个名为光子的CDN图像服务。
光子，你得到无缝的WebP图像支持。
光子CDN包含在Jetpack的空闲级别中，因此这是一个很好的价值和不干涉实现。
缺点是光子会调整图像大小，在URL中放入查询字符串，并且每个图像都需要额外的DNS查找。

Cache Enabler and Optimizer — If you are using WordPress, there is at least one halfway-open source option. The open source plugin Cache Enabler has a menu checkbox option for caching WebP images to be served if available and the current user’s browser supports them. This makes serving WebP images easy. There is a drawback: Cache Enabler requires the use of a sister program called Optimizer, which has an annual fee. This seems out of character for a genuinely open source solution.

缓存启用器和优化器——如果你使用WordPress，至少有一个半开源的选项。
开源插件缓存启用程序有一个菜单复选框选项，用于缓存可用的WebP图像，当前用户的浏览器支持它们。
这使得提供WebP图像变得容易。
有一个缺点:缓存启用程序需要使用名为Optimizer的姊妹程序，这需要每年付费。
对于真正的开源解决方案来说，这似乎不符合其特性。

Short Pixel — Another option for use with Cache Enabler, also at a cost, is Short Pixel. Short Pixel functions much like Optimizer, described above. You can optimize up to 100 images a month for free.
短像素-另一个与缓存启用器一起使用的选项，也是有代价的，是短像素。
短像素函数很像上面描述的优化器。
你可以每月免费优化多达100张图片。

Compressing Animated GIFs and why ``<video>`` is better
压缩动画gif和为什么``<video>``更好

Animated GIFs continue to enjoy widespread use, despite being a very limited format. Although everything from social networks to popular media sites embed animated GIFs heavily, the format was never designed for video storage or animation. In fact, the GIF89a spec notes ‘the GIF is not intended as a platform for animation’. The number of colors, number of frames and dimensions all impact animated GIF size. Switching to video offers the largest savings.
尽管动画gif格式非常有限，但它仍然得到了广泛的使用。
尽管从社交网络到流行媒体网站，所有东西都大量嵌入了动画gif，但这种格式从未设计用于视频存储或动画。
事实上，GIF89a规范指出“GIF并不是一个动画平台”。
颜色的数量，帧数和尺寸都会影响GIF动画的大小。
转换到视频提供了最大的节省。

Animated GIF vs. Video: a comparison of file sizes at ~equivalent quality for different formats.
Animated GIF vs. Video: a comparison of file sizes at ~equivalent quality for different formats.
Delivering the same file as an MP4 video can often shave 80% or more off your file-size. Not only do GIFs often waste significant bandwidth, but they take longer to load, include fewer colors and generally offer sub-part user experiences. You may have noticed animated GIFs uploaded to Twitter perform better on Twitter than on other websites. Animated GIFs on Twitter aren’t actually GIFs. To improve user experience and reduce bandwidth consumption, animated GIFs uploaded to Twitter are actually converted to video. Similarly, Imgur converts GIFs to videos on upload, silently converting it to an MP4 for you.
动画GIF与视频:不同格式的文件大小在~同等质量下的比较。
动画GIF与视频:不同格式的文件大小在~同等质量下的比较。
与MP4视频传输相同的文件通常可以减少80%或更多的文件大小。
gif不仅常常浪费大量带宽，而且加载时间更长，包含的颜色更少，而且通常提供子部分的用户体验。
你可能已经注意到上传到Twitter的动态gif在Twitter上的表现比在其他网站上要好。
Twitter上的动画gif实际上并不是gif。
为了改善用户体验和减少带宽消耗，上传到Twitter的动画gif实际上被转换成视频。
类似地，Imgur在上传时将gif图片转换成视频，并无声地将其转换成MP4格式。

Why are GIFs many times larger? Animated GIFs store each frame as a lossless GIF image – yes, lossless. The degraded quality we often experience is due to GIFs being limited to a 256-color palette. The format is often large as it doesn’t consider neighbor frames for compression, unlike video codecs like H.264. An MP4 video stores each key frame as a lossy JPEG, which discards some of the original data to achieve better compression.
为什么gif要大很多倍?
动画GIF存储每个帧作为无损GIF图像-是的，无损。
我们经常经历的质量下降是由于gif被限制为256种颜色。
与H.264等视频编解码器不同，这种格式通常比较大，因为它不考虑用于压缩的相邻帧。
MP4视频将每个关键帧存储为有损的JPEG, JPEG会丢弃一些原始数据以实现更好的压缩。

If you can switch to videos

Use ffmpeg to convert your animated GIFs (or sources) to H.264 MP4s. I use this one-liner from Rigor: ffmpeg -i animated.gif -movflags faststart -pix_fmt yuv420p -vf "scale=trunc(iw/2)2:trunc(ih/2)2" video.mp4
ImageOptim API also supports converting animated gifs to WebM/H.264 video, removing dithering from GIFs which can help video codecs compress even more.
If you must use animated GIFs

如果你可以切换到视频

使用ffmpeg将动画gif(或源文件)转换为H.264 MP4s。
我使用来自Rigor的一行代码:ffmpeg -i animated。
gif -movflags faststart -pix_fmt yuv420p -vf "scale=trunc(iw/2)2:trunc(ih/2)2" video.mp4
ImageOptim API还支持将动画gif转换为WebM/H。
264视频，消除gif的抖动，这可以帮助视频编解码器压缩更多。
如果你必须使用动画gif

Tools like Gifsicle can strip metadata, unused palette entries and minimize what changes between frames
Consider a lossy GIF encoder. The Giflossy fork of Gifsicle supports this with the —lossy flag and can shave ~60-65% off size. There’s also a nice tool based on it called Gifify. For non-animated GIFs, convert them to PNG or WebP.
For more information, checkout the Book of GIF by Rigor.

像Gifsicle这样的工具可以删除元数据、未使用的调色板条目，并最小化帧之间的更改
考虑一个有损GIF编码器。
Gifsicle的Giflossy fork支持-lossy标志，可以将尺寸缩减60-65%。
基于它还有一个很好的工具叫Gifify。
对于非动画gif，将它们转换为PNG或WebP。
更多信息，检出书的GIF严格。