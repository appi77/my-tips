---
title: "windows TrustedInstaller 권한 관련 메시지 발생 시"
date: "No Date"
---

windows TrustedInstaller 권한 관련 메시지 발생 시
=======================================

by 
[박경원](https://appi77.github.io/my-tips/author/appi77/ "박경원이(가) 작성한 글")
·
Published 2018년 11월 30일
· Updated 2018년 11월 30일

하드디스크 교체 또는 계정 전환 후 권한 문제가 발생했을때  
CMD 명령어로 TrustedInstaller권한 해결 가능  
1. CMDa(관리자 권한)  
2. takeown /f c:\users\myid /a /r 명령어로 소유자 변경  
3. icacls c:\users\myid /grant administrators:f /t /l

이렇게 하면 권한이 바뀐다.

```html
<article class="post-485 post type-post status-publish format-standard hentry category-windows-"><div class="post-inner group">
<h1 class="post-title entry-title">windows TrustedInstaller 권한 관련 메시지 발생 시</h1>
<p class="post-byline">
   by   <span class="vcard author">
<span class="fn"><a href="https://appi77.github.io/my-tips/author/appi77/" rel="author" title="박경원이(가) 작성한 글">박경원</a></span>
</span>
   ·
                                Published <time class="published" datetime="2018년 11월 30일">2018년 11월 30일</time>
              · Updated <time class="updated" datetime="2018년 11월 30일">2018년 11월 30일</time></p>
<div class="clear"></div>
<div class="entry themeform">
<div class="entry-inner">
<p>하드디스크 교체 또는 계정 전환 후 권한 문제가 발생했을때<br/>
CMD 명령어로 TrustedInstaller권한 해결 가능<br/>
1. CMDa(관리자 권한)<br/>
2. takeown /f c:\users\myid /a /r 명령어로 소유자 변경<br/>
3. icacls c:\users\myid /grant administrators:f /t /l</p>
<p>이렇게 하면 권한이 바뀐다.</p>
<nav class="pagination group"></nav></div>
<div class="clear"></div>
</div>
</div>
</article>
```
