## SVG 优化
Keeping SVGs lean means stripping out anything unnecessary. SVG files created with editors usually contain a large quantity of redundant information (metadata, comments, hidden layers and so forth). This content can often be safely removed or converted to a more minimal form without impacting the final SVG that’s being rendered.
SVG优化
保持SVGs精简意味着去掉任何不必要的东西。
使用编辑器创建的SVG文件通常包含大量冗余信息(元数据、注释、隐藏层等)。
这些内容通常可以安全地删除或转换为更小的形式，而不会影响最终呈现的SVG。

svgo
SVGOMG, by Jake Archibald, is a GUI interface enabling you to optimize your SVGs to your preference by selecting optimizations, with a live preview of the outputted markup
Some general rules for SVG optimization (SVGO):

svgo
SVGOMG由Jake Archibald编写，它是一个GUI界面，通过选择optimizations，您可以通过输出标记的实时预览，将SVGs优化到您的首选项
SVG优化(SVGO)的一些一般规则:

Minify and gzip your SVG files. SVGs are really just text assets expressed in XML, like CSS, HTML and JavaScript, and should be minified and gzipped to improve performance.
缩小和压缩SVG文件。
SVGs实际上只是用XML表示的文本资产，如CSS、HTML和JavaScript，应该进行压缩和gzip，以提高性能。

Instead of paths, use predefined SVG shapes like <rect>, <circle>, <ellipse>, <line> and <polygon>. Preferring predefined shapes decreases how much markup is needed to produce a final image, meaning less code to parse and rasterize by the browser. Reducing SVG complexity means a browser can display it more quickly.
If you must use paths, try to reduce your curves and paths. Simplify and combine them where you can. Illustrator’s simplify tool is adept at removing superfluous points in even complex artwork while smoothing out irregularities.
Avoid using groups. If you can’t, try to simplify them.
使用预定义的SVG形状代替路径，如<rect>、<circle>、<ellipse>、<line>和<polygon>。
选择预定义的形状可以减少生成最终图像所需的标记，这意味着浏览器解析和光栅化的代码更少。
降低SVG的复杂性意味着浏览器可以更快地显示它。
如果你必须使用路径，尽量减少你的曲线和路径。
尽可能地简化和组合它们。
Illustrator的简化工具擅长去除多余的点，即使是复杂的艺术品，同时消除不规则。
避免使用组。
如果不能，试着简化它们。

Delete layers that are invisible.
Avoid any Photoshop or Illustrator effects. They can get converted to large raster images.
Double check for any embedded raster images that aren’t SVG-friendly
Use a tool to optimize your SVGs. SVGOMG is a super handy web-based GUI for SVGO by Jake Archibald that I’ve found invaluable. If you use Sketch, the Sketch plugin for running SVGO can be used when exporting to shrink the file size.
svgo precision reduction can sometimes have a positive impact on size
An example of running an SVG source through SVGO in high-precision mode (leading to a 29% improvement in size) vs. low-precision mode (a 38% size improvement).
SVGO is a Node-based tool for optimizing SVG. SVGO can reduce file-size by lowering the precision of numbers in yourdefinitions. Each digit after a point adds a byte and this is why changing the precision (number of digits) can heavily influence file size. Be very very careful with changing precision however as it can visually impact how your shapes look.

删除不可见的层。
避免任何Photoshop或Illustrator效果。
它们可以转换成大光栅图像。
仔细检查任何不支持svg的嵌入式光栅图像
使用工具优化您的SVGs。
SVGOMG是一个非常方便的基于web的GUI，由Jake Archibald为SVGO开发，我发现它非常有价值。
如果使用Sketch，可以在导出文件时使用运行SVGO的Sketch插件来缩小文件大小。
svgo精度的降低有时会对尺寸产生积极的影响
通过SVGO以高精度模式(导致大小改进29%)运行SVG源与以低精度模式(大小改进38%)运行SVG源的示例。
SVGO是一种基于节点的SVG优化工具。
SVGO可以通过降低定义中数字的精度来减少文件大小。
一个点之后的每一位数字都会增加一个字节，这就是为什么改变精度(位数)会严重影响文件大小的原因。
但是，要非常非常小心地更改精度，因为它会在视觉上影响形状的外观。

