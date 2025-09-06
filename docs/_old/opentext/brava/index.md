---
title: "livelink에서 brava preview 호출URL"
date: "No Date"
---

livelink에서 brava preview 호출URL
==============================

by 
[박경원](https://appi77.github.io/my-tips/author/appi77/ "박경원이(가) 작성한 글")
·
Published 2017년 11월 25일
· Updated 2018년 1월 24일

### 미리보기 목록 호출

http://192.168.10.47/livelink/cs?func=brava.preloadmarkups&nodeid=21243&docversion=1&popupid=preload21243

SQL) select dataid from dtreecore where parentid=21242  
21243  
SQL) select dataid, name from dtreecore where parentid=21243 and subtype=31444  
18492 1111  
35762 2222

### 열기로 열었을때

http://192.168.10.47/livelink/cs?func=brava.bravaviewer&src=preloadx&nodeid=21243&vernum=1&reviewNodes={%2218492-1%22}&nexturl=http%3A%2F%2F192%2E168%2E10%2E47%2Flivelink%2Fcs%3Ffunc%3Dll%26objId%3D21242%26objAction%3Dbrowse%26viewType%3D1&OpenInNewWin=\_blank&NewWinParam=resizable

열기로 열었을때 – 특수기호 빼면 ( %2E . %3A : %3F ? %2F / %22 ” %26 & ) http://192.168.10.47/livelink/cs?func=brava.bravaviewer&src=preloadx&nodeid=21243&vernum=1&reviewNodes={“218492-1”}&nexturl=http://192.168.10.47/livelink/cs?func=ll&objId=21242&objAction=browse&viewType=1&OpenInNewWin=\_blank&NewWinParam=resizable

해당파일이 있는 폴더를 찍었을떄  
http://192.168.10.47/livelink/cs?func=ll&objId=21242&objAction=browse&viewType=1

편집으로 열었을때
=========

http://192.168.10.47/livelink/cs?func=brava.bravaviewer&src=preloadx&nodeid=21243&vernum=1&editNode=18492-1&nexturl=http%3A%2F%2F192%2E168%2E10%2E47%2Flivelink%2Fcs%3Ffunc%3Dll%26objId%3D21242%26objAction%3Dbrowse%26viewType%3D1&OpenInNewWin=\_blank&NewWinParam=resizable

http://192.168.10.47/livelink/cs?func=brava.bravaviewer&src=preloadx&nodeid=21243&vernum=1&reviewNodes={“218492-1”}&nexturl=http://192.168.10.47/livelink/cs?func=ll&objId=21242&objAction=browse&viewType=1&OpenInNewWin=\_blank&NewWinParam=resizable

### 주석을 여러개 열었을때

http://192.168.10.47/livelink/cs?func=brava.bravaviewer&src=preloadx&nodeid=21243&vernum=1&reviewNodes={%2218492-1%22%2C%2235762-1%22}&nexturl=http%3A%2F%2F192%2E168%2E10%2E47%2Flivelink%2Fcs%3Ffunc%3Dll%26objId%3D21242%26objAction%3Dbrowse%26viewType%3D1&OpenInNewWin=\_blank&NewWinParam=resizable

### 이전주석과 편집으로 열었을때

http://192.168.10.47/livelink/cs?func=brava.bravaviewer&src=preloadx&nodeid=21243&vernum=1&editNode=35762-1&reviewNodes={%2218492-1%22}&nexturl=http%3A%2F%2F192%2E168%2E10%2E47%2Flivelink%2Fcs%3Ffunc%3Dll%26objId%3D21242%26objAction%3Dbrowse%26viewType%3D1&OpenInNewWin=\_blank&NewWinParam=resizable

