---
title: 网站地图
date: 2020-01-06 18:00:00
categories: 
- SEO
tags:
- SEO
---

### XML网站地图

在搜索引擎爬虫进行信息采集的过程中，我们的页面应尽可能主动提交友好的页面的链接。 



### 一、XML网站地图中的priority标签是什么意思？

网站地图中的priority表达的是该页面的优先级，范围是0~1.0之间，一般默认为0.5，1.0表示页面非常重要。



### 二、XML网站地图示例讲解

小小课堂SEO自学网的部分XML网站地图如下：

```
<?xml version=”1.0″ encoding=”UTF-8″?><!--声明xml格式-->
<urlset xmlns="http://www.google.com/schemas/sitemap/0.84"><!--sitemap协议版本-->
<loc>https://www.xxkt.org/11921</loc>
<lastmod>2018-011-15T09:23:34+00:00</lastmod>
<changefreq>hourly</changefreq>
<priority>0.7</priority>
<image:image>
	<image:loc>https://www.xxkt.org/wp-content/uploads/2018/03/11-6.jpg</image:loc>
	<image:title><![CDATA[11]]></image:title>
</image:image>
</url>
<urlset>
```

**① 页面重要性**

<priority>0.7</priority>

**② 编码为UTF-8和XML版本声明**

<?xml version=”1.0″ encoding=”UTF-8″?>

**③ sitemap版本声明**

<urlset xmlns=”http://www.sitemaps.org/schemas/sitemap/0.9”</urlset>

**④ 最后一次更新时间**

<lastmod>2018-011-15T09:23:34+00:00</lastmod>

**⑤ 页面的URL**

<loc>https://www.xxkt.org/11921 </loc>

**⑥ 更新频率可以是一直更新，也可以是每小时更新，还可以是每个星期、月、年和从不更新。**

<changefreq>hourly</changefreq>



### 三、XML网站地图的作用

马慧SEO认为XML网站地图有以下几点作用：

**① 告知网络爬虫页面优先级**

通过<priority>表达页面的重要性，网络爬虫一般会先爬行重要的页面，一些WordPress可以设置这个选项。

