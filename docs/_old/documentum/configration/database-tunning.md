---
title: "Database tunning"
date: "No Date"
---

Database tunning
================

by 
[박경원](https://appi77.github.io/my-tips/author/appi77/ "박경원이(가) 작성한 글")
·
2016년 6월 30일

▣ Oracle Server.

[문제] rocesses와 sessions 계산  
[해법] processes = 2 \* total number of concurrent\_session in server.ini  
sessions = processes \* 1.1 + 5

[문제] 폴더 탐색과 폴더 표시에 성능 저하가 보이기 시작함  
[해법] /WEB-INF/classes/dfc.properties 파일에 trace옵션을 설정한다.  
dfc.tracing.enable = true  
dfc.tracing.verbose = true  
dfc.tracing.max\_stack\_depth = 0  
dfc.tracing.include\_rpcs = true  
dfc.tracing.mode = compact  
dfc.tracing.include\_session\_id = true

[![trace](https://appi77.github.io/my-tips/wordpress/wp-content/uploads/2016/06/111.png)](https://appi77.github.io/my-tips/wordpress/wp-content/uploads/2016/06/111.png)

장기실행 DQL을 찾아 쿼리 타이밍과 응답을 검토한다.  
[해법] 이슈를 재현하기 위해 동일ID로 IAPI에 로그인한다.(실사용자 성능과 관련된 문제라면 설치소유자ID를 사용하지 말것)  
– SQL trace ON :  
API> trace,c,1,,SQL\_TRACE  
…  
OK  
– 문제쿼리를 실행 (예) :  
API> ?,c, select 1,upper(object\_name),r\_object\_id,object\_name,r\_object\_type …..  
– 다음 폴더에서 결과를 볼 수 있음 :  
$DOCUMENTUM/dba/log//  
– SQL trace on OFF:  
API> trace,c,0,,SQL\_TRACE  
…  
OK  
▣ SQL Server.

서버 -> 속성 -> 고급  
최대 병렬 처리 수준( Max Degree of Parallelism ) = 1 로 설정한다.  
Max Degree of Parallelism 은 하나의 SQL문에 대해 CPU 프로세서의 수를 지정해 주는 것이다.  
기본값은 0이고 이는 필요에 따라 가지고 있는 모든 CPU를 사용할 수도 있다는 뜻이다.  
하나의 SQL문이 너무 많은 리소스를 사용하면 다른 작업의 속도가 저하된다.

데이터베이스 -> 속성 -> 옵션  
매개 변수화 (Parameterization) = 강제(Forced)  
통계 자동 작성(Auto Create Statistics) = False  
통계 자동 업데이트(Auto Update Statistics)= True(\*)  
통계를 비동기적으로 자동 업데이트(Auto Update Statistics Asynchronously)= True(\*)  
(\*) 과도한 업데이트가 서버에서 발견되면 False로 설정하고 통계 수동 업데이트 한다.  
READ\_COMMITTED\_SNAPSHOT=True  
ALTER DATABASE DM\_\_docbase SET READ\_COMMITTED\_SNAPSHOT ON

```html
<article class="post-13 post type-post status-publish format-standard hentry category-configration"><div class="post-inner group">
<h1 class="post-title entry-title">Database tunning</h1>
<p class="post-byline">
   by   <span class="vcard author">
<span class="fn"><a href="https://appi77.github.io/my-tips/author/appi77/" rel="author" title="박경원이(가) 작성한 글">박경원</a></span>
</span>
   ·
                                <time class="published" datetime="2016년 6월 30일">2016년 6월 30일</time></p>
<div class="clear"></div>
<div class="entry themeform">
<div class="entry-inner">
<p>▣ Oracle Server.</p>
<p>[문제] rocesses와 sessions 계산<br/>
[해법] processes = 2 * total number of concurrent_session in server.ini<br/>
sessions = processes * 1.1 + 5</p>
<p>[문제] 폴더 탐색과 폴더 표시에 성능 저하가 보이기 시작함<br/>
[해법] <webapp>/WEB-INF/classes/dfc.properties 파일에 trace옵션을 설정한다.<br/>
dfc.tracing.enable = true<br/>
dfc.tracing.verbose = true<br/>
dfc.tracing.max_stack_depth = 0<br/>
dfc.tracing.include_rpcs = true<br/>
dfc.tracing.mode = compact<br/>
dfc.tracing.include_session_id = true</webapp></p>
<p><a href="https://appi77.github.io/my-tips/wordpress/wp-content/uploads/2016/06/111.png"><img alt="trace" class="alignnone wp-image-14" height="104" sizes="(max-width: 675px) 100vw, 675px" src="https://appi77.github.io/my-tips/wordpress/wp-content/uploads/2016/06/111.png" srcset="https://appi77.github.io/my-tips/wordpress/wp-content/uploads/2016/06/111.png 1036w,https://appi77.github.io/my-tips/wordpress/wp-content/uploads/2016/06/111-300x46.png 300w,https://appi77.github.io/my-tips/wordpress/wp-content/uploads/2016/06/111-768x118.png 768w,https://appi77.github.io/my-tips/wordpress/wp-content/uploads/2016/06/111-1024x157.png 1024w,https://appi77.github.io/my-tips/wordpress/wp-content/uploads/2016/06/111-624x96.png 624w" width="675"/></a></p>
<p>장기실행 DQL을 찾아 쿼리 타이밍과 응답을 검토한다.<br/>
[해법] 이슈를 재현하기 위해 동일ID로 IAPI에 로그인한다.(실사용자 성능과 관련된 문제라면 설치소유자ID를 사용하지 말것)<br/>
– SQL trace ON :<br/>
API&gt; trace,c,1,,SQL_TRACE<br/>
…<br/>
OK<br/>
– 문제쿼리를 실행 (예) :<br/>
API&gt; ?,c, select 1,upper(object_name),r_object_id,object_name,r_object_type …..<br/>
– 다음 폴더에서 결과를 볼 수 있음 :<br/>
$DOCUMENTUM/dba/log/<docbase_id>/<user_name><br/>
– SQL trace on OFF:<br/>
API&gt; trace,c,0,,SQL_TRACE<br/>
…<br/>
OK<br/>
▣ SQL Server.</user_name></docbase_id></p>
<p>서버 -&gt; 속성 -&gt; 고급<br/>
최대 병렬 처리 수준( Max Degree of Parallelism ) = 1 로 설정한다.<br/>
Max Degree of Parallelism 은 하나의 SQL문에 대해 CPU 프로세서의 수를 지정해 주는 것이다.<br/>
기본값은 0이고 이는 필요에 따라 가지고 있는 모든 CPU를 사용할 수도 있다는 뜻이다.<br/>
하나의 SQL문이 너무 많은 리소스를 사용하면 다른 작업의 속도가 저하된다.</p>
<p>데이터베이스 -&gt; 속성 -&gt; 옵션<br/>
매개 변수화 (Parameterization) = 강제(Forced)<br/>
통계 자동 작성(Auto Create Statistics) = False<br/>
통계 자동 업데이트(Auto Update Statistics)= True(*)<br/>
통계를 비동기적으로 자동 업데이트(Auto Update Statistics Asynchronously)= True(*)<br/>
(*) 과도한 업데이트가 서버에서 발견되면 False로 설정하고 통계 수동 업데이트 한다.<br/>
READ_COMMITTED_SNAPSHOT=True<br/>
ALTER DATABASE DM_<repository_name>_docbase SET READ_COMMITTED_SNAPSHOT ON</repository_name></p>
<nav class="pagination group"></nav></div>
<div class="clear"></div>
</div>
</div>
</article>
```
