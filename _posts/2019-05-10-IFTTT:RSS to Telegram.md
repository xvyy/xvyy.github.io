---
layout: post
title: "IFTTT: RSS to Telegram"
crawlertitle: "page title"
summary: "post description"
date: 2019-05-10 16:00:00 +0800
tags : "Ubuntu"
author: "vpromise"
categories: "tech"
---





*通过IFTTT将RSS源信息推送到Telegram，获取各种信息更新，同时通过Feed43将不支持RSS订阅的网站生成RSS订阅源，及时获取教务通知等各种信息*

---

又到月底没钱吃饭的时候了，一般这个时候就惦记着国家的低保，时不时就看看研究生院官网的通知，看看有没有发钱，这样一直打开网页看就很麻烦，就萌生了做个网站出通知就提醒的想法，也便有了以下的方案。

# 一、生成RSS源

首先的想法就是，要是研究生院网站有个[RSS](https://baike.baidu.com/item/rss/24470?fr=aladdin)订阅就好了，不过这恐怕不可能，但也不是没办法，只需要神器[feed43](https://feed43.com/)就可以了，这个网站，可以将任意网页转成RSS订阅源。

![feed43](https://upload-images.jianshu.io/upload_images/4018124-9441803ebafce1de.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

初看feed43还是很复杂的，需要懂一点html语言，还要自己改代码，看到这也许就能劝退一些人了，不过我自己弄一遍后发现，就是无脑操作，并不需要代码基础的，好了，开始吧！

## 1、原网页

打开我们想转RSS的网页，将网址复制下来，比如我的研究生院奖助学金通知的页面，网址是[http://gr.uestc.edu.cn/xuesheng/91](http://gr.uestc.edu.cn/xuesheng/91)，页面是这样的![gr 奖助学金](https://upload-images.jianshu.io/upload_images/4018124-9996e1e0bd36db2a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 2、利用Feed43生成RSS

### Step 1

好了，接下来转到[feed43](https://feed43.com/)中去，点击[`Create your first RSS feed`](https://feed43.com/feed.html?action=new)，在`Step 1`下面的地址栏内填上我们粘贴过来的连接，`Encoding`可以不用填，接下来点击`Reload`。

![step 1-1](https://upload-images.jianshu.io/upload_images/4018124-419b4ca39bbac3ad.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

点击`Reload`后，下面的`Page Source`就会出现网页的html source代码，看着确实让人头疼，但是当我们翻阅就会发现一些有意思的东西，看下面的截图就发现，我们在代码中找到了通知的信息，每条通知对应的代码好像都是一样的，仔细看的话就能发现一些规律，其中有每个通知的`链接`、`标题`和`日期`，每条通知都是以`</div></div>`结尾，接下来就很简单了。

![Step 1-2](https://upload-images.jianshu.io/upload_images/4018124-6c03b9e5d896d3d6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### Step 2

发现了通知的规律后，我们随便复制一条通知对应的代码，粘贴到`Step 2`中的框中，此时我们需要修改代码了，不用慌，无脑操作，很简单的。

![Step 2-1](https://upload-images.jianshu.io/upload_images/4018124-ffb091245aacfcfc.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

我们需要做的就是将代码中的信息提取出来，将特定的信息替换一下，将代码变成对应的rules，开始弄吧，对于代码中的特定信息`链接`、`标题`和`日期`全部替换为`{%}`，然后在每行后面添加`{*}`，是不是很简单，操作完成后，代码就变成下面这样了。

![Step 2-2](https://upload-images.jianshu.io/upload_images/4018124-ee9fd8162b1663c3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

点击`Extract`，就能看到令人兴奋的事情了，我们看到在下面的框中出现了多条`Item`，每条Item都对应着一条通知信息，其中`{%1}`=`链接`， `{%2}`=`标题`， `{%3}`=`日期`，记住这个对应关系。

![Step 2-3](https://upload-images.jianshu.io/upload_images/4018124-f981174017ca5cd4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### Step 3

接下来到了`Step 3`，`Feed Title` 、`Feed Link` 和 `Feed Description`都自动填好了，你也可以自己修改，但是`Feed Link` 不要去修改它。再看下面，`Item Title Template`填上标题对应的`{%2}`，`Item Link Template`填上链接对应的`{%1}`，至于`Item Content Template`我的代码里并没有通知的具体内容，所以就不填，完成后如下。 

![Step 3-1](https://upload-images.jianshu.io/upload_images/4018124-4f404ee8fdb4e855.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

离完成不远了，我们点击`Preview`来预览，如下，还可以，通知都弄好了，是不是满满的成就感！

![Step 3-2](https://upload-images.jianshu.io/upload_images/4018124-38cac0940764064e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

最后，就得到了我们`Feed URL`的地址了，当然，为了美观，我们可以自己修改我们地址的名字，点击下面的`Change file name`，由于我的是研究生院奖助学金的通知，我就将名字改成了`gr_finance`，至此，完成了RSS源的制作了，也得到了`Feed URL`=`https://feed43.com/gr_finance.xml`。

![Step 3-3](https://upload-images.jianshu.io/upload_images/4018124-a17e493fecd132f7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

# 二、IFTTT通知
在IFTTT中的操作就很简单了，我弄的是RSS到Telegram的通知，操作就很简单了，在`Feed URL`中贴上我们的RSS链接地址`https://feed43.com/gr_finance.xml`，在`Message text`中添加我们需要的信息即可。
IFTTT也可选接收信息提醒，这样RSS源消息有更新，IFTTT和Telegram都会收到通知

![if rss then telegram](https://upload-images.jianshu.io/upload_images/4018124-784a20ae6ccf4b5a.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

具体的通知效果如下，由于之前的通知没了，就贴上我做的学院的通知信息。

![notice of SMEE](https://upload-images.jianshu.io/upload_images/4018124-73349d8a6788342e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

# 三、RSS
## 1.RSSHub
[RSSHub](https://docs.rsshub.app/) 是一个轻量、易于扩展的 RSS 生成器, 可以给任何奇奇怪怪的内容生成 RSS 订阅源
RSSHub给我们提供了很多RSS订阅源，我们可以去网站上找自己需要的，例如我就用RSSHub提供的订阅源推送bilibili up主更新
## 2.官方RSS源
很多新闻类网站都提供了RSS源，例如我就订阅了少数派的RSS[https://sspai.com/feed](https://sspai.com/feed)，其他的源网站可以自己找找看

---
```
> update at 20190509_1637
```
