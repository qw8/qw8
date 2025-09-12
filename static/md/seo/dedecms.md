---
title: 织梦CMS
date: 2020-01-08 18:00:00
categories: 
- SEO
tags:
- SEO
---

### www.dedecms.com织梦

★模板介绍★ 
压滤机过滤机机械设备类网站织梦营销型模板(带手机版)
★模板安装方法★

1.把文件上传到你的站点的根目录（或者本地www目录配置好host和httpd-vhosts.conf），然后运行 http://你的域名/install/index.php 安装，根据提示填写好相关信息，如：
数据库名称：baowen6
数据库root-空
管理员admin-zhang6797
网站名称：聚氨酯保温管_橡塑保温管_硅酸盐板-山西上品国际贸易
点“下一步”...即可完成安装。
注：若提示无法安装，页面出现DIY字样。请进入install文件夹，将install_lock.txt文件删掉。把index.php.bak文件改为index.php即可！

2.安装好后，浏览器打开http://你的域名/dede/login.php输入admin-密码-验证码

在后台“系统设置”—“数据库备份/还原”，点右上角“数据还原”—点左下角“开始还原数据”，等待恢复数据库。
3.点“系统设置”—“系统基本参数”，修改一下网站基本信息，点一下左下角“确定”。（没有这一步，有时候会导致更新后，前台显示织梦默认模板内容）。
4.搜索"更新系统缓存"，回车，点击“开始执行”。
5.点“常用操作” - “一键更新网站” - “更新所有”-“开始更新”，重新生成一次所有页面，安装步骤全部完成。
后台地址：http://你的域名/dede
管理员账号：admin
管理员密码：admin
如果安装后出现网站错位和无数据的情况，请检查以下三点设置
一. 网站程序必须放在根目录
二. 进入后台[系统]-[系统基本参数]，修改“站点根网址”为你的网址，或者留空。
三. 进入后台[核心]-[网站栏目管理]，点击底部按钮中的“更新排序”。

===================================================
★模板作者介绍★

作者QQ：413886902

www.zmzmb.com追梦者模板

http://www.dede58.com/

http://www.360doc.com/content/14/0724/21/16498929_396830867.shtml常用全局变量标签及调用路径

https://ckeditor.com/编辑器

http://www.baowen6.com/install/index.php
http://www.baowen6.com/dede/login.php
http://www.baowen6.com/index.php



### 修改步骤

1.logo和网站名称，导航栏高度，网站地图链接修改，所有页面加地域化meta标签

```
<meta name="location" content="province=山西;city=吕梁;coord=111.14426,37.495347">
```

2.修改栏目名称英文和更新对应文件夹

3.dede文件夹重命名为admin（防止别人找到后台地址破解密码），删除install文件夹



### 安全

后台管理员不要使用admin或者其他一类很容易被猜到的账号！ 

使用最新版的dede cms建站，经常注意后台的升级信息哦！ 



### Dedecms织梦去掉路径URL中a目录的操作方法

**一：刚刚安装网站，即将新建数据去掉/a/方法**

如果你是新站我们可以在创建时文章栏目的时,选择网站根目录或者cms根目录,这样就会去掉a/

1、首选在系统设置那的系统基本参数那，文档HTML默认保存路径，把a去掉。

2、然后在到栏目管理那修改下,文件保存目录,自己命名（**所有的栏目修改“ 文件保存目录”，去掉a/，删除原来a文件夹即可**）

**二：网站已经创建过了数据，已经产生了/a/目录，这时候我们需要用到SQL命令处理。**

针对已经创建过了数据的网站，我们直接在Dedecms后台中命令中执行下面sql即可，然后重新生成页面。

输入,代码如下:

UPDATE dede_arctype SET typedir=REPLACE(typedir,'a/','')

sql执行语句界面在系统 —— SQL命令行工具——输入上面那段代码即可，注意dede_arctype要对应到你的数据库中的表名称，如果你的数据库表前缀为xiuzhan_那就要改成xiuzhan_arctype。



