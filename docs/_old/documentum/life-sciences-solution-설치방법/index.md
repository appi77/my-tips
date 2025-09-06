---
title: "Life Sciences solution 설치방법"
date: "No Date"
---

Life Sciences solution 설치방법
===========================

by 
[박경원](https://appi77.github.io/my-tips/author/appi77/ "박경원이(가) 작성한 글")
·
2016년 7월 3일

1. Content Server 6.7 SP1 설치  
   6.7 SP1을 사용하지 않는다면 Life Sciences solution을 매뉴얼로 설치해야함  
   6.7 SP1, 6.7 SP2, 7.0, 7.1에서 설치스크립트 테스트됨  
   Java Method Server가 기동되어 있어야 함  
   Composer 필요  
   repository 기동되어 있어야 함  
   환경에 ANT\_HOME이 없어야 함
2. 업그레이드라면 Java Method Server lib 폴더의 파일들을 백업 후 삭제해야함  
   LSTMF – CFS-Methods.jar, TMF-Methods.jar  
   LSQM – CDF-Methods.jar
3. dmadmin이 super user가 아니면 nodmadmin.installparam.xml에 super user명을 수정
4. install.properties 파일 수정 – docbase,username,and password / 6.7.1, 6.7.2, 7.0, 7.1 / http://~
5. 컴맨드모드에서 %Temp% 위치 수정후 각각의 install.bat 실행
6. web application 설치  
   stop was  
   \01 LSTMF\CDFD2Plugins\CDFD2Plugins.jar -> WAS lib에 복사  
   \01 LSTMF\WAS\d2ls.war -> WAS webapps에 배포  
   dfc.properties 수정  
   start was

```html
<article class="post-113 post type-post status-publish format-standard hentry category-documentum"><div class="post-inner group">
<h1 class="post-title entry-title">Life Sciences solution 설치방법</h1>
<p class="post-byline">
   by   <span class="vcard author">
<span class="fn"><a href="https://appi77.github.io/my-tips/author/appi77/" rel="author" title="박경원이(가) 작성한 글">박경원</a></span>
</span>
   ·
                                <time class="published" datetime="2016년 7월 3일">2016년 7월 3일</time></p>
<div class="clear"></div>
<div class="entry themeform">
<div class="entry-inner">
<ol><li>Content Server 6.7 SP1 설치<br/>
6.7 SP1을 사용하지 않는다면 Life Sciences solution을 매뉴얼로 설치해야함<br/>
6.7 SP1, 6.7 SP2, 7.0, 7.1에서 설치스크립트 테스트됨<br/>
Java Method Server가 기동되어 있어야 함<br/>
Composer 필요<br/>
repository 기동되어 있어야 함<br/>
환경에 ANT_HOME이 없어야 함</li>
<li>업그레이드라면 Java Method Server lib 폴더의 파일들을 백업 후 삭제해야함<br/>
LSTMF – CFS-Methods.jar, TMF-Methods.jar<br/>
LSQM – CDF-Methods.jar</li>
<li>dmadmin이 super user가 아니면 nodmadmin.installparam.xml에 super user명을 수정</li>
<li>install.properties 파일 수정 – docbase,username,and password / 6.7.1, 6.7.2, 7.0, 7.1 / http://~</li>
<li>컴맨드모드에서 %Temp% 위치 수정후 각각의 install.bat 실행</li>
<li>web application 설치<br/>
stop was<br/>
\01 LSTMF\CDFD2Plugins\CDFD2Plugins.jar -&gt; WAS lib에 복사<br/>
\01 LSTMF\WAS\d2ls.war -&gt; WAS webapps에 배포<br/>
dfc.properties 수정<br/>
start was</li>
</ol><nav class="pagination group"></nav></div>
<div class="clear"></div>
</div>
</div>
</article>
```
