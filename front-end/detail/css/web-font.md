# web-font
浏览器要渲染使用了 Web 字体的文本，就必须从互联网下载字体。由于网络的不确定性，如果下载字体花费的时间非常久，浏览器该如何处理？
实际上，浏览器能使用的策略并不多，无外乎以下几种：
* 先使用系统默认字体渲染文本；等 Web 字体下载完，使用新字体再渲染一次；
* 等到 Web 字体下载完成，才渲染文本。也就是字体下载完全阻塞对应文本渲染
* 先跳过文本的渲染；一段时间后，如果 Web 字体仍未下载完，使用系统默认字体渲染文本；等字体下载完，再次渲染；

方案 1 的好处是用户可以第一时间看到文本内容，坏处是：两种字体之间的差异，一定会造成内容抖动。早期的 Firefox 以及现阶段所有 IE 都是采用的这种方案。    

方案 2 的好处是完全避免了内容抖动，坏处也很明显：字体下载需要多久，用户就有多久完全看不到文本内容。现阶段基于 Webkit 内核的浏览器，如 Chrome 和 Safari 都是如此。    

方案 3 则是一个折中方案，如果 Web 字体能在一段时间内加载完，不会有因为字体变换带来的抖动；同时如果加载字体需要很久，也不至于不显示文本。现阶段 Firefox 采用的这种方案。Firefox 默认等 3 秒，可以找到 about:config 中的 gfx.downloadable_fonts.fallback_delay 配置来修改。

转自 https://www.imququ.com/post/chrome_and_web_fonts.html

ps：谷歌字体被墙，解决方案是，用360提供的[cdn](http://libs.useso.com/)