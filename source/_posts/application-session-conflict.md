title: "应用的Session冲突"
id: 201
date: 2012-12-26 15:09:23
tags: 
- Java
- Tomcat
- Weblogic
- Websphere
categories: 
- 服务器
---

<span style="font-size: 16px;">使用apache反向代理解决在应用A使用Iframe嵌入应用B的功能而产生的跨域问题后，应用B的功能能正常使用了。但也产生了另外一个问题：打开应用A的任何页面都会跳转主页，问题原因是：session丢失。</span>
<div></div>
<div><span style="font-size: 16px;">**具体分析：**</span></div>
<!--more-->

<span style="font-family: 微软雅黑; color: #000000; font-size: 16px;">session是通过在客户端生成一个cookie，所有请求会带上这个cookie。一个cookie的NAME、Domain和Path属性值均相同，则会覆盖，若未设置Domain域，则域为ip（不包括端口），因此应用A的session被应用B的session覆盖了。</span>

&nbsp;

<span style="font-family: 微软雅黑; color: #000000; font-size: 16px;">经测试：tomcat、weblogic、websphere的session默认都是JSESSIONID 为key来识别的，因此在没有特别设置下，同一个域下的多个应用session会互相覆盖。 </span>

**<span style="font-family: 微软雅黑; color: #000000; font-size: 16px;">解决办法：</span>**

<span style="background-color: #ffffff; color: #555554;">设置各个应用使用不同的cookie-name，或者将JSESSIONID的path路径设置为不同。</span>

<span style="background-color: #ffffff; color: #555554;">1）</span><span style="background-color: #ffffff; color: #555554;">WebLogic的Cookie相关配置：<span style="background-color: #ffffff; color: #555554;">weblogic.xml</span></span>

<table border="1">
<tbody>
<tr style="text-align: left; widows: 2; text-transform: none; background-color: #ffffff; text-indent: 0px; font: 14px/25px Arial, Helvetica, simsun, u5b8bu4f53; white-space: normal; orphans: 2; letter-spacing: normal; color: #555554; word-spacing: 0px; -webkit-text-size-adjust: auto; -webkit-text-stroke-width: 0px;">
<td style="line-height: 25px;">

属性名

