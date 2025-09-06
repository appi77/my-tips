---
title: "Tomcat 튜닝"
date: "No Date"
---

Tomcat 튜닝
=========

by 
[박경원](https://appi77.github.io/my-tips/author/appi77/ "박경원이(가) 작성한 글")
·
2016년 7월 20일

server.xml 변경

Tomcat7W.exe 에서 Java탭 java Option 에 추가  
-Djava.awt.headless=true -Dfile.encoding=UTF-8 -server -Xms1024m -Xmx1024m -XX:NewSize=512m -XX:MaxNewSize=512m -XX:PermSize=512m -XX:MaxPermSize=1024m -XX:+DisableExplicitGC

```html
<article class="post-173 post type-post status-publish format-standard hentry category-was"><div class="post-inner group">
<h1 class="post-title entry-title">Tomcat 튜닝</h1>
<p class="post-byline">
   by   <span class="vcard author">
<span class="fn"><a href="https://appi77.github.io/my-tips/author/appi77/" rel="author" title="박경원이(가) 작성한 글">박경원</a></span>
</span>
   ·
                                <time class="published" datetime="2016년 7월 20일">2016년 7월 20일</time></p>
<div class="clear"></div>
<div class="entry themeform">
<div class="entry-inner">
<p>server.xml 변경<br/><br/><listener checkedosusers="root" classname="org.apache.catalina.security.SecurityListener"></listener></p>
<p> <br/><connector acceptcount="100" address="localhost" compressablemimetype="text/html,text/xml,text/plain,application/octet-stream" compression="500" connectiontimeout="20000" disableuploadtimeout="true" emptysessionpath="true" enablelookups="false" maxhttpheadersize="8192" maxthreads="250" port="80" protocol="HTTP/1.1" redirectport="8443" uriencoding="utf-8"></connector></p>
<p>Tomcat7W.exe 에서 Java탭 java Option 에 추가<br/>
-Djava.awt.headless=true -Dfile.encoding=UTF-8 -server -Xms1024m -Xmx1024m -XX:NewSize=512m -XX:MaxNewSize=512m -XX:PermSize=512m -XX:MaxPermSize=1024m -XX:+DisableExplicitGC</p>
<nav class="pagination group"></nav></div>
<div class="clear"></div>
</div>
</div>
</article>
```
