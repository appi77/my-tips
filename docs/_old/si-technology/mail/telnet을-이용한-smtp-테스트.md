---
title: "telnet을 이용한 smtp 테스트"
date: "No Date"
---

telnet을 이용한 smtp 테스트
====================

by 
[박경원](https://appi77.github.io/my-tips/author/appi77/ "박경원이(가) 작성한 글")
·
2016년 6월 30일

비인증방식  
telnet www.example.com 25  
HELO mydomain.com  
MAIL FROM:   
RCPT TO:   
data  
To: friend  
From: myname  
Subject: mail test

Hello,  
This is a test.  
Goodbye.  
.  
quit

인증 방식 (AUTH LOGIN 다음에 메일주소와 암호를 Base 64변환하여 넣는다 – http://ostermiller.org/calc/encode.html )  
telnet www.example.com 25  
HELO  
AUTH LOGIN  
ZWNtYWRtaW5AcG9vbmdzYW4uY28ua3I=  
ZWNtYWRtaW4=  
MAIL FROM:   
RCPT TO:   
data  
To: friend  
From: myname  
Subject: mail test

Hello,  
This is a test.  
Goodbye.  
.  
quit

```html
<article class="post-53 post type-post status-publish format-standard hentry category-mail"><div class="post-inner group">
<h1 class="post-title entry-title">telnet을 이용한 smtp 테스트</h1>
<p class="post-byline">
   by   <span class="vcard author">
<span class="fn"><a href="https://appi77.github.io/my-tips/author/appi77/" rel="author" title="박경원이(가) 작성한 글">박경원</a></span>
</span>
   ·
                                <time class="published" datetime="2016년 6월 30일">2016년 6월 30일</time></p>
<div class="clear"></div>
<div class="entry themeform">
<div class="entry-inner">
<p>비인증방식<br/>
telnet www.example.com 25<br/>
HELO mydomain.com<br/>
MAIL FROM: <sender@mydomain.com><br/>
RCPT TO: <friend@example.com><br/>
data<br/>
To: friend<friend@example.com><br/>
From: myname<sender@mydomain.com><br/>
Subject: mail test</sender@mydomain.com></friend@example.com></friend@example.com></sender@mydomain.com></p>
<p>Hello,<br/>
This is a test.<br/>
Goodbye.<br/>
.<br/>
quit</p>
<p>인증 방식 (AUTH LOGIN 다음에 메일주소와 암호를 Base 64변환하여 넣는다 – http://ostermiller.org/calc/encode.html )<br/>
telnet www.example.com 25<br/>
HELO<br/>
AUTH LOGIN<br/>
ZWNtYWRtaW5AcG9vbmdzYW4uY28ua3I=<br/>
ZWNtYWRtaW4=<br/>
MAIL FROM: <sender@mydomain.com><br/>
RCPT TO: <friend@example.com><br/>
data<br/>
To: friend<friend@example.com><br/>
From: myname<sender@mydomain.com><br/>
Subject: mail test</sender@mydomain.com></friend@example.com></friend@example.com></sender@mydomain.com></p>
<p>Hello,<br/>
This is a test.<br/>
Goodbye.<br/>
.<br/>
quit</p>
<nav class="pagination group"></nav></div>
<div class="clear"></div>
</div>
</div>
</article>
```
