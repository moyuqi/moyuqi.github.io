title: "更改host1free域名转向到.tk域名"
id: 39
date: 2012-01-07 22:53:45
tags: 
- host1free
- tk
- 域名
categories: 
- 网站域名
---

以前使用的是host1free的免费空间，当然啦，访问速度实在是不敢恭维，不过又没找到合适的空间转移，也就没有换了。

原本注册这个空间自带的域名为moyuiq.host898.net，我注册了hongen.tk域名，设置为自动转向。

这样设置有一个问题就是，不管我点击哪一篇文章，地址栏永远都是hongen.tk，不会改变。

<!--more-->

经过咨询 锋辉 童鞋后，当然，在他的帮助下，终于把域名转向设置好了。

首先：

1.到host1free
<pre>登录之后，点击website control--点击你的二级域名--Domain Setup--Add Another Domain，</pre>
<pre>然后在Domain处输入你的域名，点击create，之后会自动host1free会自动生成你绑定域名的a记录那些。</pre>
![](http://moyuqi-wordpress.stor.sinaapp.com/uploads/2012/01/wpid-d2649b925e2cf3200aa981359a577e37_11-300x331.png)
<pre>2.到dot.tk</pre>
<pre>修改域名信息-》使用DOT TK的免费DNS服务器，添加A记录，ip地址通过host1free后台的DNS Mangement查看到。</pre>
![](http://moyuqi-wordpress.stor.sinaapp.com/uploads/2012/01/wpid-d2649b925e2cf3200aa981359a577e37_2-300x1931.png)
<pre>3.登录FTP，在新建的hongen.tk域名文件下，把原域名里的wordpress文件夹拷贝过来</pre>
![](http://moyuqi-wordpress.stor.sinaapp.com/uploads/2012/01/wpid-d2649b925e2cf3200aa981359a577e37_3-300x1011.png)
<pre>4.登录wordpress后台，设置-》常规，修改wordpress地址 和站点地址。</pre>
<pre></pre>
![](http://moyuqi-wordpress.stor.sinaapp.com/uploads/2012/01/wpid-d2649b925e2cf3200aa981359a577e37_4-300x1941.png)
<div>[通过 Wiz 发布](http://www.wiz.cn/ "Wiz")</div>