---

title: mac上的二维码识别
---

{{ page.title }}
===============

微信上的一些文章有时候为了阅读方便会通过 handoff 功能发送到 mac 阅读，但是这样会碰到一个问题，就是文章的有些二维码无法识别了，所以就在考虑怎么在mac浏览器上实现二维码的识别。
一个很容易想到的方案是通过浏览器扩展比如 chrome 上的 extension 来实现识别功能。大致了解了一些，chrome 上开发扩展还是比较容易的，比如360开发者网站上有这个 [getimageinfo](http://open.chrome.360.cn/extension_dev/samples.html#646325c25f572a1d15edc73d057f821d847a4fbe) 的扩展的例子，能够实现通过右键菜单获取图片信息。

![]({{ site.img_url }}/getimageinfo.png)

那问题就归结成拿到图片信息之后如何识别图片。

在网上找方案，首选的是本地识别，倒是找到[一个](https://github.com/LazarSoft/jsqrcode)，但是文档不详细，很难用得上。那退而求其次可以用远程后台的方式来解析，也找到一个[php库](https://github.com/khanamiryan/php-qrcode-detector-decoder)，这个库看起来可用，但是恰恰对微信上的有些二维码无法识别，比如这个

![]({{ site.img_url }}/640.png)

对于这个问题，我大概调试了一下，无奈看懂逻辑需要领域知识，也没法深究。网上搜索还发现这个 php 库和上面的 js 库都是源于一个叫 zxing 的开源项目，找到几个以此为后端的在线解析网站都没法识别这张图片，怀疑是这个项目对这种特定类型的二维码支持不够。

后来网络搜索的过程中居然发现已经有人把这个工作做了，比如[这个扩展](https://chrome.google.com/webstore/detail/qrreader-beta/bfdjglobiolninfgldchakgfldifphic)，交互方式也是通过右键菜单，跟我设想的一样，那这样我的需求是基本上都解决了，最重要的是这个工具也能识别上面所述 zxing 无法识别的这个二维码，而且还是本地识别的，简直 perfect。

如果要弄清楚这个软件为什么可以识别 zxing 无法识别的二维码，可能需要研究源码或者与作者取得联系了，对这块暂时兴趣不是特别大，后面有需要研究的时候再说吧。
ps：

真是神奇，下载源码下来发现用的也是就是我之前找的那个 js 库，只是做了精简合成了一个 qrcode.min.js ，我在本地使用非精简版尝试还是识别不了。用精简版代码做实验也还是不行~