### 织梦robots

第一步：根目录新建robots.txt文件（ 此处命名必须为robots.txt，小写 ）

第二步：复制如下代码到robots.txt文件，（ 代码/dede/是后台默认的路径，如果有改动的话robots里也记得改哦！）以下文件路径都是不要蜘蛛访问的！如果你有其他隐私文件夹的话 自己在下面添加一行一样的代码写上文件夹名称蜘蛛就抓不到了！

```
User-agent: * 

Disallow: /data/
Disallow: /d*e/
Disallow: /images/
Disallow: /include/
Disallow: /plus/
Disallow: /skin/
Disallow: /static/
Disallow: /special/
Disallow: /templets/
Disallow: /uploads/

Sitemap: http://www.baowen6.com/sitemap.xml
```

注意事项
d*e是指dede，为了安全；路径后面一定要带“/”；

网站域名换成你自己的哦，Sitemap去百度下载个生成网站地图的软件生成sitemap.xml传到根目录，不然蜘蛛抓不到你的网站地图，会影响你网站收录！



### 将网站地图sitemap生成到根目录

dede默认的网站地图sitemap是生成在data目录下，因为data目录很特别，用dede的朋友都明白，因为安全和便于收录的考虑，需要把网站地图sitemap生成到网站根目录下，共享世纪就是如此！方法如下： 
详细的步骤： 
1、首先登录ftp，在根目录下建立rss文件夹 
2、修改根目录下你的管理员文件夹(默认是dede)下的makehtml_map.php文件 
将17行的$cfg_cmspath."/data/sitemap.html"; 
和22行的$cfg_cmspath."/data/rssmap.html"; 
data/ 去掉 
3、修改根目录下include下面的arc.rssview.class.php和sitemap.class.php 
在arc.rssview.class.php 
将71行的$murl = $GLOBALS['cfg_cmspath']."/data/rss/".$this->TypeID.".xml"; 
data/ 去掉 
在sitemap.class.php 
将57行的$typelink = $GLOBALS['cfg_cmsurl']."/data/rss/".$row->id.".xml"; 
和94行的$typelink = $GLOBALS['cfg_cmsurl']."/data/rss/".$row->id.".xml"; 
data/ 去掉 
好了，生成试试吧！此外，还可以用sitemap生成软件，生成之后手动上传到网站根目录，我自己用的sitemap生成器是sitemapx，比较顺手！ 



### 织梦cms生成xml格式的网站地图

1.分别打开/dede/inc/inc_menu.php和/dede/inc/inc_menu_map.php文件，找到 

```
<m:item name='更新主页HTML' link='makehtml_homepage.php' rank='sys_MakeHtml' target='main' />
```

下面一行增加

```
<m:item name='更新Sitemap' link='makehtml_sitemap.php' rank='sys_MakeHtml' target='main' /> 
```

2.拷贝一个dede/makehtml_homepage.php文件，重命名为makehtml_sitemap.php放在dede文件夹，找到

