---
title: "윈도우10 OneDrive 삭제 방법"
date: "No Date"
---

윈도우10 OneDrive 삭제 방법
====================

by 
[박경원](https://appi77.github.io/my-tips/author/appi77/ "박경원이(가) 작성한 글")
·
2019년 11월 19일

set x86=”%SYSTEMROOT%\System32\OneDriveSetup.exe”  
set x64=”%SYSTEMROOT%\SysWOW64\OneDriveSetup.exe”

echo Closing the OneDrive process.  
echo.  
taskkill /f /im OneDrive.exe > NUL 2>&1  
ping 127.0.0.1 -n 5 > NUL 2>&1

echo Uninstalling OneDrive…  
echo.  
if exist %x64% (  
%x64% /uninstall  
) else (  
%x86% /uninstall  
)  
ping 127.0.0.1 -n 5 > NUL 2>&1

echo Removing OneDrive leftovers…  
echo.  
rd “%USERPROFILE%\OneDrive” /Q /S > NUL 2>&1  
rd “C:\OneDriveTemp” /Q /S > NUL 2>&1  
rd “%LOCALAPPDATA%\Microsoft\OneDrive” /Q /S > NUL 2>&1  
rd “%PROGRAMDATA%\Microsoft OneDrive” /Q /S > NUL 2>&1

echo Removing OneDrive from the Windows Explorer Side Panel…  
echo.  
REG DELETE “HKEY\_CLASSES\_ROOT\CLSID\{018D5C66-4533-4307-9B53-224DE2ED1FE6}” /f > NUL 2>&1  
REG DELETE “HKEY\_CLASSES\_ROOT\Wow6432Node\CLSID\{018D5C66-4533-4307-9B53-224DE2ED1FE6}” /f > NUL 2>&1

```html
<article class="post-1578 post type-post status-publish format-standard hentry category-pc-"><div class="post-inner group">
<h1 class="post-title entry-title">윈도우10 OneDrive 삭제 방법</h1>
<p class="post-byline">
   by   <span class="vcard author">
<span class="fn"><a href="https://appi77.github.io/my-tips/author/appi77/" rel="author" title="박경원이(가) 작성한 글">박경원</a></span>
</span>
   ·
                                <time class="published" datetime="2019년 11월 19일">2019년 11월 19일</time></p>
<div class="clear"></div>
<div class="entry themeform">
<div class="entry-inner">
<p>set x86=”%SYSTEMROOT%\System32\OneDriveSetup.exe”<br/>
set x64=”%SYSTEMROOT%\SysWOW64\OneDriveSetup.exe”</p>
<p>echo Closing the OneDrive process.<br/>
echo.<br/>
taskkill /f /im OneDrive.exe &gt; NUL 2&gt;&amp;1<br/>
ping 127.0.0.1 -n 5 &gt; NUL 2&gt;&amp;1</p>
<p>echo Uninstalling OneDrive…<br/>
echo.<br/>
if exist %x64% (<br/>
%x64% /uninstall<br/>
) else (<br/>
%x86% /uninstall<br/>
)<br/>
ping 127.0.0.1 -n 5 &gt; NUL 2&gt;&amp;1</p>
<p>echo Removing OneDrive leftovers…<br/>
echo.<br/>
rd “%USERPROFILE%\OneDrive” /Q /S &gt; NUL 2&gt;&amp;1<br/>
rd “C:\OneDriveTemp” /Q /S &gt; NUL 2&gt;&amp;1<br/>
rd “%LOCALAPPDATA%\Microsoft\OneDrive” /Q /S &gt; NUL 2&gt;&amp;1<br/>
rd “%PROGRAMDATA%\Microsoft OneDrive” /Q /S &gt; NUL 2&gt;&amp;1</p>
<p>echo Removing OneDrive from the Windows Explorer Side Panel…<br/>
echo.<br/>
REG DELETE “HKEY_CLASSES_ROOT\CLSID\{018D5C66-4533-4307-9B53-224DE2ED1FE6}” /f &gt; NUL 2&gt;&amp;1<br/>
REG DELETE “HKEY_CLASSES_ROOT\Wow6432Node\CLSID\{018D5C66-4533-4307-9B53-224DE2ED1FE6}” /f &gt; NUL 2&gt;&amp;1</p>
<nav class="pagination group"></nav></div>
<div class="clear"></div>
</div>
</div>
</article>
```