where svgo can go wrong, oversimplifying paths and artwork
It’s important to note that while SVGO does well in the previous example without over-simplifying paths and shapes, there are plenty of cases where this may not be the case. Observe how the light strip on the above rocket is distorted at a lower precision.
Using SVGO at the command-line:

svgo哪里会出错，过度简化路径和艺术品
需要注意的是，虽然SVGO在前面的示例中没有过度简化路径和形状，但在很多情况下可能不是这样。
观察上面火箭上的光带是如何以较低的精度扭曲的。
在命令行使用SVGO:

SVGO can be installed as a global npm CLI should you prefer that to a GUI:
SVGO可以安装为一个全球npm CLI，如果你喜欢它比GUI:

npm i -g svgo
This can then be run against a local SVG file as follows:
然后可以对一个本地SVG文件运行如下操作:

svgo input.svg -o output.svg
It supports all the options you might expect, including adjusting floating point precision:
它支持您可能期望的所有选项，包括调整浮点精度:

svgo input.svg --precision=1 -o output.svg
See the SVGO readme for the full list of supported options.
有关支持的选项的完整列表，请参见SVGO自述文件。

Don’t forget to compress SVGs!
不要忘记压缩SVGs!

before and after running an image through svgo
Also, don’t forget to Gzip your SVG assets or serve them using Brotli. As they’re text based, they’ll compress really well (~50% of the original sources).
在通过svgo运行映像之前和之后
另外，不要忘记Gzip SVG资产或使用Brotli提供它们。
由于它们是基于文本的，所以可以很好地压缩(大约50%的原始源代码)。

When Google shipped a new logo, we announced that the smallest version of it was only 305 bytes in size.
当谷歌发布一个新徽标时，我们宣布最小的版本只有305字节。

the smallest version of the new google logo was only 305 bytes in size
There are lots of advanced SVG tricks you can use to trim this down even further (all the way to 146 bytes)! Suffice to say, whether it’s through tools or manual clean-up, there’s probably a little more you can shave off your SVGs.
新谷歌徽标的最小版本只有305字节大小
您可以使用许多高级SVG技巧将其进一步缩减(一直到146字节)!
我只想说，无论是通过工具还是手动清理，您都可以删除更多的SVGs。

SVG Sprites
SVG精灵

SVG can be powerful for icons, offering a way to represent visualizations as a sprite without the quirky workarounds needed for icon fonts. It has more granular CSS styling control than icon fonts (SVG stroke properties), better positioning control (no need to hack around pseudo-elements and CSS display) and SVGs are much more accessible.
SVG可以为图标提供强大的功能，它提供了一种将可视化表示为精灵的方法，而不需要为图标字体提供奇怪的变通方法。
它具有比图标字体(SVG笔画属性)更细粒度的CSS样式控制、更好的定位控制(不需要修改伪元素和CSS显示)和SVGs更容易访问。

Tools like svg-sprite and IcoMoon can automate combining SVGs into sprites which can be used via a CSS Sprite, Symbol Sprite or Stacked Sprite. Una Kravetz has a practical write-up on how to use gulp-svg-sprite for an SVG sprite workflow worth checking out. Sara Soudein also covers making the transition from icon fonts to SVG on her blog.
像svg-sprite和IcoMoon这样的工具可以自动将SVGs组合成可以通过CSS Sprite、符号Sprite或堆栈Sprite使用的Sprite。
Una Kravetz写了一篇关于如何将gulp-svg-sprite用于SVG sprite工作流的实用文章，值得一看。
Sara Soudein还在她的博客中介绍了从图标字体到SVG的转换。

Further reading
进一步的阅读

Sara Soueidan’s tips for optimising SVG delivery for the web and Chris Coyier’s Practical SVG book are excellent. I’ve also found Andreas Larsen’s optimizing SVG posts enlightening (part 1,part 2).Preparing and exporting SVG icons in Sketch was also a great read.
Sara Soueidan为web优化SVG交付的技巧和Chris Coyier的实用SVG书籍都非常优秀。
我还发现Andreas Larsen的SVG优化文章很有启发(第1部分和第2部分)。