```html
<article class="post-266 post type-post status-publish format-standard hentry category-brava"><div class="post-inner group">
<h1 class="post-title entry-title">livelink에서 brava preview 호출URL</h1>
<p class="post-byline">
   by   <span class="vcard author">
<span class="fn"><a href="https://appi77.github.io/my-tips/author/appi77/" rel="author" title="박경원이(가) 작성한 글">박경원</a></span>
</span>
   ·
                                Published <time class="published" datetime="2017년 11월 25일">2017년 11월 25일</time>
              · Updated <time class="updated" datetime="2018년 1월 24일">2018년 1월 24일</time></p>
<div class="clear"></div>
<div class="entry themeform">
<div class="entry-inner">
<h3>미리보기 목록 호출</h3>
<p>http://192.168.10.47/livelink/cs?func=brava.preloadmarkups&amp;nodeid=21243&amp;docversion=1&amp;popupid=preload21243</p>
<p>SQL) select dataid from dtreecore where parentid=21242<br/>
21243<br/>
SQL) select dataid, name from dtreecore where parentid=21243 and subtype=31444<br/>
18492 1111<br/>
35762 2222</p>
<h3>열기로 열었을때</h3>
<p>http://192.168.10.47/livelink/cs?func=brava.bravaviewer&amp;src=preloadx&amp;nodeid=21243&amp;vernum=1&amp;reviewNodes={%2218492-1%22}&amp;nexturl=http%3A%2F%2F192%2E168%2E10%2E47%2Flivelink%2Fcs%3Ffunc%3Dll%26objId%3D21242%26objAction%3Dbrowse%26viewType%3D1&amp;OpenInNewWin=_blank&amp;NewWinParam=resizable</p>
<p>열기로 열었을때 – 특수기호 빼면 ( %2E . %3A : %3F ? %2F / %22 ” %26 &amp; ) http://192.168.10.47/livelink/cs?func=brava.bravaviewer&amp;src=preloadx&amp;nodeid=21243&amp;vernum=1&amp;reviewNodes={“218492-1”}&amp;nexturl=http://192.168.10.47/livelink/cs?func=ll&amp;objId=21242&amp;objAction=browse&amp;viewType=1&amp;OpenInNewWin=_blank&amp;NewWinParam=resizable</p>
<p>해당파일이 있는 폴더를 찍었을떄<br/>
http://192.168.10.47/livelink/cs?func=ll&amp;objId=21242&amp;objAction=browse&amp;viewType=1</p>
<h1>편집으로 열었을때</h1>
<p>http://192.168.10.47/livelink/cs?func=brava.bravaviewer&amp;src=preloadx&amp;nodeid=21243&amp;vernum=1&amp;editNode=18492-1&amp;nexturl=http%3A%2F%2F192%2E168%2E10%2E47%2Flivelink%2Fcs%3Ffunc%3Dll%26objId%3D21242%26objAction%3Dbrowse%26viewType%3D1&amp;OpenInNewWin=_blank&amp;NewWinParam=resizable</p>
<p>http://192.168.10.47/livelink/cs?func=brava.bravaviewer&amp;src=preloadx&amp;nodeid=21243&amp;vernum=1&amp;reviewNodes={“218492-1”}&amp;nexturl=http://192.168.10.47/livelink/cs?func=ll&amp;objId=21242&amp;objAction=browse&amp;viewType=1&amp;OpenInNewWin=_blank&amp;NewWinParam=resizable</p>
<h3>주석을 여러개 열었을때</h3>
<p>http://192.168.10.47/livelink/cs?func=brava.bravaviewer&amp;src=preloadx&amp;nodeid=21243&amp;vernum=1&amp;reviewNodes={%2218492-1%22%2C%2235762-1%22}&amp;nexturl=http%3A%2F%2F192%2E168%2E10%2E47%2Flivelink%2Fcs%3Ffunc%3Dll%26objId%3D21242%26objAction%3Dbrowse%26viewType%3D1&amp;OpenInNewWin=_blank&amp;NewWinParam=resizable</p>
<h3>이전주석과 편집으로 열었을때</h3>
<p>http://192.168.10.47/livelink/cs?func=brava.bravaviewer&amp;src=preloadx&amp;nodeid=21243&amp;vernum=1&amp;editNode=35762-1&amp;reviewNodes={%2218492-1%22}&amp;nexturl=http%3A%2F%2F192%2E168%2E10%2E47%2Flivelink%2Fcs%3Ffunc%3Dll%26objId%3D21242%26objAction%3Dbrowse%26viewType%3D1&amp;OpenInNewWin=_blank&amp;NewWinParam=resizable</p>
<nav class="pagination group"></nav></div>
<div class="clear"></div>
</div>
</div>
</article>
```
