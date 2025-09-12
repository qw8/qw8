---
title: 代码优化
date: 2020-01-02 18:00:00
categories: 
- SEO
tags:
- SEO
---

### rel=nofollow"属性简介

   **nofollow**是HTML元标签(meta)的content属性和链接标签(a)的rel属性的一个值，告诉机器(爬虫)无需追踪目标页，为了对抗blogspam(博客垃圾留言信息)，Google推荐使用nofollow，告诉搜索引擎爬虫无需抓取目标页，同时告诉搜索引擎无需将的当前页的Pagerank传递到目标页。但是如果你是通过sitemap直接提交该页面，爬虫还是会爬取，这里的nofollow只是当前页对目标页的一种态度，并不代表其他页对目标页的态度。

#### **nofollow的使用**

nofollow有两种用法：
1.用于meta元标签：<meta name="robots" content="nofollow" />，告诉爬虫该页面上所有链接都无需追踪。
2.用于a标签：<a href="login.aspx" rel="nofollow">登录</a>,告诉爬虫该页面无需追踪。 

 

------

#### **nofollow的作用**

nofollow主要有三个作用：
1.防止不可信的内容，最常见的是博客上的垃圾留言与评论中为了获取外链的垃圾链接，为了防止页面指向一些拉圾页面和站点。
2.付费链接：为了防止付费链接影响Google的搜索结果排名，Google建议使用nofollow属性。
3.引导爬虫抓取有效的页面：避免爬虫抓取一些无意义的页面，影响爬虫抓取的效率。

 

------

#### **PR修剪(Pagerank Sculpting)**

nofollow的滥用，一些SEO为了做到搜索引擎的最大优化，通过nofollow来控制PR的流动，可以很好的优化一些特定页面。当然这种优化比较适合一些已经积淀了相当数量PR的老站点。为了防止PR修剪和nofollow的滥用，Google已经减弱了nofollow的作用，以前的nofollow不仅仅不会造成PR流动，同时不会造成PR损失，现在的nofollow规定虽然也不会造成PR流向目标页，但是原本流向的目标页的将会损失掉。比方当前页PR为1，而且页面上有10个链接，其中一个是nofollow的链接，根据先前的nofollow的规定，每个非nofollow链接指向的目标页将获得1/9的PR，含nofollow的链接不能获得PR，而根据现在Google对nofollow的新规定，非nofollow链接指向的目标页只能获得1/10，nofollow链接同样不能获得PR，也就是损失了1/10的PR。

 

------

#### SEO建议

   nofollow在Google的作用已经很弱，所以SEO要控制站点的PR的流动，避免链接指向垃圾页面，只能靠人工审核的方法。



近年来在网站的链接中我们经常会看到类似**rel=”nofollow”**或**rel=”external nofollow”**的属性定义，有很多朋友并不明白它们的语义，今天园子就详细给大家分析一下rel 这个属性在网页中的用法。

rel 属性是用来说明**链接和包含此链接页面的关系，以及链接打开的目标**。它有许多的属性值，比如next、previous,、chapter、section等等。我们现在比较长见的是rel=”external nofollow”与rel=”nofollow”两种参数的应用。

#### 首先来说下Nofollow

“Nofollow”向网站管理员提供了一种方式，即告诉搜索引擎”**不要追踪此网页上的链接”**或”**不要追踪此特定链接**“。 最初，nofollow 属性出现在网页级元标记中，指示搜索引擎不要追踪（即抓取）网页上的所有外向链接。 例如：

```html
<meta name="robots" content="nofollow" />
```

或者您可以这样用：

```html
<a href="signin.php" rel="nofollow">用户注册</a>
```

#### 再来说说external nofollow

rel=”external nofollow”只是更相对于rel=”nofollow”参数更加规范一些。rel=”external nofollow”与rel=”nofollow”其功能就中文译文”**不要读取**” 及”**外部链接不要读取**“,就已说得很清楚了。其实rel=”external”只是一个替代target=”_blank” 的属性。target=”_blank” 的属性是打开新窗口。但有些博客因为是采用严格的DOCTYPE声名的，如果你打开网站的源代码，在第一行的位置就可以看到：

```html
< !DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
```

在这种情况下target=”_blank”可能会失效，因此采用rel=”external”这个参数来替代，因此我们可以明白rel=”external”的属性只是打开新窗口的作用。

通过上面的说明您应该明白在何种情况下可以考虑使用nofollow了吧？以下列出经常用到nofollow的几种情况：

- 不可信赖的内容

- 付费链接

- 按优先级别进行抓取

  

> 对于网站SEO优化的人来说，rel=”nofollow”大家都不太陌生，特别是很多站长在和其他网站进行友情链接的交换的时候，其中重要的一项指标就是友情链接不能带有nofollow。不过仍然有一些新手站长对此并不太了解，下面就让我们一起来看看什么是nofollow，以及使用nofollow有哪些好处。

------

## 什么是nofollow?

> nofollow是一个HTML标签的属性值，随着搜索引擎优化(SEO)的兴起，它渐渐被大家所了解，这个标签的意思是告诉搜索引擎不要此网页上的链接或不要追踪此特定链接。如果A网页上有一个链接指向B网页，但A网页给这个链接加上了 
> rel=”nofollow” 标注，则搜索引擎不把A网页计算入B网页的反向链接。搜索引擎看到这个标签就可能减少或完全取消链接的投票权重。

------

> 它最早出现在网页级元标记也就是head头部文件，用于指示搜索引擎不要追踪(即抓取)网页上的任何出站链接，常见写法为

```
<meta name="robots” content="nofollow” />1
```

目前，起主要放在标签中，常见的写法比如为

```
<a href=”http://www.baidu.com” target=”_blank” rel=”nofollow”>百度</a> 1
```

------

***使用nofollow有哪些好处呢?现在大家对于网站优化越来越认可，通过使用nofollow可以精确的定位到指定的链接。目前其主要的用途主要有如下三点：\***

## 1、屏蔽付费链接

现在很多站长都会在自己的网站上投放广告，常见的比如百度推广联盟，淘宝广告联盟，google广告等等， 
通过对这些链接使用nofollow，可以告诉搜索引擎，不用将网站的权重传递到这些网站，特别是一些较为大型的网站来说，在挂广告的时候一定要注意使用nofollow标签，来阻止权重的传递和广告的内容质量的控制。