![img](http://5b0988e595225.cdn.sohucs.com/images/20181115/be837b0e43b347a39a75e692315b258e.jpeg)

**② 告诉网络爬虫页面链接**

网络爬虫通过网站地图即可提取网站新生产的页面，而不用费力去爬行。

**③ 告诉网络爬虫页面更新时间**

比如有一些页面最近更新了，网络爬虫会去重新爬行并更新这些页面的快照信息。同时，有助于减少网络爬虫的工作量，当然这就是针对搜索引擎系统而言了。





### 网站地图

又称站点地图，它就是一个页面，上面放置了网站上需要搜索引擎抓取的所有页面的链接（注：不是所有页面）。大多数人在网站上找不到自己所需要的信息时，可能会将网站地图作为一种补救措施。搜索引擎蜘蛛非常喜欢网站地图。

  二、分类

  主要有两种，一是给用户看的：html----方便用户找到他想要的信息，二是给搜索引擎看的：xml-----加快搜索引擎的收录速度

  三、注意事项

![网站地图](http://www.seokuaipai.cn/uploads/allimg/190702/1-1ZF21H34RO.jpg)

  首先是新站没有什么内容，不需要做.，还有就是避免产生死链接，http状态返回码404，最后就是软件和在线生成注意不要其他什么文件

  

### 四、网站地图的制作

  （一）在线生成

  打开浏览器百度搜索网站地图在线生成 出来后再点击sitmap网站地图生成工具xml，然后把自己的域名链接输入http：//框，这里注意一点，如果自己域名是，那么点,如果是https：// 那么下拉点https：//，域名后面的怎么看呢 单击右键点自己网站查看源代码，找到最上面，如果是utf-8格式，那么就选utf-8，然后百度sitemap选项里点pc，基本设置里一般更新频率为一周，优先级，自动，内链，锚过滤，忽视sitemap，html 都打上勾。模拟来源设置为“你的域名“，然后生成抓取，再下载到本地桌面已方面后面的操作。注意：如果生成不了，那么就换个其他的生成器工具，直到生成成功。

  （二）软件生成

下载sitemap X软件，安装好后打开 建立分组输入工程名称，然后把网站网址复制输入，开始抓取是5层，时间最大的，再点击下一步，格式只需要第一个 后面三个都不需要，下面那些不需要管 修改频率可以调为一周，然后下一步 ，下一步，把“是否上传robots.txt”文件前面的勾去掉，再下一步，直接抓取，如果只能抓取http，那么把s去掉再点抓取。抓取完成后点击生成xml文件，再打开文件目录，把下载的文件复制到桌面右键用代码源打开可查看是否成功.

  （三）插件

  用插件相对来讲比较简单一点，更新也是后台自动更新，而在线生成和软件生成要手动更新比较麻烦一点。直接进入网站后台下载系统xml地图自动生成插件文件，比如织梦xml，百度xmap等等。如百度的 ，辅助插件里 随选，标签前勾去掉，然后生成。如果插件管理器里没有就在模块管理里上传新模块，如果已经压缩了就选zip模块包，然后选择文件，utf-8的 ，然后确认再点安装点确认，安装好后会出现在辅助插件里，如果没有就去dede官网后台下载个同编码的把dede换掉就可以了或重命名。

最后最关键的操作就是去各站长提交，比如百度站长平台 ，360 搜狐等等，比如百度站长工具里点用户中心再站点管理，再点击自己的网站，然后有个链接提交，下面有个自动提交那里点击sitemap地图提交。数据文件地址就是：自己的域名/+地图地址sitsmap.xml然后点击提交就完成了。



### 网站地图制作提交步骤

1、生成网站地图：

 网页版：http://www.xml-sitemaps.com/

 客户端：http://cn.sitemapx.com/

2、下载生成的地图文件sitemap.xml并上传至网站根目录

3、到站长平台提交网站地图。

**生成网站地图：http://www.xml-sitemaps.com/**

change frequency:指的是频率，地图的自动更新频率，默认每天(daily);

last modification:是网站地图最后修改时间，默认使用服务器的响应(Use server's response);

priority:权重-可自动计算。

点击start开始生产。自动跳转到生成页面，稍等一段时间便可生成（时间和网站内容多少有关）。

它提供多种格式的网站地图文件下载(xml、xml.gz、ror.xml、html等)，看你所提交的搜索引擎需要哪种格式的地图文件，就下载哪一个，或者直接打包全下载。

**各搜索引擎推荐网站地图格式：**

Google：建议使用xml格式的网站地图

地图提交地址：https://www.google.com/webmasters/tools/dashboard?hl=zh-CN

Yahoo： 建议使用Txt格式的网站地图

Yahoo地图提交地址 ：http://sitemap.cn.yahoo.com/?require_login=1

Baidu:建议使用robots.txt提交html格式的网站地图

http://www.baidu.com/search/url_submit.html

在robots.txt爬虫协议中定义（Allow: /sitemap.hxml）robots.txt文档是表式允许蜘蛛网访问网站地图。



语法很简单。其中priority是指相对于其他页面的优先权，changefreq则是指内容更新的频率。有了这些设置，就等于告诉搜索引擎机器人，你的网站的更新情况如何，以及希望搜索引擎优先收录哪些内容。



### 格式说明

#### 1、首尾格式

如下：

```
<?xml version="1.0"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
```

这两句代码类似Html标签是死的。照抄即可。文件最后会有</urlset>

#### 2、<loc></loc>

这两个标签中间的地址必填。格式为:http://www.tekuba.net/share，此网址应以协议开始（例如：http）并以斜线结尾。此值应少于 2048 个字符。

#### 3、<lastmod>

可选标签 标签含义:该文件上次修改的日期。此日期应采用 W3C Datetime 格式。如果需要的话，此格式允许省略时间部分，而仅使用 YYYY-MM-DD。 列子：2014-07-16。

一 般来说这个很重要。Google的机器人会在索引此链接前先和上次索引记录的最后更新时间进行 比较，如果时间一样就会跳过不再索引。所以如果你的链接内容基于上次Google索引时的内容有所改变，应该更新该时间，让Google下次索引时会重新 对该链接内容进行分析和提取关键字。

#### 4、<changefreq>

可选标签 标签含义:页面可能发生更改的频率。此值为搜索引擎提供一般性信息，可能与搜索引擎抓取页面的频率不完全相关。有效值为：

```
always 
hourly 
daily 
weekly 
monthly 
yearly 
never
```

值“always”应当用于描述每次访问时都会改变的文档。而值“never”应当用于描述已存档网址。

#### 5、<priority>

可 选标签 此网址的优先级与您网站上其他网址的优先级相关。有效值范围从 0.0 到 1.0。此值不会影响您的网页与其他网站上网页的比较结果，只是告诉搜索引擎您认为您的那个网页最重要，从而它们对您页面的抓取可以按照您最喜欢的方式进 行排序。一个网页的默认优先级为 0.6。

xml文件必须是utf-8的编码格式，可以用记事本打开xml然后另存为时选择编码(或转换器)为UTF-8。了解这些标签的作用我们就可以根据自己网站的情况做出适合自己站点sitemap.xml。

通过以上的知识我们可以知道：如果要想添加问说网（http://www.uedsc.com）的站点地图的话，值需要增加如下代码即可：

```
<url>
    <loc>http://www.uedsc.com/tag/2d\\%e5\\%8f\\%98\\%e6\\%8d\\%a2</loc>
    <lastmod>2015-03-12T18:31:43+00:00</lastmod>
    <changefreq>weekly</changefreq>
    <priority>0.3</priority>
</url>
```



### 提交Sitemap.xml

Sitemap.xml制作完成后，就需要将xml文件提交到相关搜索引擎。

Google提交网址：http://www.google.com/webmasters/sitemaps/?hl=zh-CN
Yahoo提交网址：http://sitemap.cn.yahoo.com/

提交后，一般在几个小时之内，系统就开始下载处理了。



### Google SiteMap

Google SiteMap Protocol是Google自己推出的一种站点地图协议，此协议文件基于早期的robots.txt文件协议，并有所升级。在Google官方指南中指出加入了Google SiteMap文件的网站将更有利于Google网页爬行机器人的爬行索引，这样将提高索引网站内容的效率和准确度。文件协议应用了简单的XML格式，一共用到6个标签，其中关键标签包括链接地址、更新时间、更新频率和索引优先权。

```
<urlset xmlns="网页列表地址">

<url>

<loc>网址</loc>

<lastmod>2005-06-03T04:20-08:00</lastmod>

<changefreq>always</changefreq>

<priority>1.0</priority>

</url>

<url>

<loc>网址</loc>

<lastmod>2005-06-02T20:20:36Z</lastmod>

<changefreq>daily</changefreq>

<priority>0.8</priority>

</url>

</urlset>
```



### 百度sitemap

```
<?xml version="1.0" encoding="UTF-8"?>

<urlset>

<url>

<loc>网页地址</loc>

<lastmod>2010-01-01</lastmod>

<changefreq>daily</changefreq>

<priority>1.0</priority>

</url>

</urlset>
```



### XML标签

changefreq：页面内容更新频率。

lastmod：页面最后修改时间

loc：页面永久链接地址

priority：相对于其他页面的优先权

url：相对于前4个标签的父标签

urlset：相对于前5个标签的父标签

我将一句一句分解讲解这个xml文件的每一个标签：

<urlset xmlns="

这一行定义了此xml文件的命名空间，相当于网页文件中的<html>标签一样的作用。

****

这是具体某一个链接的定义入口，你所希望展示在SiteMap文件中的每一个链接都要用<url>和</url>包含在里面，这是必须的。

****

用<loc>描述出具体的链接地址，这里需要注意的是链接地址中的一些特殊字符必须转换为XML(HTML)定义的转义字符，如下表：字符 转义后的字符

HTML字符 字符编码

& 符号 & &amp；

单引号 ' &apos；

双引号 " "

大于 > &gt；

小于 < &lt；

**2005-06-03T04:20:32-08:00**

<lastmod>是用来指定该链接的最后更新时间，这个很重要。Google的机器人会在索引此链接前先和上次索引记录的最后更新时间进行比较，如果时间一样就会跳过不再索引。所以如果你的链接内容基于上次Google索引时的内容有所改变，应该更新该时间，让Google下次索引时会重新对该链接内容进行分析和提取关键字。这里必须用[ISO 8601](https://baike.baidu.com/item/ISO 8601)中指定的时间格式进行描述，格式化的时间格式如下：

年：YYYY(2005)

年和月：YYYY-MM(2005-06)

年月日：YYYY-MM-DD(2005-06-04)

年月日小时分钟：YYYY-MM-DDThh:mmTZD(2005-06-04T10:37+08:00)

年月日小时分钟秒：YYYY-MM-DDThh:mmTZD(2005-06-04T10:37:30+08:00)

这里需注意的是TZD，TZD指定就是本地时间区域标记，像中国就是+08:00了

**always**

用这个标签告诉Google此链接可能会出现的更新频率，比如首页肯定就要用always(经常)，而对于很久前的链接或者不再更新内容的链接就可以用yearly(每年)。这里可以用来描述的单词共这几个："always"、 "hourly"、 "daily"、 "weekly"、 "monthly"、 "yearly"、 "never"，具体含义我就不用解释了吧，光看单词的意思就明白了。

**1.0**

<priority>是用来指定此链接相对于其他链接的优先权比值，此值定于0.0 - 1.0之间

还有</url>和</urlset>，这两个就是来关闭xml标签的，这和HTML中的</body>和</html>是一个道理。

另外需要注意的是，这个xml文件必须是utf-8的编码格式，不管你是手动生成还是通过代码生成，建议最好检查一下xml文件是否是utf-8编码，最简单的方法就是用记事本打开xml然后另存为时选择编码(或转换器)为UTF-8。

登陆Google提交你的SiteMap文件，链接，如果还没有注册或者登陆Google，就先用自己的帐号登陆Google，登陆后转到Your Sitemaps状态页面，可以点击那个Add a Sitemap + 跳转到提交页面进行Sitemap文件的提交。建议文件放在你的站点[根目录](https://baike.baidu.com/item/根目录)下。给Google提交你的Sitemap URL后可以看见在列表里已存在，不过这时候还没有生效，必须过几个小时后Status栏变成OK表示正式生效，如果不是OK，可以查看Google给出的状态标示解释看看是什么原因。



### 新手如何掌握制作和提交网站地图？

网站地图作为根据网站的结构，框架，内容生成的导航网页文件。

大多数人都知道网站地图对于[提高用户体验](https://lusongsong.com/reed/768.html)有好处：它们为网站访问者指明方向，并帮助迷失的访问者找到他们想看的页面。

**那么什么是网站地图呢?**

在开始介绍网站地图的制作与提交之前，我们有必要先了解一下什么是网站地图。

**网站地图也就是sitemap，是一个网站所有链接的容器。**很多网站的链接层次比较深，蜘蛛是很难抓取到的，网站地图可以方便搜索引擎蜘蛛抓取网站页面，通过抓取网站页面，可以清晰的了解网站的架构。网站地图一般存放在根目录下并命名为sitemap，为搜索引擎蜘蛛引路，增加网站重要内容页面的收录。

**网站地图的作用：**

1.为搜索引擎蜘蛛提供可以浏览整个网站的链接，简单的体现出网站的整体框架。

2.为搜索引擎蜘蛛提供一些链接，指向动态页面或者采用其他方法比较难以到达的页面。

3.作为一种潜在的着陆页，可以对搜索流量进行优化。

4.如果访问者试图访问网站所在域内并不存在的URL，那么这个访问者就会被转到“无法找到文件”的错误页面，而网站地图可以作为该页面的“准”内容。

**HTML版本的网站地图**

html版本的网站地图就是用户可以在网站上看到的，列出网站上所有主要页面的链接的页面。对于小型网站来说，甚至可以列出整个网站的所有的页面。而对于具有一定规模的网站来说，一个网站地图不可能罗列所有的页面链接，可以采用两种方法解决：

第一种就是网站地图只列出网站最主要的链接，如一级分类，二级分类。

第二种方法是将网站地图分成几个文件，主网站地图列出通往那次级[网站的链接](https://lusongsong.com/reed/471.html)，刺激网站地图在列出一部分页面链接。

**XML本的网站地图**

XML版本的网站地图是由goole首先提出的，怎么区分呢?上面所说的HTML版本中的sitemap首字母s是小字写的，XML版本中的S则是大写的。XML版本的网站地图是由XML标签组成的，文件本身必须UTF-8编码，网站地图文件实际上就是列出网站需要被收录的页面的URL。最简单的网站地图可以是一个纯文本文件，文件只要列出页面的URL，一行一个URL，搜索引擎就能抓取并理解文件内容。

**网站地图的制作方法**

网上有很多网站地图的生成方法，比如说在线生成，软件生成等。这里小编推荐使用小爬虫网站地图生成工具：http：//www.sitemap-xml.org。使用方法如下：

1)输入域名，选择网站对应的编码，点击“生成”按钮(建议使用搜狗浏览器或者google浏览器)如图所示：

 ![新手如何掌握制作和提交网站地图？ 免费资源 建站工具 网站运营 经验心得 第1张](https://images.lusongsong.com/zb_users/upload/2017/09/201709196348_897.jpg)

2)等待小爬虫爬行网站，爬行时间根据网站内容多少和服务器访问速度不定，如果数据较多，则建议晚上10点以后操作，

3)下载sitemap.xml或者sitemap.html文件，上传到网站根目录，在首页做链接，如图所示： 

 ![新手如何掌握制作和提交网站地图？ 免费资源 建站工具 网站运营 经验心得 第2张](https://images.lusongsong.com/zb_users/upload/2017/09/201709191351_201.jpg)

这里需要说明一下sitemap.xml和sitemap.html文件的区别：

sitemap.xml文件的创建是为了更有利于搜索引擎的抓取，从而提高工作效率，生成sitemap.xml文件后将其链接放入robort.txt文件内。提示：

良好的robort.txt协议可以指引搜索引擎抓取方向，节省蜘蛛抓取时间，所以无形中提升了蜘蛛的工作效率，也就增大了页面被抓取的可能性。

将sitemap.xml和robort.txt文件放在网站的根目录下。

sitemap.html格式的网站地图主要是用来方便用户的浏览，并不能起到XMLSitemap所起的作用。所以最好两者都要有。

4)登录[百度](https://lusongsong.com/tags/baidu.html)站长平台，点击“链接提交”，填写sitemap.xml对应的URL地址，如图所示：

![新手如何掌握制作和提交网站地图？ 免费资源 建站工具 网站运营 经验心得 第3张](https://images.lusongsong.com/zb_users/upload/2017/09/201709199879_660.jpg)

提交完后，百度[搜索引擎蜘蛛](http://bbs.lusongsong.com/forum/detail_59872/page/1.html)会对我们的网站进行抓取。大量案例证明，添加网站能加速网站内容收录速度，提升网站收录率。但是这要建立在网站内容质量符合搜索引擎标准的基础上，如果网站内容质量太差，则使用网站地图也是无济于事的。以上就是制作提交网站地图的一些分享，也是基础中的基础，希望对新手有用。