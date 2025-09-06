---
title: "No Title"
date: "2018-11-30"
---

[Windows 문제해결](https://appi77.github.io/my-tips/category/si-technology/windows-%eb%ac%b8%ec%a0%9c%ed%95%b4%ea%b2%b0/)

2018년 11월 30일

 by 
[박경원](https://appi77.github.io/my-tips/author/appi77/ "박경원이(가) 작성한 글")
 · Published 2018년 11월 30일

[Windows 10 기본 앱 삭제 방법](https://appi77.github.io/my-tips/si-technology/windows-%eb%ac%b8%ec%a0%9c%ed%95%b4%ea%b2%b0/windows-10-%ea%b8%b0%eb%b3%b8-%ec%95%b1-%ec%82%ad%ec%a0%9c-%eb%b0%a9%eb%b2%95/ "Permalink to Windows 10 기본 앱 삭제 방법")
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Powershell.exe 실행 후 하당 목록에서 삭제할 프로그램 제거 하시면 됩니다. (ex. Get-AppxPackage \*3dbuilder\* | Remove-AppxPackage ) 3D Builder(3D빌더) Get-AppxPackage \*3dbuilder\* | Remove-AppxPackage Alarms and Clock(알람 앤 클락) Get-AppxPackage \*windowsalarms\* | Remove-AppxPackage Calculator(계산기) Get-AppxPackage \*windowscalculator\*...

```html
<article class="group grid-item post-481 post type-post status-publish format-standard hentry category-windows-" id="post-481"><div class="post-inner post-hover">
<div class="post-thumbnail">
<a href="https://appi77.github.io/my-tips/si-technology/windows-%eb%ac%b8%ec%a0%9c%ed%95%b4%ea%b2%b0/windows-10-%ea%b8%b0%eb%b3%b8-%ec%95%b1-%ec%82%ad%ec%a0%9c-%eb%b0%a9%eb%b2%95/">
</a>
</div>
<div class="post-meta group">
<p class="post-category"><a href="https://appi77.github.io/my-tips/category/si-technology/windows-%eb%ac%b8%ec%a0%9c%ed%95%b4%ea%b2%b0/" rel="category tag">Windows 문제해결</a></p>
<p class="post-date">
<time class="published updated" datetime="2018-11-30 13:22:53">2018년 11월 30일</time></p>
<p class="post-byline" style="display:none"> by    <span class="vcard author">
<span class="fn"><a href="https://appi77.github.io/my-tips/author/appi77/" rel="author" title="박경원이(가) 작성한 글">박경원</a></span>
</span> · Published <span class="published">2018년 11월 30일</span>
</p>
</div>
<h2 class="post-title entry-title">
<a href="https://appi77.github.io/my-tips/si-technology/windows-%eb%ac%b8%ec%a0%9c%ed%95%b4%ea%b2%b0/windows-10-%ea%b8%b0%eb%b3%b8-%ec%95%b1-%ec%82%ad%ec%a0%9c-%eb%b0%a9%eb%b2%95/" rel="bookmark" title="Permalink to Windows 10 기본 앱 삭제 방법">Windows 10 기본 앱 삭제 방법</a>
</h2>
<div class="entry excerpt entry-summary">
<p>Powershell.exe 실행 후 하당 목록에서 삭제할 프로그램 제거 하시면 됩니다. (ex. Get-AppxPackage *3dbuilder* | Remove-AppxPackage ) 3D Builder(3D빌더) Get-AppxPackage *3dbuilder* | Remove-AppxPackage Alarms and Clock(알람 앤 클락) Get-AppxPackage *windowsalarms* | Remove-AppxPackage Calculator(계산기) Get-AppxPackage *windowscalculator*...</p>
</div>
</div>
</article>
```
