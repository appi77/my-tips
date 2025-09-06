---
title: "DA 설정"
date: "No Date"
---

DA 설정
=====

by 
[박경원](https://appi77.github.io/my-tips/author/appi77/ "박경원이(가) 작성한 글")
·
2016년 6월 30일

Session timeout .  
\WEB-INF\web.xml 의 를 수정한다.  
예를 들어 :  
  
300

300분 동안 요청이 없으면 session-timeout

```html
<article class="post-11 post type-post status-publish format-standard hentry category-configration"><div class="post-inner group">
<h1 class="post-title entry-title">DA 설정</h1>
<p class="post-byline">
   by   <span class="vcard author">
<span class="fn"><a href="https://appi77.github.io/my-tips/author/appi77/" rel="author" title="박경원이(가) 작성한 글">박경원</a></span>
</span>
   ·
                                <time class="published" datetime="2016년 6월 30일">2016년 6월 30일</time></p>
<div class="clear"></div>
<div class="entry themeform">
<div class="entry-inner">
<p>Session timeout .<br/>
<web-app>\WEB-INF\web.xml 의 <session-config>를 수정한다.<br/>
예를 들어 :<br/>
<session-config><br/>
<session-timeout>300</session-timeout><br/>
</session-config></session-config></web-app></p>
<p>300분 동안 요청이 없으면 session-timeout</p>
<nav class="pagination group"></nav></div>
<div class="clear"></div>
</div>
</div>
</article>
```
