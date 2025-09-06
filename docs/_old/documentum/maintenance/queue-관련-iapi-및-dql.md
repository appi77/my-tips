---
title: "QUEUE 관련 IAPI 및 DQL"
date: "No Date"
---

QUEUE 관련 IAPI 및 DQL
===================

by 
[박경원](https://appi77.github.io/my-tips/author/appi77/ "박경원이(가) 작성한 글")
·
2016년 6월 30일

PDF변환 QUEUE 등록 API :  
queue,session,object\_id,user\_name,event,priority[,send\_mail],[due\_date],message  
예  
queue,c,091876a98002095a,dm\_autorender\_win31,rendition,0,,,rendition\_req\_ocr

PDF변환 QUEUE 삭제 API :  
dequeue,c,stamp

PDF변환 QUEUE 조회 DQL :  
select \* from dm\_queue where name = ‘dm\_autorender\_win31’ and message = ‘rendition\_req\_ocr’;  
※ ‘rendition\_req\_ocr’ 은 queue 처리 할 쪽과 약속한 메시지임

```html
<article class="post-28 post type-post status-publish format-standard hentry category-maintenance"><div class="post-inner group">
<h1 class="post-title entry-title">QUEUE 관련 IAPI 및 DQL</h1>
<p class="post-byline">
   by   <span class="vcard author">
<span class="fn"><a href="https://appi77.github.io/my-tips/author/appi77/" rel="author" title="박경원이(가) 작성한 글">박경원</a></span>
</span>
   ·
                                <time class="published" datetime="2016년 6월 30일">2016년 6월 30일</time></p>
<div class="clear"></div>
<div class="entry themeform">
<div class="entry-inner">
<p>PDF변환 QUEUE 등록 API :<br/>
queue,session,object_id,user_name,event,priority[,send_mail],[due_date],message<br/>
예<br/>
queue,c,091876a98002095a,dm_autorender_win31,rendition,0,,,rendition_req_ocr</p>
<p>PDF변환 QUEUE 삭제 API :<br/>
dequeue,c,stamp</p>
<p>PDF변환 QUEUE 조회 DQL :<br/>
select * from dm_queue where name = ‘dm_autorender_win31’ and message = ‘rendition_req_ocr’;<br/>
※ ‘rendition_req_ocr’ 은 queue 처리 할 쪽과 약속한 메시지임</p>
<nav class="pagination group"></nav></div>
<div class="clear"></div>
</div>
</div>
</article>
```
