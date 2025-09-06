---
title: "ASPECT 사용법"
date: "No Date"
---

ASPECT 사용법
==========

by 
[박경원](https://appi77.github.io/my-tips/author/appi77/ "박경원이(가) 작성한 글")
·
2016년 6월 30일

ASPECT TYPE 설치와 별개로 DQL과 API에서 사용하기 위한 DQL 및 API

ASPECT 속성추가 :  
ALTER ASPECT dm\_document\_aspect add years\_to\_retain int, level\_of\_security String(2) OPTIMIZEFETCH

ASPECT 속성 제거 :  
ALTER ASPECT dm\_document\_aspect drop level\_of\_security

TYPE에 ASPECT add :  
ALTER TYPE dm\_document add DEFAULT ASPECTS dm\_document\_aspect

ASPECT 속성 테스트 :  
SELECT r\_object\_id, dm\_document\_aspect.years\_to\_retain, dm\_document\_aspect.level\_of\_security  
FROM dm\_document WHERE dm\_document\_aspect.years\_to\_retain = 10

TYPE에 ASPECT remove :  
ALTER TYPE dm\_document REMOVE DEFAULT ASPECTS dm\_document\_aspect;

ASPECT 삭제 :  
ALTER ASPECT dm\_document\_aspect DROP ALL

iapi에서 ASPECT 사용예 :  
create,c,dm\_document  
set,c,l,a\_content\_type  
text  
set,c,l,object\_name  
test test3  
setfile,c,l,d:\temp\a.txt  
link,c,l,/Temp  
set,c,l,dm\_document\_aspect.level\_of\_security  
A  
set,c,l,dm\_document\_aspect.years\_to\_retain  
1  
save,c,l

```html
<article class="post-34 post type-post status-publish format-standard hentry category-maintenance"><div class="post-inner group">
<h1 class="post-title entry-title">ASPECT 사용법</h1>
<p class="post-byline">
   by   <span class="vcard author">
<span class="fn"><a href="https://appi77.github.io/my-tips/author/appi77/" rel="author" title="박경원이(가) 작성한 글">박경원</a></span>
</span>
   ·
                                <time class="published" datetime="2016년 6월 30일">2016년 6월 30일</time></p>
<div class="clear"></div>
<div class="entry themeform">
<div class="entry-inner">
<p>ASPECT TYPE 설치와 별개로 DQL과 API에서 사용하기 위한 DQL 및 API</p>
<p>ASPECT 속성추가 :<br/>
ALTER ASPECT dm_document_aspect add years_to_retain int, level_of_security String(2) OPTIMIZEFETCH</p>
<p>ASPECT 속성 제거 :<br/>
ALTER ASPECT dm_document_aspect drop level_of_security</p>
<p>TYPE에 ASPECT add :<br/>
ALTER TYPE dm_document add DEFAULT ASPECTS dm_document_aspect</p>
<p>ASPECT 속성 테스트 :<br/>
SELECT r_object_id, dm_document_aspect.years_to_retain, dm_document_aspect.level_of_security<br/>
FROM dm_document WHERE dm_document_aspect.years_to_retain = 10</p>
<p>TYPE에 ASPECT remove :<br/>
ALTER TYPE dm_document REMOVE DEFAULT ASPECTS dm_document_aspect;</p>
<p>ASPECT 삭제 :<br/>
ALTER ASPECT dm_document_aspect DROP ALL</p>
<p>iapi에서 ASPECT 사용예 :<br/>
create,c,dm_document<br/>
set,c,l,a_content_type<br/>
text<br/>
set,c,l,object_name<br/>
test test3<br/>
setfile,c,l,d:\temp\a.txt<br/>
link,c,l,/Temp<br/>
set,c,l,dm_document_aspect.level_of_security<br/>
A<br/>
set,c,l,dm_document_aspect.years_to_retain<br/>
1<br/>
save,c,l</p>
<nav class="pagination group"></nav></div>
<div class="clear"></div>
</div>
</div>
</article>
```
