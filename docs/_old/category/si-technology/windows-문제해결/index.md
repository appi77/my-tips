---
title: "No Title"
date: "2018-11-30"
---

[Windows 문제해결](https://appi77.github.io/my-tips/category/si-technology/windows-%eb%ac%b8%ec%a0%9c%ed%95%b4%ea%b2%b0/)

2018년 11월 30일

 by 
[박경원](https://appi77.github.io/my-tips/author/appi77/ "박경원이(가) 작성한 글")
 · Published 2018년 11월 30일

[windows TrustedInstaller 권한 관련 메시지 발생 시](https://appi77.github.io/my-tips/si-technology/windows-%eb%ac%b8%ec%a0%9c%ed%95%b4%ea%b2%b0/windows-trustedinstaller-%ea%b6%8c%ed%95%9c-%ea%b4%80%eb%a0%a8-%eb%a9%94%ec%8b%9c%ec%a7%80-%eb%b0%9c%ec%83%9d-%ec%8b%9c/ "Permalink to windows TrustedInstaller 권한 관련 메시지 발생 시")
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

하드디스크 교체 또는 계정 전환 후 권한 문제가 발생했을때 CMD 명령어로 TrustedInstaller권한 해결 가능 1. CMDa(관리자 권한) 2. takeown /f c:\users\myid /a /r 명령어로 소유자 변경 3. icacls c:\users\myid /grant administrators:f /t /l 이렇게...

```html
<article class="group grid-item post-485 post type-post status-publish format-standard hentry category-windows-" id="post-485"><div class="post-inner post-hover">
<div class="post-thumbnail">
<a href="https://appi77.github.io/my-tips/si-technology/windows-%eb%ac%b8%ec%a0%9c%ed%95%b4%ea%b2%b0/windows-trustedinstaller-%ea%b6%8c%ed%95%9c-%ea%b4%80%eb%a0%a8-%eb%a9%94%ec%8b%9c%ec%a7%80-%eb%b0%9c%ec%83%9d-%ec%8b%9c/">
</a>
</div>
<div class="post-meta group">
<p class="post-category"><a href="https://appi77.github.io/my-tips/category/si-technology/windows-%eb%ac%b8%ec%a0%9c%ed%95%b4%ea%b2%b0/" rel="category tag">Windows 문제해결</a></p>
<p class="post-date">
<time class="published updated" datetime="2018-11-30 15:28:55">2018년 11월 30일</time></p>
<p class="post-byline" style="display:none"> by    <span class="vcard author">
<span class="fn"><a href="https://appi77.github.io/my-tips/author/appi77/" rel="author" title="박경원이(가) 작성한 글">박경원</a></span>
</span> · Published <span class="published">2018년 11월 30일</span>
</p>
</div>
<h2 class="post-title entry-title">
<a href="https://appi77.github.io/my-tips/si-technology/windows-%eb%ac%b8%ec%a0%9c%ed%95%b4%ea%b2%b0/windows-trustedinstaller-%ea%b6%8c%ed%95%9c-%ea%b4%80%eb%a0%a8-%eb%a9%94%ec%8b%9c%ec%a7%80-%eb%b0%9c%ec%83%9d-%ec%8b%9c/" rel="bookmark" title="Permalink to windows TrustedInstaller 권한 관련 메시지 발생 시">windows TrustedInstaller 권한 관련 메시지 발생 시</a>
</h2>
<div class="entry excerpt entry-summary">
<p>하드디스크 교체 또는 계정 전환 후 권한 문제가 발생했을때 CMD 명령어로 TrustedInstaller권한 해결 가능 1. CMDa(관리자 권한) 2. takeown /f c:\users\myid /a /r 명령어로 소유자 변경 3. icacls c:\users\myid /grant administrators:f /t /l 이렇게...</p>
</div>
</div>
</article>
```