```
$dsql->ExecuteNoneQuery($iquery);
$iquery = "UPDATE `#@__homepageset` SET showmod='$showmod'";
```

这两行代码，将其注释或者直接删除，底部最后一行修改调用生成文件模板为makehtml_sitemap.htm，保存。

```
include DedeInclude('templets/makehtml_sitemap.htm');
```

3.制作后台更新模板文件

拷贝一个dede/templets/makehtml_homepage.htm文件，重命名为makehtml_sitemap.htm放在dede/templets文件夹中，这个文件中所有“主页”文字改为“网站地图”，找到

```
<form name="form1" action="makehtml_homepage.php" target="stafrm" method="post">
```

修改为action="makehtml_sitemap.php"，找到

```
<input name="templet" type="text" id="templet" style="width:300″ value="<?php echo $row['templet']?>">
```

修改value="plus/sitemap.htm"（default为默认风格模板文件夹，也可以放在plus文件夹），找到

```
<td height="20″ valign="top" bgcolor="#FFFFFF"><input name="position" type="text" id="position" value="<?php echo $row['position']?>" size="30″>
```

修改value="../sitemap.xml"（意思是默认在根目录生成），修改80行左右为以下代码

```
<input name="showmod" type="radio" value="0" class="np"/>
动态浏览
<input name="showmod" type="radio" class="np" value="1" checked/>
生成静态 (或者手动删除根目录下sitemap.xml文件)
```

去掉下面这一行代码，保存

```
<input name="view" class='coolbg np' type="button" id="view" value="预览主页" onClick="window.open('makehtml_homepage.php?dopost=view&templet='+form1.templet.value);" />
```

4.在dede/templets/index2.htm中增加下面的第二行代码

```
<li><a href="makehtml_homepage.php" target="main">更新主页HTML</a></li>
<li><a href="makehtml_sitemap.php" target="main">更新Sitemap</a></li>
```

5.在/templets/plus文件夹中创建XML样式文件sitemap.xsl

```
<?xml version="1.0" encoding="UTF-8"?>
<xsl:stylesheet version="2.0" 
                xmlns:html="http://www.w3.org/TR/REC-html40"
                xmlns:sitemap="http://www.sitemaps.org/schemas/sitemap/0.9"
                xmlns:xsl="http://www.w3.org/1999/XSL/Transform">
	<xsl:output method="html" version="1.0" encoding="UTF-8" indent="yes"/>
	<xsl:template match="/">
		<html xmlns="http://www.w3.org/1999/xhtml">
			<head>
				<title>XML Sitemap</title>
				<meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
				<style type="text/css">
					body \\{font-family:"Lucida Grande","Lucida Sans Unicode",Tahoma,Verdana;font-size:13px;\\}
					h1 \\{color:#0099CC;\\}
					#intro \\{background-color:#CFEBF7;border:1px #2580B2 solid;padding:5px 13px 5px 13px;margin:10px;\\}
					#intro p \\{line-height:16.8667px;\\}
					td \\{font-size:11px;\\}
					th \\{text-align:left;padding-right:30px;font-size:11px;\\}
					tr.high \\{background-color:whitesmoke;\\}
					#footer \\{padding:2px;margin:10px;font-size:8pt;color:gray;\\}
					#footer a \\{color:gray;\\}
					a \\{color:black;\\}
				</style>
			</head>
			<body>
				<h1>XML Sitemap</h1>

				<div id="content">
					<table cellpadding="5">
						<tr style="border-bottom:1px black solid;">
							<th>URL</th>
							<th>Priority</th>
							<th>Change Frequency</th>
							<th>Last Change</th>
						</tr>
						<xsl:variable name="lower" select="'abcdefghijklmnopqrstuvwxyz'"/>
						<xsl:variable name="upper" select="'ABCDEFGHIJKLMNOPQRSTUVWXYZ'"/>
						<xsl:for-each select="sitemap:urlset/sitemap:url">
							<tr>
								<xsl:if test="position() mod 2 != 1">
									<xsl:attribute  name="class">high</xsl:attribute>
								</xsl:if>
								<td>
									<xsl:variable name="itemURL">
										<xsl:value-of select="sitemap:loc"/>
									</xsl:variable>
									<a href="\\{$itemURL\\}">
										<xsl:value-of select="sitemap:loc"/>
									</a>
								</td>
								<td>
									<xsl:value-of select="concat(sitemap:priority*100,'\\%')"/>
								</td>
								<td>
									<xsl:value-of select="concat(translate(substring(sitemap:changefreq, 1, 1),concat($lower, $upper),concat($upper, $lower)),substring(sitemap:changefreq, 2))"/>
								</td>
								<td>
									<xsl:value-of select="concat(substring(sitemap:lastmod,0,11),concat(' ', substring(sitemap:lastmod,12,5)))"/>
								</td>
							</tr>
						</xsl:for-each>
					</table>
				</div>
			</body>
		</html>
	</xsl:template>
</xsl:stylesheet>
```

6.制作sitemap模板文件，放在/templets/plus/sitemap.htm，在后台“更新sitemap”页面点击更新按钮即可生成sitemap.xml成功，如果主页不对了，记得重新生成动态主页。

```
<?xml version="1.0" encoding="UTF-8"?>
<?xml-stylesheet type="text/xsl" href="/templets/plus/sitemap.xsl"?>
<urlset xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://www.sitemaps.org/schemas/sitemap/0.9 http://www.sitemaps.org/schemas/sitemap/0.9/sitemap.xsd"
 xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
	<url>
		<loc>\\{dede:global.cfg_basehost/\\}</loc>
		<lastmod>\\{dede:arclist row=1 titlelen=24 orderby=pubdate\\}[field:pubdate
			function=strftime('\\%Y-\\%m-\\%d',@me)/]\\{/dede:arclist\\}</lastmod>
		<changefreq>always</changefreq>
		<priority>1.0</priority>
	</url>
	\\{dede:channel row='1000' type='top'\\}
	<url>
		<loc>[field:global.cfg_basehost/][field:typelink /]</loc>
		<changefreq>daily</changefreq>
		<priority>0.9</priority>
	</url>
	\\{/dede:channel\\}
	\\{dede:arclist row=2000 orderby=pubdate\\}
	<url>
		<loc>[field:global.cfg_basehost/][field:arcurl/]</loc>
		<lastmod>[field:pubdate function=strftime('\\%Y-\\%m-\\%d',@me)/]</lastmod>
		<changefreq>monthly</changefreq>
		<priority>0.8</priority>
	</url>
	\\{/dede:arclist\\}
</urlset>
```



### 织梦默认网站地图sitemap.html的优化

织梦自带的网站地图使用方法：织梦后台——生成——HTML更新——更新网站地图，可以在data目录下生成sitemap.html 。

缺点很明显：

1、生成的地图太简单，sitemap.html里面只有网站栏目列表，没有网站文章列表

2、sitemap.html生成的位置在data文件夹中，而data文件夹一般情况下为了安全是禁止访问的。

所以我们优化的工作就是让sitemap.html生成文章列表，并且生成在网站根目录。

以DEDECMS5.7为例：网站地图的模板sitemap.htm 在/templets/plus/目录里，就算在sitemap.htm中添加了织梦文章列表相关标签，也不能调用文章列表。

这是因为makehtml_map.php不能解析织梦的相关调用标签，我们可以稍作修改。让他实现调用任意标签。

备注：makehtml_map.php所在位置“根目录/dede/makehtml_map.php”

修改makehtml_map.php如下： 

（1）把require_once(DEDEINC."/dedetag.class.php");改成require_once(DEDEINC."/arc.partview.class.php");

（2）把

```
$dtp = new DedeTagParse();
$dtp->LoadTemplet($tmpfile);
$dtp->SaveTo($cfg_basedir.$murl);
```

改成

```
$dtp = new PartView();
$GLOBALS['_arclistEnv'] = 'index';
$dtp->SetTemplet($tmpfile);
$dtp->SaveToHtml($cfg_basedir.$murl);
```

（3）把$dtp->Clear();注释掉//$dtp->Clear();

（4）26行把$murl = $cfg_cmspath."/data/sitemap.html";改成$murl = $cfg_cmspath."/sitemap.html";

都改好之后就可以解析dedecms所有的标签了，包括文章列表标签。

用这种方法做的网站地图有个小问题，就是文章列表没有分页效果，所以需要设置的文章显示数量多一点。网站地图模板plus/sitemap.htm ，模板中改为下面的代码：

```
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
	<head>
		<meta http-equiv="Content-Type" content="text/html; charset=\\{dede:global name='cfg_soft_lang'/\\}" />
		<title>网站地图-\\{dede:global name='cfg_webname'/\\}</title>
		<link href="\\{dede:global name='cfg_templets_skin'/\\}/style/dedecms.css" rel="stylesheet" type="text/css" media="screen" />
	</head>
	<body class="mapspage">

		<div class="header">
			<div class="top w960 center">
				<div class="title">
					<h1>网站地图
						<a href="\\{dede:global name='cfg_basehost'/\\}" title="\\{dede:global name='cfg_webname'/\\}">
							<img src="/skin/images/logo.jpg" width="30" alt="\\{dede:global name='cfg_webname'/\\}" />
						</a></h1>
				</div><!-- /title -->
			</div><!-- /top -->
		</div><!-- /header -->

		<div class="w960 clear center mt1">
			<div class="sp-title">
				<span class="more">
				<a href='\\{dede:global name=' cfg_basehost'/\\}'>返回首页 </a> </span> </div> 							<h2>栏目列表</h2>
						\\{dede:global name='maplist'/\\}
						<h2>文章列表</h2>
						<ul>
							\\{dede:arclist typeid='' orderby=’pubdate’ row='999999' \\}
							<li><a href="[field:arcurl/]">[field:title/]</a></li>
							\\{/dede:arclist\\}
						</ul>
			</div>
	</body>
</html>
```

点击后台——生成——更新网站地图。查看：http://你的域名/sitemap.html ，就可以看到自己的sitemap.html了。



### 织梦404页面

单独做一个404页面，放在网站的根目录中，之后在服务器的控制面板中设置网站404即可。

可以参考https://404.life/里面有很多404模板，我用了腾讯公益的一个。

```
<!DOCTYPE html>
<html lang="zh">
	<head>
		<meta charset="UTF-8">
		<title>404页面-上品国际贸易</title>
		<script type="text/javascript" src="//qzonestyle.gtimg.cn/qzone/hybrid/app/404/search_children.js" charset="utf-8"
		 homePageUrl="http://www.baowen6.com" homePageName="回到我的主页"></script>
	</head>
	<body>

		<div class="footer">
			<p>Copyright (©) 2001-2020 吕梁上品国际贸易有限公司 All rights reserved. 备案号：晋ICP备19001386号</p>
			<p>24小时咨询电话：400-0358 396 QQ：470142287 邮箱：470142287@qq.com 地址：山西省吕梁市离石区徐家沟村口</p>
			<p>工业建材服务商-我们专注于生产：聚氨酯发泡保温材料、聚合物干混砂浆、聚苯乙烯泡沫制品</p>
		</div>
	</body>
</html>

```

第一步:在根目录创建一个文本文件，重命名为.htaccess，在里面添加如下语句:
ErrorDocument 404 /404.html
然后上传到wwwroot，如果网站目录本身就有这个文件，下载以后用编辑器打开添加上述规则即可。
第二步：上传自己的404文件，改名为404.html文件,也可以使用其他后缀,只要.htaccess中指定同样的文件就可以,例如ErrorDocument 404 /404.html



### PHP获取MySQL版本

后台主页“MySQL 版本”出错，将 **admin\templets\index_body.htm** 第80行代码改为如下

```
<?php
					$con = mysqli_connect("localhost","root","","baowen6");
					// 检测连接
					if (mysqli_connect_errno($con))
					\\{
					    echo "数据库连接失败: " . mysqli_connect_error();
					\\}
					echo "MySQL ".mysqli_get_server_info($con);
					mysqli_close($con);
					?>
```

mysqli_get_server_info() 函数返回 MySQL 服务器版本。 

- connection	

- - 必需。
  - 规定要使用的 MySQL 连接。

- 返回值

- - 返回一个表示 MySQL 服务器版本的字符串。



### 织梦dedecms文章列表页倒序排列方法

 在有些情况下 我们需要文章列表排序方式采用倒序排列； 
即先发表的文章排在最后一篇，那么dede通过什么标签来实现这个功能呢？ 
请看如下代码： 
\\{dede:arclist row='6' typeid='18' orderway='asc'\\}<li>;<a href="[field:arcurl/]">[field:title/]</a></li>\\{/dede:arclist\\} 
注意代码中红色标注位置 dede通过该标签来控制排序方式 
正常排列：orderway='asc' 
倒序排列：orderway='desc' 



### 更改织梦dedecms中文章ID的方法

 一次需要修改dede_archives表、dede_arctiny表、dede_addonarticle表所对应的文章前面的ID，才能真正实现修改ID；修改后，进入后台，刷新一下与全面静态化一次就好了！ 



### dedecms文章keywords关键词字数限制修改方法（同适用于描述）

最近在发布文章的时候发现文章关键词字数会有限制，如果填多了会自动截取，原来dedecms的关键字默认限制是60个字符也就是30个关键字，下边教您如何修改织梦程序关键字的字数限制，不管是新建网站还是老网站使用dedecms程序建议修改此项，本人亲测可行！

**第一步**

修改网站后台数据库的关键词字数限制，修改数据库之前建议备份一下！

进入数据库，查看dede_archives表，默认的关键字与摘要字段是：keywords此项值就是关键字可以看到后边是30，如果修改描述就修改description值，默认为255

点击进去将数值改为自己想要的，建议255一般都够用了！类型里面char修改为varchar，保存即可！

**第二步**

修改织梦程序后台管理目录dede中的2个文件：`article_add.php`和`article_edit.php`，

在里面分别搜索：搜索不到就搜索keywords即可找到

```
$keywords = cn_substrR($keywords,60);
```

将后面的数字60改成想要的数字。

**第三步**

修改管理目录dede中的`/inc/inc_archives_functions.php`文件，搜索代码：

```
if(strlen($keywords.$k)>=60
```

将后面的数字60改成想要的数字。

最后上传覆盖，清空缓存即可解除字数限制！



### 织梦文章排序orderby排序规则

栏目文章调用代码中orderby就是代表的文章的排序方法设置的代码值，orderby排序方式大致可以分为下面几种：

1，按点击数排序（orderby='hot' 或 orderby='click'），这个也就是我们在有些网站上看到的热门文章

2， 随机文档列表排序  orderby='rand'  也就是我们在有些网站看到随机推荐

3，按最后出现评论的时间排序  orderby=='lastpost'

4，按得分排序  orderby=='scores'

5，按文章ID排序  orderby='id'

6，按出版时间排序（orderby='sortrank' 或 orderby='pubdate' ）

其中上面六种，其中第一种和第二种是我们最常用的织梦文章排序方法。

下面我们为orderby的用法来举个实例说明下，代码如下：

```
<dl>
\\{dede:arclist row=5 titlelen=30 orderby='hot' \\}
<dd><a href='[field:arcurl/]' target="_blank">[field:title/]</a></dd>
\\{/dede:arclist\\} 
</dl>
```

上面这个就是热门文章的排序调用标签。



### DEDECMS数据库配置文件在哪?如何进行配置

有的朋友更换dede空间,dede数据库时,需要修改数据库配置.如数据库前缀,数据库名等.

那dede数据库配置文件在哪里找呢?

dede数据库配置文件所在路径为:/data/common.inc.php

修改方法:

把这个文件使用ftp下载下来,用记事本编辑.

下面是该dede数据库配置文件的内容:

```
$cfg_dbhost = 'localhost';网站地址
$cfg_dbname = 'data';数据库名
$cfg_dbuser = 'data_user';数据库用户名
$cfg_dbpwd = 'admin';数据库连接密码
$cfg_dbprefix = 'dede_';数据库前缀
$cfg_db_language = 'gbk';数据库语言版本
```



### 目录

　../a　默认生成文件存放目录

　../data　系统缓存或其他可写入数据存放目录

　../dede　默认后台登录管理（可任意改名）

　../images　系统默认的部分系统需要的图片目录

　../include　程序核心系统文件目录

　../install　安装文件目录

　../member　会员系统目录

　../plus　插件及辅助功能目录

　../special　专题目录

　../templets　模版目录

　../uploads　默认上传文件目录

　../index.php　网站默认动态首页文件

　../robots.txt　限定搜索引擎命令

　../tags.php　TAG标签文件



/data数据目录

  data ：数据目录存放后台信息，程序版本

　admin　系统后台常规配置，例如作者、快速导航、来源这些内容

　backupdata　数据库备份存放目录

　cache　系统缓存

　enums　联动类别生成的缓存和js文件

　js　栏目js调用生成的js文件

　mail　未明确

　mark　图片水印设置目录

　module　系统后台那些模块相关文件

　payment　在线支付的接口

　rss　生成RSSmap存放的文件目录

　safe　安全提问

　sessions　系统sessions存放目录

　tag　标签相关

　textdata　文本数据，系统后台保存为文本数据存放目录

　tplcache　模板缓存目录，这个缓存一般是那些动态页

　uploadtmp　未确定

　vote　默认投票文件

　ziptmp　压缩缓存目录

　common.inc.php　数据库连接信息

　余下文件打开即可判定

 

/dede后台目录

 

　css　后台界面样式文件

　images　后台界面图片文件

　inc　部分后台菜单名称配置

　js　后台JS效果文件

　templets　系统后台的模板存放目录

　下属各模版文件（以下代表的是文件开头前缀部分）

　　ad　广告管理模块

　　album　图片模型相关发布更改

　　apiUChome　整合文件

　　archives　通用文档相关发布更改

　　article　文章模型相关发布更改

　　ask　问答模块

　　cards　点卡管理

　　catalog　栏目相关管理

　　co　采集相关

　　diy　自定义表单

　　file　文件管理器

　　freelist　自由列表管理

　　friendlink　友情链接管理

　　group　圈子模块

　　index2　后台头部页面

　　index_menu2　左侧总菜单

　　login　登录界面

　　mail　邮件功能

　　makehtml　生成更新

　　media　上传数据菜单

　　member　会员管理

　　module　模块制作

　　images　目录基本可以删除

 

/include目录

config_base.php 环境定义文件。用于检测系统环境，定义工作目录，保存数据库链接信息，引入常用函数等，建议不要修改。

config_hand.php 系统配置文件。定义系统常用的配置信息定义，可从后台管理直接生成该文件。

config_passport.php 通行证文件

config_rglobals.php 检测系统外部变量

config_rglobals_magic.php 同上

inc_archives_view.php 用于浏览文档或对文档生成HTML

inc_arclist_view.php 用于浏览频道列表或对内容列表生成HTML

inc_arcmember_view.php 用于浏览会员发布的文档

inc_arcpart_view.php 用于解析和创建全局性质的模板，如频道封面，主页，单个页面等

inc_arcsearch_view.php 用于文档搜索

inc_arcspec_view.php 用于浏览所有专题列表或对专题列表生成HTML

inc_channel_unit.php 用户解析特定频道的附加数据结构信息

inc_channel_unit_functions.php 系统共用函数集合

inc_downclass.php 防采集随机字符串函数

inc_freelist_view.php 用于对特定内容列表生成HTML

inc_functions.php 可供用户使用的函数集合

inc_imgbt.php GetTypeidSelMember

inc_memberlogin.php 用于用户登录及获得会员状态

inc_photograph.php 用于处理系统中的图片，例如水印，缩略图等

inc_photowatermark_config.php 图片处理参数定义

inc_rss_view.php 用于浏览频道RSS或对RSS生成静态文件

inc_separate_functions.php SpGetArcList函数，用于获得文档列表

inc_sitemap.php 用于生成网站地图

inc_type_tree.php 用于选择栏目的目录树

inc_type_tree_member.php 同上，会员使用

inc_typelink.php 用于显示文章的位置和栏目位置等

inc_typeunit_admin.php 用于频道管理时的一些复杂操作，主要用于后台

inc_typeunit_menu.php 同上

inc_userlogin.php 用于管理员登录

inc_vote.php 用于管理投票

jump.php 用于超链接跳转

pub_charset.php 共用字符处理函数，GB/UTF-8/Unicode/BIG5等互换

pub_collection.php 用于采集

pub_collection_functions.php 采集用函数

pub_datalist.php 后台管理用数据列表

pub_datalist_dm.php 同上，不使用模板

pub_db_mysql.php 用于操作数据库

pub_dedehtml2.php 用于采集中的HTML解析

pub_dedehtml.php HTML解析器

pub_dedetag.php 用于dede模板标签解析

pub_httpdown.php 用于下载http中的资源

pub_oxwindow.php 后台程序扩展

pub_splitword_www.php 织梦分词算法

validateimg.php 验证码

vdimgck.php 验证码

/inc目录

inc_fun_funAdmin.php 获取拼音码等函数

inc_fun_funString.php html代码处理等函数

inc_fun_SpGetArcList.php 获取文档列表SpGetArcList

/install安装目录

 

/member会员中心目录

　plus　系统插件存放目录

　guestbook　留言板插件

　ad_js.php　广告插件

　advancedsearch.php　搜索

　bookfeedback.php　评论相关

　bookfeedback_js.php　评论相关

　bshare.php　分享

　car.php　购物车相关

　carbuyaction.php　购物车相关

　comments_frame.php　评论相关

　count.php　浏览次数等计数器

　digg_ajax.php　顶功能相关

　digg_frame.php　顶功能相关

　disdls.php　下载次数统计

　diy　自定义表单

　download.php　下载模块相关

　erraddsave.php　挑错

　feedback.php　评论相关

　feedback_ajax.php　评论相关

　feedback_js.php　评论相关

　flink.php　友情链接

　flink_add.php　友情链接添加

　freelist.php　自由列表

　guestbook.php　留言板

　posttocar.php　购物车相关

　recommend.php　推荐文章给好友

　stow.php　收藏功能

　task.php　计划任务功能

　view.php　文章阅读权限功能

　vote.php　投票功能

 

/special专题存放目录

 

/templets[织梦模板](http://www.dede58.com/)存放目录

/templets/default默认模板目录

article_article.htm 普通文章页面模板

article_default.htm 一般文档页面模板

article_flash.htm flash页面模板

article_image.htm 图集页面模板

article_soft.htm 软件页面模板

article_spec.htm 专题页面模板

index.htm 网站首页模板

index_article.htm 文章频道封面模板

index_article_webart1.htm

index_article_webart2.htm

index_article_webart.htm

index_default.htm 一般文档封面模板

index_flash.htm flash频道封面模板

index_image.htm 图集频道封面模板

index_soft.htm 软件频道封面模板

list_article.htm 文章列表模板

list_default.htm 一般文档列表目录模板

list_flash.htm flash文档列表模板

list_free.htm 自由列表模板

list_image.htm 图集列表模板

list_soft.htm 软件列表模板

list_spec.htm 专题列表模板

/templets/plus模板目录

download_links_templet.htm 下载链接模板

feedback_confirm.htm 评论确认模板

feedback_templet.htm 用户评论模板

feedback_templet_js.htm

flink-add.htm 友情链接添加模板

flink-list.htm 友情链接列表模板

guestbook.htm 留言本模板

heightsearch.htm 高级搜索模板

js.htm

recommend.htm 推荐好友模板

rss.htm RSS的XML模板

rssmap.htm RSS订阅文件

showphoto.htm 图片显示模板

sitemap.htm 网站地图模板

view_msg.htm 会员提示信息模板

vote.htm 投票结果显示模板

/uploads文件上传存放目录