</td>
<td style="line-height: 25px;">默认值</td>
<td style="line-height: 25px;">值</td>
</tr>
<tr style="text-align: left; widows: 2; text-transform: none; background-color: #ffffff; text-indent: 0px; font: 14px/25px Arial, Helvetica, simsun, u5b8bu4f53; white-space: normal; orphans: 2; letter-spacing: normal; color: #555554; word-spacing: 0px; -webkit-text-size-adjust: auto; -webkit-text-stroke-width: 0px;">
<td style="line-height: 25px;">cookie-name</td>
<td style="line-height: 25px;">JSESSIONID</td>
<td style="line-height: 25px;">如未设置，默认为“JSESSIONID”</td>
</tr>
<tr style="text-align: left; widows: 2; text-transform: none; background-color: #ffffff; text-indent: 0px; font: 14px/25px Arial, Helvetica, simsun, u5b8bu4f53; white-space: normal; orphans: 2; letter-spacing: normal; color: #555554; word-spacing: 0px; -webkit-text-size-adjust: auto; -webkit-text-stroke-width: 0px;">
<td style="line-height: 25px;">cookie-path</td>
<td style="line-height: 25px;">NULL</td>
<td style="line-height: 25px;">如未设置，默认为“/”</td>
</tr>
<tr style="text-align: left; widows: 2; text-transform: none; background-color: #ffffff; text-indent: 0px; font: 14px/25px Arial, Helvetica, simsun, u5b8bu4f53; white-space: normal; orphans: 2; letter-spacing: normal; color: #555554; word-spacing: 0px; -webkit-text-size-adjust: auto; -webkit-text-stroke-width: 0px;">
<td style="line-height: 25px;">cookie-domain</td>
<td style="line-height: 25px;">NULL</td>
<td style="line-height: 25px;">如未设置，默认为发放cookie的服务器的域</td>
</tr>
</tbody>
</table>
<div><span style="background-color: #ffffff; color: #555554; font-size: 16px;">示例代码：  </span></div>
<div>
<pre style="overflow-x: auto;"><span style="text-align: right; padding-bottom: 0px; margin: -2px 10px 0px 0px; padding-left: 10px; padding-right: 10px; color: #000; border-right: #ccc 5px solid; padding-top: 2px;">1.  </span>&lt;<span style="color: #808000;">session-descriptor</span>&gt; 
<span style="text-align: right; padding-bottom: 0px; margin: -5px 10px 0px 0px; padding-left: 10px; padding-right: 10px; color: #000; border-right: #ccc 5px solid; padding-top: 4px;">2.  </span>&lt;<span style="color: #808000;">session-param</span>&gt; 
<span style="text-align: right; padding-bottom: 0px; margin: -5px 10px 0px 0px; padding-left: 10px; padding-right: 10px; color: #000; border-right: #ccc 5px solid; padding-top: 4px;">3.  </span>&lt;<span style="color: #808000;">param-name</span>&gt;CookieName&lt;<span style="color: #808000;">/param-name</span>&gt; 
<span style="text-align: right; padding-bottom: 0px; margin: -5px 10px 0px 0px; padding-left: 10px; padding-right: 10px; color: #000; border-right: #ccc 5px solid; padding-top: 4px;">4.  </span>&lt;<span style="color: #808000;">param-value</span>&gt;XXX_SESSIONID&lt;<span style="color: #808000;">/param-value</span>&gt;</pre>
<pre style="overflow-x: auto;"><span style="text-align: right; padding-bottom: 0px; margin: -5px 10px 0px 0px; padding-left: 10px; padding-right: 10px; color: #000; border-right: #ccc 5px solid; padding-top: 4px;">5.  </span>&lt;<span style="color: #808000;">/session-param</span>&gt; 
<span style="text-align: right; padding-bottom: 0px; margin: -5px 10px 0px 0px; padding-left: 10px; padding-right: 10px; color: #000; border-right: #ccc 5px solid; padding-top: 4px;">6.  </span>&lt;<span style="color: #808000;">/session-descriptor</span>&gt;</pre>
</div>
<div></div>
<div></div>
<div><span style="color: #404040; font-size: 16px;">延伸阅读：</span></div>
<div><span style="color: #404040; font-size: 16px;">1. </span><span style="color: #404040; font-size: 16px;">[关于WebLogic的Session丢失的问题](http://blog.csdn.net/designlife/article/details/2552186) </span><span style="background-color: #ffffff; color: #2c2c2c;">[<span style="background-color: #ffffff; color: #404040; font-size: 16px;">http://blog.csdn.net/DesignLife/article/details/2552186</span>](http://blog.csdn.net/DesignLife/article/details/2552186)</span></div>
<div><span style="background-color: #ffffff; color: #2c2c2c;"><span style="background-color: #ffffff; color: #404040; font-size: 16px;"> 2. WebLogic如何设置session超时时间 </span>[<span style="background-color: #ffffff; color: #404040; font-size: 16px;">http://tonyaction.blog.51cto.com/227462/201900</span>](http://tonyaction.blog.51cto.com/227462/201900)</span></div>
<div><span style="color: #404040;"> </span></div>
<div><span style="color: #404040;"> </span></div>
<div>

<span style="font-family: Arial; color: #000000; font-size: 16px;">2）websphere的设置（设置不同JSESSIONID的path）</span>

<span style="color: #000000; font-size: 16px;">应用程序-&gt;企业应用程序-&gt; [Application Server] -&gt;</span>
<span style="color: #000000; font-size: 16px;">会话管理-&gt;1.覆盖会话管理(需打钩).</span>
<span style="color: #000000; font-size: 16px;">会话管理-&gt;2.启用 cookie(需打钩)-&gt;修改'Cookie路径' </span>

</div>
![websphere设置](/images/2012/1226/websphere-setting.png)

&nbsp;

**3）Tomcat的设置（设置不同JSESSIONID的path）**

<span style="background-color: #ffffff; color: #555554;">修改tomcat/conf/server.xml：<span class="Apple-converted-space" style="font-family: Arial;"> </span></span>

&nbsp;

**1.tomcat5修改方法**

在启动项中增加org.apache.catalina.SESSION_COOKIE_NAME参数
linux
```
JAVA_OPTS='-Dorg.apache.catalina.SESSION_COOKIE_NAME=yousessionname'
```

win
```
set JAVA_OPTS='-Dorg.apache.catalina.SESSION_COOKIE_NAME=yousessionname'
```

**2.tomcat6和tomcat7修改方法相同**

在Context容器标签上增加sessionCookieName参数

&lt;Context path=”/” docBase=”webapp” reloadable=”false” <span style="color: #ff0000;">sessionCookieName=”yoursessionname”</span>&gt;&lt;/Context&gt;

还可以加上sessionCookiePath

<span style="background-color: #ffffff; color: #555554;"><span style="background-color: #ffffff; color: #555554;">&lt;Context ... sessionCookiePath="/" &gt; ... &lt;/Context&gt;<span class="Apple-converted-space" style="font-family: Arial;"> </span></span></span>


<span style="background-color: #ffffff; color: #555554;"><span style="background-color: #ffffff; color: #555554;"><span class="Apple-converted-space" style="font-family: Arial;">延伸阅读：tomcat修改jsessionid在cookie中的名称 [http://blog.shilimin.com/338.htm](http://blog.shilimin.com/338.htm)</span></span></span>


<div>[通过 为知笔记 发布](http://www.wiz.cn/ "为知笔记")</div>