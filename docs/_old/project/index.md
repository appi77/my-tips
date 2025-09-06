---
title: "No Title"
date: "2019-11-19"
---

[PC환경 수정](https://appi77.github.io/my-tips/category/project/pc%ed%99%98%ea%b2%bd-%ec%88%98%ec%a0%95/)

2019년 11월 19일

 by 
[박경원](https://appi77.github.io/my-tips/author/appi77/ "박경원이(가) 작성한 글")
 · Published 2019년 11월 19일

[윈도우10 OneDrive 삭제 방법](https://appi77.github.io/my-tips/project/pc%ed%99%98%ea%b2%bd-%ec%88%98%ec%a0%95/%ec%9c%88%eb%8f%84%ec%9a%b010-onedrive-%ec%82%ad%ec%a0%9c-%eb%b0%a9%eb%b2%95/ "Permalink to 윈도우10 OneDrive 삭제 방법")
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

set x86=”%SYSTEMROOT%\System32\OneDriveSetup.exe” set x64=”%SYSTEMROOT%\SysWOW64\OneDriveSetup.exe” echo Closing the OneDrive process. echo. taskkill /f /im OneDrive.exe > NUL 2>&1 ping 127.0.0.1 -n 5 > NUL 2>&1 echo Uninstalling OneDrive… echo. if exist %x64% ( %x64% /uninstall...

```html
<article class="group grid-item post-1578 post type-post status-publish format-standard hentry category-pc-" id="post-1578"><div class="post-inner post-hover">
<div class="post-thumbnail">
<a href="https://appi77.github.io/my-tips/project/pc%ed%99%98%ea%b2%bd-%ec%88%98%ec%a0%95/%ec%9c%88%eb%8f%84%ec%9a%b010-onedrive-%ec%82%ad%ec%a0%9c-%eb%b0%a9%eb%b2%95/">
</a>
</div>
<div class="post-meta group">
<p class="post-category"><a href="https://appi77.github.io/my-tips/category/project/pc%ed%99%98%ea%b2%bd-%ec%88%98%ec%a0%95/" rel="category tag">PC환경 수정</a></p>
<p class="post-date">
<time class="published updated" datetime="2019-11-19 21:19:29">2019년 11월 19일</time></p>
<p class="post-byline" style="display:none"> by    <span class="vcard author">
<span class="fn"><a href="https://appi77.github.io/my-tips/author/appi77/" rel="author" title="박경원이(가) 작성한 글">박경원</a></span>
</span> · Published <span class="published">2019년 11월 19일</span>
</p>
</div>
<h2 class="post-title entry-title">
<a href="https://appi77.github.io/my-tips/project/pc%ed%99%98%ea%b2%bd-%ec%88%98%ec%a0%95/%ec%9c%88%eb%8f%84%ec%9a%b010-onedrive-%ec%82%ad%ec%a0%9c-%eb%b0%a9%eb%b2%95/" rel="bookmark" title="Permalink to 윈도우10 OneDrive 삭제 방법">윈도우10 OneDrive 삭제 방법</a>
</h2>
<div class="entry excerpt entry-summary">
<p>set x86=”%SYSTEMROOT%\System32\OneDriveSetup.exe” set x64=”%SYSTEMROOT%\SysWOW64\OneDriveSetup.exe” echo Closing the OneDrive process. echo. taskkill /f /im OneDrive.exe &gt; NUL 2&gt;&amp;1 ping 127.0.0.1 -n 5 &gt; NUL 2&gt;&amp;1 echo Uninstalling OneDrive… echo. if exist %x64% ( %x64% /uninstall...</p>
</div>
</div>
</article>
```
