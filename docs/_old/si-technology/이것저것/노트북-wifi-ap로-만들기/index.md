---
title: "노트북 WiFi  AP로 만들기"
date: "No Date"
---

노트북 WiFi AP로 만들기
================

by 
[박경원](https://appi77.github.io/my-tips/author/appi77/ "박경원이(가) 작성한 글")
·
2016년 7월 14일

netsh wlan set hostednetwork mode=allow “ssid=xxxx” “key=xxx\_passwd” keyUsage=persistent  
사용하는 어댑터 -> 속성-> 공유에서 [무선 네트워크 연결 2] 선택  
netsh wlan start hostednetwork  
사용을 중지할 때:  
netsh wlan stop hostednetwork  
Virtual WiFi Adapter를 제거할 때:  
netsh wlan set hostednetwork mode=disallow

```html
<article class="post-159 post type-post status-publish format-standard hentry category-21"><div class="post-inner group">
<h1 class="post-title entry-title">노트북 WiFi  AP로 만들기</h1>
<p class="post-byline">
   by   <span class="vcard author">
<span class="fn"><a href="https://appi77.github.io/my-tips/author/appi77/" rel="author" title="박경원이(가) 작성한 글">박경원</a></span>
</span>
   ·
                                <time class="published" datetime="2016년 7월 14일">2016년 7월 14일</time></p>
<div class="clear"></div>
<div class="entry themeform">
<div class="entry-inner">
<p>netsh wlan set hostednetwork mode=allow “ssid=xxxx” “key=xxx_passwd” keyUsage=persistent<br/>
사용하는 어댑터 -&gt; 속성-&gt; 공유에서 [무선 네트워크 연결 2] 선택<br/>
netsh wlan start hostednetwork<br/>
사용을 중지할 때:<br/>
netsh wlan stop hostednetwork<br/>
Virtual WiFi Adapter를 제거할 때:<br/>
netsh wlan set hostednetwork mode=disallow</p>
<nav class="pagination group"></nav></div>
<div class="clear"></div>
</div>
</div>
</article>
```