## 2、不可信赖的用户来制造的垃圾内容、评论或留言：

　　现在很多博客评论功能是使用Nofollow属性的，可以很好的控制“恶邻”使用群发留言来提高PR值和定位文字。大型的门户网站网易博客为了降低内容和链接对用户的影响。

## 3、按优先级别进行抓取

　　![这里写图片描述](https://img-blog.csdn.net/20180704112910982?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMzOTgxNDM4/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

　网站上面有登陆和注册页面，搜索引擎不可能和人一样能登陆或者注册到我们的网站 ，因此没有理由邀请搜索引擎追踪”在此注册”或”登录”链接。或者一些链接，站长不希望网站传递权重，都可以使用nofollow进行控制，如上图所示。 
　　通过上面的结束，我们相信了解了nofollow的含义，使用方法以及用途，如果大家对网站推广优化还想了解更多，欢迎关注百易互通的更多内容。



### meta name="location" 标签的使用

本地化的业务，所以对于移动站点的优化就可以很好的利用这一点来提升网站在当地网站的一个排名优势。

这对于做区域性移动站点有较为好的优化效果， 为了方便用户根据自身位置查找或使用本地信息与服务，百度移动搜索会根据用户地理位置信息优先将具有地域属性的内容展现给用户，如果是提供地域性信息服务的站点，可以通过为自己网页添加地理位置信息 Meta 标注，让目标用户在百度移动搜索中更快的找到您网站的内容。

在进行一些操作的时候，我们可能会用到这个标签来什么，地理位置，不错的网站优化标签。

```
<meta name="location" content="province=山西;city=吕梁;coord=111.14426,37.495347">
```

具体的定位信息可以，在百度的API中找到：

```
http://api.map.baidu.com/lbsapi/getpoint/index.html
```

作用：定位当前的位置，便于百度移动搜索。非常不错。



### 百度移动搜索地域优化服务说明

为方便用户根据自身位置查找和使用本地信息与服务，帮助移动站点健康、稳定地提升流量，百度移动搜索现提供地域优化服务。

如果您是提供线下信息服务的站点，可以通过为自己的网页添加地理位置信息的方式，让您的站点所在地的用户更快在找到您。

具体方法很简单，您只需在具有地域性的页面上进行如下标识即可。

a）Meta声明格式为：

Name属性的值是location。Content的值为province=北京;city=北京;coord=116.306522891,40.0555055968。



**province**为省份简称，**city**为城市简称。具体参见下面省份和城市列表。

**coord**是页面信息的经纬度坐标，采用的是**bd09ll**坐标。若页面信息为城市级别，填写城市中心点即可。若页面信息有具体的地址，经纬度坐标填写该具体地址的坐标（可以通过百度地图的地址解析 API获取）。

注：province及city不可为空。

b）站长需要将Meta声明放在网页源代码标签内部，如下：

<head>

     <meta name="location" content="province=北京北京116.306522891,40.0555055968

**常见问题**

Q1：是不是PC站和移动站都要标？

A：首先，地域标签主要应用于移动搜索。而移动搜索检索机制支持用户搜索到PC站或移动站，所以PC站和移动站都需要标记。

Q2：标了这个有什么好处？

A：从百度用户的搜索行为可以看到，大量的用户对于本地或者附近的结果更有倾向性。站长配合进行地域信息标注后，我们将根据页面的地域信息和用户所在位置进行匹配，优先展示距离近的结果。也就是说，您的站点将更有机会被当地用户看到。

Q3：经纬度可以为空吗？

A：可以为空。如果没有经纬度，可以是<meta name="location" content="province=北京;city=北京">

Q4：我们的站点更多是外地用户在搜索，打了标签后会不会有问题？

A：不会出现问题。百度移动搜索会通过精准的需求识别，对“外地搜索”行为做特殊策略，不会影响到搜索异地结果。同时，站长还是需要注意只对页面内容或服务本身具有较强地域属性的页面进行地域信息标注。

Q5：这个移动搜索的地域优化标签做好后，是否需要单独提交？

A：没有标记经纬度的话不需要单独提交。如果页面更新了，可以到站长平台提交sitemap，加速百度收录的速度。

**附录：省份与城市列表**![img](https://zhanzhang.bj.bcebos.com/files/000941413169203.png)



### 链接a标签中title属性是否有利于SEO

在a标签中添加title属性的作用就是为链接添加描述性文字，wordpress中的导出链接的函数经常bai自带title的，seo实践认为的title属性对关键词排名是有利的，但要分情况，要做到合理不重复！
我们看两个代码：

```
<a title="闪电博客" href="http://shandian.biz/">闪电博客</a>
<a title="闪电博客" href="http://shandian.biz/">点击这里</a>
```

对于第一段代码，提示文字跟锚文本一样，这个提示就显得有点多余。第二段代码，提示文字跟锚文本不一样，我们通过锚文本不知道对应网站是干什么的，而有了title属性的提示文字，我们就可以知道。
对于第一种情况，title属性对seo是没有效果的，第二种情况，会有一些效果。
总结：在优化网站的时候，出现一些链接的锚文本我们无法读懂或者不能通过锚文本知道网站大体内容的，我们就可以给这个链接加上title属性；如果锚文本本身就能很清晰地让大家知道网站的大体内容，就没必要使用title属性。
从另一方面讲，有title的补充解释对用户的友好程度较高。

链接a标签中的title属性有利于SEO
里面要包含关键词；
我们常设置dao的是网页title，图专片title，链接title；
蜘蛛爬行属时会经过a标签中的title，所以有利于SEO；
另外：网页的SEO优化：标题（title），描述（description），关键字(keywords)，代码优化，结构优化，图片优化，链接优化等等；而a中的重要程度并不是很高，但肯定有利于SEO优化。
页面SEO优化很重要的一部分就是关键词优化，而title属性中包含关键词，也是蜘蛛关注的重要部分，达到内容相关性，包含关键词，提高用户体验度，所以有利于SEO优化！







### php怎么seo优化

#### 一、PHP网站关键词优化

  根据搜索引擎的工作原理，我们知道用户和搜索引擎都是根据关键词对目标网站进行搜索分析。通过分析这些的关键词和搜索流量，我们发现在网站发展前期关键词是影响网站被搜索引擎收录的一个核心因素，关键词给网站带来了大量用户的同时也带来了大量的流量，其流量比例占网站总流量的绝大部分。由此可见，关键词的优化对于网站的流量至关重要。而关键词的确定必须是和网站内容高度相关的，一般网站需要在以下位置设置关键词:

  (1)关键词需要出现在标签当中，也就是标题当中需要包含关键词，而且还需要保证不同的页面是不一样的;

  (2)关键词应放在网站的标签内的keywords和description里面，并且一般只可出现一次;

  (3)网站logo图片的Alt属性中可以设置于网站主题的关键词，其他图片的Alt应放着与图片相符合的ALT属性，否则会被搜索引擎认为在作弊;

  (4)网站的目录名和文件名可以设置为关键词，会更好的被搜索引擎抓取;

  (5)网页内容的中一般放置一篇文章的标题或者内容提要，这里需要放置关键词，但是整个页面的关键词不易设置过度，一般设置在 标签中，但需与文章内容相关，否则会认为在作弊。（php视频教程）

#### 二、PHP网站 URL地址优化

  URL地址优化包括URL地址静态化(又叫伪静态)和URL地址转向两个方面。根据搜索引擎的搜索原理，静态页面更有利于搜索引擎抓取收录。现在大多数网站都是动态的页面，比如本文所讨论的PHP网站就为动态链接的页面。那么我们就要采取措施把PHP动态生成的页面转化为静态页面。

#### 三、PHP网站地图优化

  网站地图优化又叫网站导航优化俗称sitemap。首先网站地图为网站访问者指明了访问网站的方向和路径，清晰明了的告诉网站访问者网站的布局和内容，给网站访问者友好的体验。用户的体验感觉不错，那么他下次访问网站的几率就会大大提高;其次搜索引擎蜘蛛也非常喜欢网站地图。因此做好网站地图SEO，对于网站非常重要。

  (1)针对PHP网站，一般采用XML格式的网站地图。网站地图保存在根目录下的一个XML文件里，大家在很多网站的底部都会发现有这么一个文件。例如：www.xxx.com/sitemap.xml,它是网站上链接的列表。制作一个简洁明了高效的网站地图，可以为搜索引擎快速浏览整个网站的窗口，并且收录网站的全部内容。

  (2)一般在网站的footer下添加一个关键词，并指向相应的内容页面。

#### 四、 url地址静态化

  (1))把网页上带链接的地方，都换上新的静态化链接。搜索引擎和浏览器将通过该链接来发生请求。

  (2)Apache服务器中在httpd.conf或.htaccess使用”/dir/([^./]*)\.html”来实现新的重写规则，告诉Apache服务执行这个重写规则之后的操作。通过这样一个重写规则使得PHP生成的动态页面转化为静态页面展现给搜索引擎。当搜索引擎蜘蛛爬行到这里页面的时候，就会记录下这个新的页面，从而达到URL地址优化的目的。在执行这样的操作后，要保留原链接只需在httpd.conf中使用Alias指令(仅适用于apache服务器)。







### PHP实现页面静态化

随着网站的内容的增多和用户访问量的增多，无可避免的是网站加载会越来越慢，受限于带宽和服务器同一时间的请求次数的限制，我们往往需要在此时对我们的网站进行代码优化和服务器配置的优化。 

**一般情况下会从以下方面来做优化**

1、动态页面静态化

2、优化数据库

3、使用负载均衡

4、使用缓存

5、使用CDN加速

现在很多网站在建设的时候都要进行静态化的处理，为什么网站要进行静态化处理呢？我们都知道纯静态网站是所有的网页都是独立的一个html页面，当我们访问的时候不需要经过数据的处理直接就能读取到文件，访问速度就可想而知了，而其对于搜索引擎而言也是非常友好的一个方式。



静态化常见的方法：
1、用smarty模板，是一种缓存机制，简单学习一下就好了；
2、把页面全部生成了静态html文件，常见的方法是按照网页的规律，用正则匹配网址，然后确定一个静态的html路径，路径存到数据库里，生成为html文件，然后链接全部读取html的路径。
3、伪静态，就是服务器把地址伪装成html格式的，其实不是真正的静态html文件。可以搜索：apache rewrite 重写。是根据网址的规则，用正则表达式匹配的，比如新闻页面news.php?id=100,匹配成news/100.html。



**纯静态网站在网站中是怎么实现的？**
纯静态的制作技术是需要先把网站的页面总结出来，分为多少个样式，然后把这些页面做成模板，生成的时候需要先读取源文件然后生成独立的以.html结尾的页面文件，所以说纯静态网站需要更大的空间，不过其实需要的空间也不会大多少的，尤其是对于中小型企业网站来说，从技术上来讲，大型网站想要全站实现纯静态化是比较困难的，生成的时间也太过于长了。不过中小型网站还是做成纯静态的比较，这样做的优点是很多的。

 

**而动态网站又是怎么进行静态处理的？**
页面静态化是指将动态页面变成html/htm静态页面。动态页面一般由asp,php,jsp,.net等程序语言编写而成，非常便于管理。但是访问网页时还需要程序先处理一遍，所以导致访问速度相对较慢。而静态页面访问速度快，却又不便于管理。那么动态页面静态化即可以将两种页面的好处集中到一起。

 

**静态处理后又给网站带来了哪些好处？**

1、静态页面相对于动态页面更容易被搜索引擎收录。

2、访问静态页面不需要经过程序处理，因此可以提高运行速度。

3、减轻服务器负担。

4、HTML页面不会受Asp相关漏洞的影响。

静态处理后的网站相对没有静态化处理的网站来讲还比较有安全性，因为静态网站是不会是黑客攻击的首选对象，因为黑客在不知道你后台系统的情况下，黑 客从前台的静态页面很难进行攻击。同时还具有一定的稳定性，比如数据库或者网站的程序出了问题，他不会干扰到静态处理后的页面，不会因为程序或数据影响而 打不开页面。

搜索引擎蜘蛛程序更喜欢这样的网址，也可以减轻蜘蛛程序的工作负担，虽然有的人会认为现在搜索引擎完全有能力去抓取和识别动态的网址，在这里还是建议大家能做成静态的尽量做成静态网址。

 

下面我们主要来讲一讲页面静态化这个概念，希望对你有所帮助！

**什么是HTML静态化:**

**![img](https://img-blog.csdnimg.cn/20190529171429234.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2Fzc2FzaW4wMzA4,size_16,color_FFFFFF,t_70)**

常说的页面静态化分为两种，一种是**伪静态**，即url 重写，一种是**真静态化**。
在PHP网站开发中为了网站推广和SEO等需要，需要对网站进行全站或局部静态化处理，PHP生成静态HTML页面有多种方法，比如利用PHP模板、缓存等实现页面静态化。
**PHP静态化的简单理解**就是使网站生成页面以静态HTML的形式展现在访客面前，PHP静态化分纯静态化和伪静态化，两者的区别在于PHP生成静态页面的处理机制不同。
**PHP伪静态**：利用Apache mod_rewrite实现URL重写的方法。

 

**HTML静态化的好处**:

一、减轻服务器负担，浏览网页无需调用系统数据库。
二、有利于搜索引擎优化SEO，Baidu、Google都会优先收录静态页面，不仅被收录的快还收录的全；
三、加快页面打开速度，静态页面无需连接数据库打开速度较动态页面有明显提高；
四、网站更安全，HTML页面不会受php程序相关漏洞的影响；观看一下大一点的网站基本全是静态页面，而且可以减少攻击，防sql注入。数据库出错时，不影响网站正常访问。
五、数据库出错时，不影响网站的正常访问。
最主要是可以增加访问速度,减轻服务器负担,当数据量有几万，几十万或是更多的时候你知道哪个更快了. 而且还容易被搜索引擎找到。生成html文章虽操作上麻烦些，程序上繁杂些，但为了更利于搜索，为了速度更快些，更安全，这些牺牲还是值得的。

 

**实现HTML静态化的策略与实例讲解:**
**基本方式**
file_put_contents()函数 
使用php内置缓存机制实现页面静态化 —output-bufferring.

![img](https://img-blog.csdnimg.cn/2019052917150686.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2Fzc2FzaW4wMzA4,size_16,color_FFFFFF,t_70)

**方法1:利用PHP模板生成静态页面**

PHP模板实现静态化非常方便，比如安装和使用PHP Smarty实现网站静态化。
在使用Smarty的情况下，也可以实现页面静态化。下面先简单说一下使用Smarty时通常动态读取的做法。 
**一般分这几步：**
1、通过URL传递一个参数(ID);
2、然后根据此ID查询数据库;
3、取得数据后根据需要修改显示内容;
4、assign需要显示的数据;
5、display模板文件。
Smarty静态化过程只需要在上述过程中添加两个步骤。
第一：在1之前使用 ob_start() 打开缓冲区。
第二：在5之后使用 ob_get_contents() 获取内存未输出内容，然后使用fwrite()将内容写入目标html文件。
根据上述描述，此过程是在网站前台实现的，而内容管理(添加、修改、删除)通常是在后台进行，为了能有效利用上述过程，可以使用一点小手段，那就是Header()。具体过程是这样的：在添加、修改程序完成之后，使用Header() 跳到前台读取，这样可以实现页面HTML化，然后在生成html后再跳回后台管理侧，而这两个跳转过程是不可见的。

**方法2:使用PHP文件读写功能生成静态页面**

```php
$out1 = "<html><head><title>PHP网站静态化教程</title></head><body>欢迎访问PHP网站开发www.startphp.cn，本文主要介绍PHP网站页面静态化的方法</body></html>"; 
$fp = fopen("leapsoulcn.html","w"); 
if(!$fp) 
\\{ 
echo "System Error"; 
exit(); 
\\} 
else 
\\{ 
fwrite($fp,$out1); 
fclose($fp); 
echo "Success"; 
\\}
```

**方法3：使用PHP输出控制函数（Output Control）/ob缓存机制生成静态页面**
输出控制函数（Output Control）也就是使用和控制缓存来生成静态HTML页面，也会使用到PHP文件读写函数。
比如某个商品的动态详情页地址是: http://xxx.com?goods.php?gid=112
那么这里我们根据这个地址读取一次这个详情页的内容，然后保存为静态页，下次有人访问这个商品详情页动态地址时，我们可以直接把已生成好的对应静态内容文件输出出来。

**PHP生成静态页面实例代码 1**

```php
ob_start(); 
echo "<html>". 
"<head>". 
"<title>PHP网站静态化教程</title>". 
"</head>". 
"<body>欢迎访问脚本之家，本文主要介绍PHP网站页面静态化的方法</body>". 
"</html>"; 
$out1 = ob_get_contents(); 
ob_end_clean(); 
$fp = fopen("leapsoulcn.html","w"); 
if(!$fp) 
\\{ 
echo "System Error"; 
exit(); 
\\} 
else 
\\{ 
fwrite($fp,$out1); 
fclose($fp); 
echo "Success"; 
\\} 
```

**PHP生成静态页面实例代码 2**

```php
$gid = $_GET['gid']+0;//商品id 
$goods_statis_file = "goods_file_".$gid.".html";//对应静态页文件 
$expr = 3600*24*10;//静态文件有效期，十天 
if(file_exists($goods_statis_file))\\{ 
 $file_ctime =filectime($goods_statis_file);//文件创建时间 
 if($file_ctime+$expr-->time())\\{//如果没过期 
  echo file_get_contents($goods_statis_file);//输出静态文件内容 
  exit; 
 \\}else\\{//如果已过期 
  unlink($goods_statis_file);//删除过期的静态页文件 
  ob_start(); 
 
  //从数据库读取数据，并赋值给相关变量 
 
  //include ("xxx.html");//加载对应的商品详情页模板 
 
  $content = ob_get_contents();//把详情页内容赋值给$content变量 
  file_put_contents($goods_statis_file,$content);//写入内容到对应静态文件中 
  ob_end_flush();//输出商品详情页信息 
 \\} 
\\}else\\{ 
ob_start(); 
 
 //从数据库读取数据，并赋值给相关变量 
 
 //include ("xxx.html");//加载对应的商品详情页模板 
 
 $content = ob_get_contents();//把详情页内容赋值给$content变量 
 file_put_contents($goods_statis_file,$content);//写入内容到对应静态文件中 
 ob_end_flush();//输出商品详情页信息 
 
\\}
```

我们知道使用PHP进行网站开发，一般执行结果直接输出到游览器，为了使用PHP生成静态页面，就需要使用输出控制函数控制缓存区，以便获取缓存区的内容，然后再输出到静态HTML页面文件中以实现网站静态化。

PHP生成静态页面的思路为：首先开启缓存，然后输出了HTML内容（你也可以通过include将HTML内容以文件形式包含进来），之后获取缓存中的内容，清空缓存后通过PHP文件读写函数将缓存内容写入到静态HTML页面文件中。
获得输出的缓存内容以生成静态HTML页面的过程需要使用三个函数：ob_start()、ob_get_contents()、ob_end_clean()。


**知识点：**
1、ob_start函数一般主要是用来开启缓存，注意使用ob_start之前不能有任何输出，如空格、字符等。
2、ob_get_contents函数主要用来获取缓存中的内容以字符串形式返回，注意此函数必须在ob_end_clean函数之前调用，否则获取不到缓存内容。
3、ob_end_clean函数主要是清空缓存中的内容并关闭缓存，成功则返回True，失败则返回False
**方法4：使用nosql从内存中读取内容(其实这个已经不算静态化了而是缓存);**
以memcache为例：

```php
gid = $_GET['gid']+0;//商品id 
$goods_statis_content = "goods_content_".$gid;//对应键 
$expr = 3600*24*10;//有效期，十天 
$mem = new Memcache; 
$mem--->connect('memcache_host', 11211); 
$mem_goods_content = $mem->get($goods_statis_content);  
if($mem_goods_content)\\{ 
 echo $mem_goods_content; 
\\}else\\{ 
 ob_start(); 
 
 //从数据库读取数据，并赋值给相关变量 
 
 //include ("xxx.html");//加载对应的商品详情页模板 
 
 $content = ob_get_contents();//把详情页内容赋值给$content变量 
 $mem->add($goods_statis_content,$content, false, $expr); 
 ob_end_flush();//输出商品详情页信息 
 
\\} 
```

memcached是键值一一对应，key默认最大不能超过128个字节，value默认大小是1M，因此1M大小满足大多数网页大小的存储。



PHP站点开发过程中，因为搜索引擎对PHP页面搜鹿和html页面的收录有一定的区别，为了站点的推广或者SEO的须要，要对站点进行一定的静态化。静态化并非页面中没有动画等元素，而是指网页的html代码都在页面中，不须要再去执行PHP脚本等server端的语言，我们能够直接訪问到的网页。这就是静态网页。

有一种方式是改写訪问地址，能够通过URL的PATHINFO模式来改动它。让它看上去更像一个静态页面。从而有更大的几率被搜索引擎抓取和收录，仅是对搜索引擎比較友好，伪静态化。

第二种就是站点能够在用户訪问站点之前就通过一定的程序来进行静态化。生成静态页面。当用户去訪问该页面的时候。因为訪问的是静态页面，因此，訪问速度会比訪问动态页面的速度快了非常多倍，前台的表现是页面载入速度变快，在后台的表现是降低了数据库的连接。降低了数据库的压力，唯一的缺点就是相对占的硬盘多一些，硬盘相对便宜的多。

纯静态化，就是生成HTML文件的方式，我们须要开启PHP自带的缓存机制，即ob_start来开启缓存。而且在ob_start之前不能有不论什么输出，否则运行失败，然后我们用ob_get_contents函数来获取缓存中的内容，该函数会返回一个字符串。第三个函数就是ob_end_clean，它用来清空缓存中的内容而且关闭，成功返回True，失败返回False。

```
<?php
//开启缓存
ob_start();
//第一步连接数据库
$conn = mysqli_connect("localhost","root","","bbs");
//第二步设置对应的字符编码
$setting = 'set names utf8';
mysqli_query($conn,$setting);
//第三步进行查询
$sql = 'SELECT * FROM user';
$result = mysqli_query($conn,$sql);
//第四步把查询结果转化为一个数组
$rows = mysqli_num_rows($result);
$sqldata = array();
for($i = 0;$i <$rows;$i ++)\\{
    $sqldata[] = mysqli_fetch_assoc($result);
\\}
//然后打印该信息
var_dump($sqldata);
//得到生成的html文件，下次訪问就无需訪问数据库了
$msg = ob_get_contents();
ob_end_clean();
//把输出内容放入一个html文件里
$f = fopen("static.html","w");
fwrite($f,$msg);
echo "静态化成功";
```

目录下生成一个html文件

这样浏览器直接訪问html文件，从而减轻了数据库的压力。 



**为什么要页面静态化？**

1.动态文件执行过程:语法分析-编译-运行

2.静态文件，不需要编译，减少了服务器脚本运行的时间，降低了服务器的响应时间，直接运行，响应速度快；如果页面中一些内容不经常改动，动态页面静态化是非常有效的加速方法。（纯静态，伪静态还是需要PHP解释器的）

3、生成静态URL利于SEO，利于蜘蛛抓取和收录，有利于提升排名

**优化页面响应时间方法**

1.动态页面静态化

2.优化数据库

3.负载均衡

4.使用缓存等等

//动态页面静态化一般用于不经常改动的地方，频繁改动的地方一般不适用静态化，可用伪静态（例如微博等）

**静态化详细介绍**

1、纯静态分为局部静态化（局部动态化，使用AJAX动态获取数据）和纯静态化。

伪静态：改变URL（需要服务器支持,如：apache等等）

2、从URL结构以及页面名称看，伪静态和静态页面是一样的。伪静态的页面后缀可以是html htm 或者是目录格式

伪静态只是改变了URL的表现形式，实际上还是动态页面

静态页面可以节省服务器资源，而伪静态严格说是增加服务器资源消耗的

总结，在SEO方面，伪静态和静态页面的功能是相同的，但是伪静态本质上还是动态页面，所以消耗资源是和动态页面一样的，而且因为Rewrite服务器还需要消耗额外的资源。

**Buffer缓冲区认知**

![img](https://img.jbzj.com/file_images/article/201609/20160906152732.jpg)

**1、开启buffer**

•在php.ini中的output_buffering开启
•在php文件中使用ob_start()函数开启

```
`; Default Value: Off``; Development Value: 4096``; Production Value: 4096``; http:``//php.net/output-buffering``output_buffering = 4096`
```

**2、获取缓冲区的内容**

output_buffering=on 需要先开起，才能调用ob_get_contents()函数。但是，如果不开启output_buffering时，当在头文件中调用函数ob_start()函数时，ob_get_contents()也能使用。

ob_get_content();//返回输出缓冲区的内容;

**PHP如何实现页面纯静态化**

**基本方式**

1、file_put_contents

2、使用PHP内置缓存机制实现页面静态化output_buffering

```
`ob_start()``//如果php.ini已经开启，那么这里会开启一个新的输出缓冲区;``ob_get_contents()``//获取输出缓冲区内容；``ob_clean()``//清空输出缓冲区内容，但是不会删除输出缓冲区``ob_get_clean``//获取输出缓冲区内容并且删除输出缓冲区，等价于ob_get_contents和ob_end_clean)`
```

下方这段代码，运行是不会有输出的

原因就是输出缓冲区被清空了，看上图理解

```
`ob_start();``echo ``777``;``echo ``000``;``ob_clean();``echo ob_get_contents();`
```



纯静态实现，代码和实现逻辑参考：

```
``/**`` ``* 触发系统生成纯静态化页面业务逻辑`` ``* 有3种方案： `` ``* 第一：定时扫描程序(利用crontab来处理) `` ``* 第二：手动触发方式，人为触发`` ``* 第三：页面添加缓存时间，在页面中控制时间来操作``*/``//===========================================``//生成纯静态文件步骤``//1、连接数据库，然后从数据库里面获取数据``//2、把获取到的数据填充到模版文件里面``//3、需要把动态的页面转为静态页面，生成静态化文件``//============================================``//PHP实现页面静态化有以下步骤：``//1:A.php请求数据库数据：通过mysql或者mysqli或者PDO扩展``//2:在A.html中输出A.php请求的数据库数据:一般是将将在数据库中取出的数组形式的数据赋予新的数组，并且输出``//3:在A.php中包含A.html文件:直接通过require_once()函数或者inclde_once()``//4：开启数据缓存ob_start()=>获取获取缓存内容并且将数据生成在静态文件中file_put_contents('index.shtml',ob_get_clean());``//header("content-type:text/htm;charset=utf-8");``if``(``is_file``(``'./index.html'``) && (time() - ``filemtime``(``'./index.html'``) < 1200))``\\{`` ``//缓存未失效则直接加载静态文件`` ``require_once``(``'./index.html'``);``\\}``else``\\{`` ``//缓存失效了则重新生成`` ``// 引入数据库链接操作`` ``require_once``(``'./db.php'``);`` ``$sql` `= ``"select * from news where `category_id` = 1 and `status` = 1 limit 4"``;`` ``try`` ``\\{``   ``$db` `= Db::getInstance()->connect();``   ``$result` `= mysql_query(``$sql``, ``$db``);``   ``$newsList` `= ``array``();``   ``while``(``$row` `= mysql_fetch_assoc(``$result``)) ``   ``\\{``     ``$newsList``[] = ``$row``;``   ``\\}`` ``\\}`` ``catch``(Exception ``$e``)`` ``\\{``   ``// TODO`` ``\\}`` ``ob_start();`` ``require_once``(``'template/index.php'``);``//引入模版文件`` ``file_put_contents``(``'./index.html'``, ob_get_contents());``//生成静态文件`` ``//ob_clean();``\\}`
```

**静态页面中局部动态化实现**

利用Jquery中的ajax请求文件，获取到返回的JSON数据，然后应用到模版就可以了

**伪静态**

Nginx服务器默认不支持PATH INFO模式，需要额外配置

Apache伪静态设置

![img](https://img.jbzj.com/file_images/article/201609/20160906153212.jpg)

1、开启apache mod_rewrite.so 配置 在 httpd.conf中。

测试的话可以用phpinfo查看，看是否loaded modules 有这个模块

2、inculde conf/extra/httpd-vhosts.conf virtual hosts支持，虚拟域名配置

3、编辑vartual host 文件

4、本机host文件加入配置的域名（如果需要本机测试针对windows）

5、伪静态配置

\- 5.1 rewrite engine on 
\- 5.2编写规则

```
`^/post/([0-9]*).html$ /post.php?id=``$1`
```

放在 virtualhost 段中 

post.php 中编写

```
``echo` `'this is '``.``$_GET``[``'id'``];`
```

然后可以访问a.com/123.html 返回的就是this is 123.

扩展：如果目录下有123.html这个真正的文件，那么还是加载了动态的post 123. 
那么如何设置呢，想要当前文件有了真正的静态文件，那么需要以下配置了

```
`RewriteEngine on``RewriteRule ^/post/([0-9]*).html$ /post.php?id=``$1``#存在目录``RewriteCond \\%｛DOCUMENT_ROOT\\}\\%\\{REQUEST_FILENAME\\}!-d``#存在文件``RewriteCond\\%｛DOCUMENT_ROOT｝\\%\\{REQUEST_FILENAME}}!-f`
```

以上两句话意思是如果根目录下有请求的目录或者文件，那就用他

当然这个要放在刚刚的那个rewrite的上面。

**Nginx伪静态**

![img](https://img.jbzj.com/file_images/article/201609/20160906153552.jpg)

伪静态是影响服务器性能的，不是越多越好，需要按需求而定









### robots优化

robots.txt 文件对抓取网络的搜索引擎漫游器（称为漫游器）进行限制。这些漫游器是自动的，在它们访问网页前会查看是否存在限制其访问特定网页的 robots.txt 文件。如果你想保护网站上的某些内容不被搜索引擎收入的话，robots.txt是一个简单有效的工具。这里简单介绍一下怎么使用它。

robots.txt自身是一个文本文件。它必须位于域名的根目录中并 被命名为"robots.txt"。位于子目录中的 robots.txt 文件无效，因为漫游器只在域名的根目录中查找此文件。例如，http://www.example.com/robots.txt 是有效位置，http://www.example.com/mysite/robots.txt 则不是。

①robots.txt纯文本文件，网站管理员可以在这里声明该网站不想robots访问的部分，所以robots优化直接影响着搜索引擎对网站的收录情况；

②robots.txt必须放置在一个站点的根目录下，并且文件名必须全部小写：；

③就算你的网站全部内容都可以被搜索引擎收录，那也要写个空的robots.txt；因为有的服务器的设置会使没有robots.txt的时候返回200状态码和相应的错误信息；



织梦DedeCMS本身自带有一个robots.txt文件，但是里面的设置很简单，并不能完全满足网站的优化要求，尤其是对于使用伪静态的网站来说，robots.txt文件的优化，要怎样做才行呢？

下面是我的一点想法，适用于伪静态的DedeCMS网站。

###  User-agent: * 

　　Disallow: /dede 织梦管理后台目录，需要改名，具体设置在下面详细说明

　　Disallow: /include 程序核心文件目录

　　Disallow: /member 会员管理目录，有些文件可以开放

　　Disallow: /plus 插件及辅助功能目录

　　Disallow: /templets [织梦模板](http://www.dede58.com/)文件存放目录

　　Disallow: /data 系统缓存或其它可写入数据存放目录

　　Disallow: /uploads 上传下载文件保存目录,不想搜索引擎引用图片的话，禁止

　　Disallow: /images 系统默认模板图片存放目录

　　Disallow: /index.php 网站默认首页，静态化的话，最好禁止

　　Disallow: /404.html 404错误页面

　　Allow: /plus/search.php 开放禁止目录里的具体文件

 

下面着重讲下后台管理目录和栏目页的设置：

　　1、dede后台管理目录，为了网站安全考虑需要改名。然而改名之后，大家不免疑惑：改了名，应该在robots.txt文件里怎么设置禁止搜索引擎抓取呢？如果直接禁止抓取，就泄露了后台目录，等于改名无效。我们可以通过下面的设置解决这个问题，如我们设置后台目录为dedecms：

　　在robots.txt文件里面加上“Disallow: /d*ms”这句就可以了。

　　这样我们就能即禁止了搜索引擎的抓取，又不会泄露了后台目录名称。

 　2、栏目页。有些人会注意到，如果网站不做伪静态优化的话，栏目分页后会有两个链接指向栏目首页，如*/web/和*/web/list_1_1.html，为了网站优化，建议先将栏目分页优化以下(具体做法大家可以在网上找)，把首页和第一页的链接改为*/web/的形式，然后在robots.txt文件里做以下设置:

　　在robots.txt文件里面加上“Disallow: /*1.html$“这句。

 　以上就是DEDECMS robots.txt文件的设置，大家可以根据自己网站的情况具体设置。

 

 注意事项：

1.为安全起见，最好按官方说明设置好网站目录权限；

2.后台目录改后的名称开头字母和结尾字母不要和其他目录有相同之处；

3.设置完成后最好用百度站长工具测试一下robots.txt文件设置是否有效。



### 2、robots的写法

\# robots.txt file from

\# All robots will spider the domain

User-agent:*

Disallow:

①允许搜索引擎访问所有部分

User-agent:*

Disallow:

②禁止搜索引擎访问任何部分

User-agent:*

Disallow:/

③禁止搜索引擎访问某几个部分

User-agent:*

Disallow:

Disallow:

Disallow:

④允许某个搜索引擎访问

User-agent:Baiduspiter

Disallow:/

⑤禁止所有浏览器访问某几个目录下的内容及文件

User-agent:*

Disallow:/sss/

Disallow:/aaa/

⑥禁止除了百度浏览器以外的所有搜索引擎抓取任何内容：

User-agent:Baiduspiter

Disallow:/

User-agent:*

Disallow:/

⑦$：通配符，匹配url结尾的字符。禁止百度抓取所有.jpg文件

User-agent:Baiduspiter



这里举一个robots.txt的例子:

```
User-agent: *
Disallow: /cgi-bin/
Disallow: /tmp/
Disallow: /~name/
```

***使用 robots.txt 文件拦截或删除整个网站** 
要从搜索引擎中删除您的网站，并防止所有漫游器在以后抓取您的网站，请将以下 robots.txt 文件放入您服务器的根目录：`User-agent: \* Disallow: / `要只从 Google 中删除您的网站，并只是防止 Googlebot 将来抓取您的网站，请将以下 robots.txt 文件放入您服务器的根目录：`User-agent: Googlebot Disallow: / `每个端口都应有自己的 robots.txt 文件。尤其是您通过 http 和 https 托管内容的时候，这些协议都需要有各自的 robots.txt 文件。例如，要让 Googlebot 只为所有的 http 网页而不为 https 网页编制索引，应使用下面的 robots.txt 文件。
对于 http 协议 (http://yourserver.com/robots.txt):`User-agent: \* Allow: / `对于 https 协议 (https://yourserver.com/robots.txt):`User-agent: \* Disallow: / `**允许所有的漫游器访问您的网页**`User-agent: \* Disallow: `(另一种方法: 建立一个空的 "/robots.txt" 文件, 或者不使用robot.txt。)

**使用 robots.txt 文件拦截或删除网页**

您可以使用 robots.txt 文件来阻止 Googlebot 抓取您网站上的网页。 例如，如果您正在手动创建 robots.txt 文件以阻止 Googlebot 抓取某一特定目录下（例如，private）的所有网页，可使用以下 robots.txt 条目： 
`User-agent: Googlebot Disallow: /private`要阻止 Googlebot 抓取特定文件类型（例如，.gif）的所有文件，可使用以下 robots.txt 条目：`User-agent: Googlebot Disallow: /\*.gif$`要阻止 Googlebot 抓取所有包含 ? 的网址（具体地说，这种网址以您的域名开头，后接任意字符串，然后是问号，而后又是任意字符串），可使用以下条目：`User-agent: Googlebot Disallow: /\*? `尽管我们不抓取被 robots.txt 拦截的网页内容或为其编制索引，但如果我们在网络上的其他网页中发现这些内容，我们仍然会抓取其网址并编制索引。因此，网页网址及其他公开的信息，例如指 向该网站的链接中的定位文字，有可能会出现在 Google 搜索结果中。不过，您网页上的内容不会被抓取、编制索引和显示。

作为网站管理员工具的一部分，Google提供了[robots.txt分析工具](http://www.google.cn/support/webmasters/bin/answer.py?hlrm=en&answer=35237)。它可以按照 Googlebot 读取 robots.txt 文件的相同方式读取该文件，并且可为 Google user-agents（如 Googlebot）提供结果。我们强烈建议您使用它。 在创建一个robots.txt文件之前，有必要考虑一下哪些内容可以被用户搜得到，而哪些则不应该被搜得到。 这样的话，通过合理地使用robots.txt, 搜索引擎在把用户带到您网站的同时，又能保证隐私信息不被收录。



误区一：我的网站上的所有文件都需要蜘蛛抓取，那我就没必要在添加robots.txt文件了。反正如果该文件不存在，所有的搜索蜘蛛将默认能够访问网站上所有没有被口令保护的页面。

　　每当用户试图访问某个不存在的URL时，服务器都会在日志中记录404错误（无法找到文件）。每当搜索蜘蛛来寻找并不存在的robots.txt文件时，服务器也将在日志中记录一条404错误，所以你应该做网站中添加一个robots.txt。



误区二：在robots.txt文件中设置所有的文件都可以被搜索蜘蛛抓取，这样可以增加网站的收录率。
　　网站中的程序脚本、样式表等文件即使被蜘蛛收录，也不会增加网站的收录率，还只会浪费服务器资源。因此必须在robots.txt文件里设置不要让搜索蜘蛛索引这些文件。
　　具体哪些文件需要排除， 在robots.txt使用技巧一文中有详细介绍。
　　

误区三：搜索蜘蛛抓取网页太浪费服务器资源，在robots.txt文件设置所有的搜索蜘蛛都不能抓取全部的网页。
　　如果这样的话，会导致整个网站不能被搜索引擎收录。



### robots.txt使用技巧

  *1. 每当用户试图访问某个不存在的URL时，服务器都会在日志中记录404错误（无法找到文件）。每当搜索蜘蛛来寻找并不存在的robots.txt文件时，服务器也将在日志中记录一条404错误，所以你应该在网站中添加一个robots.txt。*

  　　2. 网站管理员必须使蜘蛛程序远离某些服务器上的目录——保证服务器性能。比如：大多数网站服务器都有程序储存在“cgi-bin”目录下，因此在robots.txt文件中加入“Disallow: /cgi-bin”是个好主意，这样能够避免将所有程序文件被蜘蛛索引，可以节省服务器资源。一般网站中不需要蜘蛛抓取的文件有：后台管理文件、程序脚本、附件、数据库文件、编码文件、样式表文件、模板文件、导航图片和背景图片等等。
       下面是VeryCMS里的robots.txt文件：

　　User-agent: *
　　Disallow: /admin/ 后台管理文件

　　Disallow: /require/ 程序文件
　　Disallow: /attachment/ 附件

　　Disallow: /images/ 图片
　　Disallow: /data/ 数据库文件

　　Disallow: /template/ 模板文件
　　Disallow: /css/ 样式表文件

　　Disallow: /lang/ 编码文件
　　Disallow: /script/ 脚本文件

  　　3. 如果你的网站是动态网页，并且你为这些动态网页创建了静态副本，以供搜索蜘蛛更容易抓取。那么你需要在robots.txt文件里设置避免动态网页被蜘蛛索引，以保证这些网页不会被视为含重复内容。
        　　4. robots.txt文件里还可以直接包括在sitemap文件的链接。就像这样：

　　Sitemap: sitemap.xml
　　目前对此表示支持的搜索引擎公司有Google, Yahoo, Ask and MSN。而中文搜索引擎公司，显然不在这个圈子内。这样做的好处就是，站长不用到每个搜索引擎的站长工具或者相似的站长部分，去提交自己的sitemap文件，搜索引擎的蜘蛛自己就会抓取robots.txt文件，读取其中的sitemap路径，接着抓取其中相链接的网页。

  　　5. 合理使用robots.txt文件还能避免访问时出错。比如，不能让搜索者直接进入购物车页面。因为没有理由使购物车被收录，所以你可以在robots.txt文件里设置来阻止搜索者直接进入购物车页面。



> Robots.txt即爬虫协议，是搜索引擎蜘蛛进入网站第一个寻找的文件，它告诉搜索引擎哪些页面可以抓取，哪些页面不能抓取。

当我们网站出现错误页面，或者某些页面不想让蜘蛛爬取时，合理的配置robots协议可以让蜘蛛更高效快捷的爬取到需要抓取的内容。当搜索引擎蜘蛛进入网站，首先查找网站根目录下是否存在robots.txt文件，若存在，则按照该文件的规范抓取内容；若不存在该文件，则按照默认的规则爬取网站中所有网页。因此，本文介绍一些robots语法和常用实例。

网站设置robots.txt的好处：禁止搜索引擎收录部分页面；引导蜘蛛爬网站地图；能够一定程度上保护网站安全；节省流量等。



### Robots基本语法：

1、定义搜索引擎：User-agent。

```
User-agent: *  #所有的搜索引擎
User-agent: Baiduspider #百度蜘蛛
User-agent: Googlebot #谷歌蜘蛛
```

2、Disallow 禁止爬取。

```
Disallow: /admin/ #禁止爬取admin文件夹
Disallow: /login.html #禁止爬取登录页面
```

3、Allow 允许。默认情况下，都是允许的。

例如：禁止admin文件夹下的所有文件，除了.html的网页。如果用Disallow一个一个的禁止，太浪费时间了。

此时用Allow就解决这个问题：

```
Allow: /admin/.html$ 
Disallow: /admin/
```

4、$ 结束符。

例：允许所有的以.html结尾的文件。不管前面有多长的URL，只要以.html结尾都允许

```
Allow: .html$
```

5、* 通配符符号0或多个任意字符。

例：屏蔽所有的动态URL

```
User-agent: *
Disallow: /*?*
```

6、Sitemap 声明网站地图。

```
Sitemap: http://www.xiaowangyun.com/sitemap.xml
```

7、#: 注释符。

8、版本号

```
Robot-version: Version 1.0
```

**注：**

```
1.robots.txt文件存放在网站根目录下。
2.文件名所有字母都必须小写（robots.txt）。
3.User-agent、Disallow、Allow、Sitemap必须是第一个字母大写，后面的字母小写，后面英文字符下的空格。
```



### 常用Robots.txt 文件举例

例1、禁止所有搜索引擎访问网站的任何部分

```
User-agent: *
Disallow: /
```

例2、禁止访问某些目录。注意的是对每一个目录必须分开声明。

```
User-agent: *
Disallow: /admin/
Disallow: /log/
Disallow: /bin/
```

例3、禁止某个搜索引擎抓取网站上的所有图片

```
User-agent: *
Disallow: .jpg$
Disallow: .jpeg$
Disallow: .gif$
Disallow: .png$
Disallow: .bmp$
```