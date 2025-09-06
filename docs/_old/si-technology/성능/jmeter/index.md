---
title: "Jmeter"
date: "No Date"
---

Jmeter
======

by 
[박경원](https://appi77.github.io/my-tips/author/appi77/ "박경원이(가) 작성한 글")
·
Published 2019년 11월 28일
· Updated 2019년 11월 28일

https://jmeter-plugins.org/install/Install/ 에서

[plugins-manager.jar](https://jmeter-plugins.org/get/) 을 다운로드 받아 lib/ext 폴더에 넣는다.

option->plugin manager 에서

Custom Thread Groups , Basic Graphs 을 추가

**jp@gc – Stepping Thread Group (deprecated) 생성**

Max 200 Thread 생성  30초후에 10개씩 Thread 생성 최대 Thread로 600초간 유지이후에 1초 간격으로 5개씩 Thread Stop

This group will start 는 총 몇개의 Thread를 발생할것인가.

Next, add는 몇개씩 더해질것인가

threads every 몇초후에 더해질것인가

using ramp-up는 Next add되는 데 걸리는 시간

Then hold load for는 몇초동안 최대 Thread를 유지할것인가

Final stop 몇개씩 Thread를 줄일것인가

threads every 는 몇초간격으로 줄일것인가.

**결과보기**

* jp@gc – Response Times Over Time 생성 : 테스트 시간에 따른 응답 시간
* jp@gc – Transactions per Second 생성 : 초당 처리량 확인
* jp@gc – Response Times vs Threads : Thread 변화에 따른 응답 속도
* jp@gc – Composite Graph : 종합 적인 그래프를 함께 보여준다.

```html
<article class="post-1582 post type-post status-publish format-standard hentry category-23"><div class="post-inner group">
<h1 class="post-title entry-title">Jmeter</h1>
<p class="post-byline">
   by   <span class="vcard author">
<span class="fn"><a href="https://appi77.github.io/my-tips/author/appi77/" rel="author" title="박경원이(가) 작성한 글">박경원</a></span>
</span>
   ·
                                Published <time class="published" datetime="2019년 11월 28일">2019년 11월 28일</time>
              · Updated <time class="updated" datetime="2019년 11월 28일">2019년 11월 28일</time></p>
<div class="clear"></div>
<div class="entry themeform">
<div class="entry-inner">
<p>https://jmeter-plugins.org/install/Install/ 에서</p>
<p><a href="https://jmeter-plugins.org/get/">plugins-manager.jar</a> 을 다운로드 받아 <tt>lib/ext 폴더에 넣는다.</tt></p>
<p>option-&gt;plugin manager 에서</p>
<p>Custom Thread Groups , Basic Graphs 을 추가</p>
<p> </p>
<p><strong>  jp@gc – Stepping Thread Group (deprecated) 생성</strong></p>
<p style="padding-left: 40px;">Max 200 Thread 생성  30초후에 10개씩 Thread 생성 최대 Thread로 600초간 유지이후에 1초 간격으로 5개씩 Thread Stop</p>
<p style="padding-left: 80px;">This group will start 는 총 몇개의 Thread를 발생할것인가.</p>
<p style="padding-left: 80px;">Next, add는 몇개씩 더해질것인가</p>
<p style="padding-left: 80px;">threads every 몇초후에 더해질것인가</p>
<p style="padding-left: 80px;">using ramp-up는 Next add되는 데 걸리는 시간</p>
<p style="padding-left: 80px;">Then hold load for는 몇초동안 최대 Thread를 유지할것인가</p>
<p style="padding-left: 80px;">Final stop 몇개씩 Thread를 줄일것인가</p>
<p style="padding-left: 80px;">threads every 는 몇초간격으로 줄일것인가.</p>
<p><strong>결과보기</strong></p>
<ul><li>jp@gc – Response Times Over Time 생성 : 테스트 시간에 따른 응답 시간</li>
<li> jp@gc – Transactions per Second 생성 : 초당 처리량 확인</li>
<li>jp@gc – Response Times vs Threads : Thread 변화에 따른 응답 속도</li>
<li style="text-align: left;">jp@gc – Composite Graph : 종합 적인 그래프를 함께 보여준다.</li>
</ul><nav class="pagination group"></nav></div>
<div class="clear"></div>
</div>
</div>
</article>
```
