---
title: "문제 있는 쿼리 찾기"
date: "No Date"
---

문제 있는 쿼리 찾기
===========

by 
[박경원](https://appi77.github.io/my-tips/author/appi77/ "박경원이(가) 작성한 글")
·
Published 2019년 4월 1일
· Updated 2019년 4월 1일

SELECT  
q.cpu\_x,  
q.execs,  
t.sql\_text,  
q.\*  
FROM ( SELECT  
q.dbid,  
q.instance\_number,  
q.sql\_id,  
MAX(q.optimizer\_mode) optmode,  
MAX(q.module) module,  
MAX(q.action) action,  
MAX(q.force\_matching\_signature) force\_matching\_signature,  
MAX(q.parsing\_schema\_name) parse\_schema,  
SUM(q.executions\_delta) execs,  
SUM(q.disk\_reads\_delta) dreads,  
SUM(q.buffer\_gets\_delta) bgets,  
SUM(q.rows\_processed\_delta) rows\_processed,  
SUM(q.cpu\_time\_delta) cpu,  
SUM(q.elapsed\_time\_delta) elapsed,  
SUM(q.iowait\_delta) iowait,  
SUM(q.clwait\_delta) clwait,  
SUM(q.apwait\_delta) apwait,  
SUM(q.ccwait\_delta) ccwait,  
SUM(q.direct\_writes\_delta) direct\_writes,  
SUM(q.plsexec\_time\_delta) plsexec\_time,  
SUM(q.javexec\_time\_delta) javaexec\_time,  
SUM(q.disk\_reads\_delta) / DECODE(SUM(q.executions\_delta),0,1,NULL,1,SUM(q.executions\_delta) ) dreads\_x,  
SUM(q.buffer\_gets\_delta) / DECODE(SUM(q.executions\_delta),0,1,NULL,1,SUM(q.executions\_delta) ) bgets\_x,  
SUM(q.rows\_processed\_delta) / DECODE(SUM(q.executions\_delta),0,1,NULL,1,SUM(q.executions\_delta) ) rows\_x,  
( SUM(q.cpu\_time\_delta) / DECODE(SUM(q.executions\_delta),0,1,NULL,1,SUM(q.executions\_delta) ) ) / 1000000 cpu\_x,  
( SUM(q.elapsed\_time\_delta) / DECODE(SUM(q.executions\_delta),0,1,NULL,1,SUM(q.executions\_delta) ) ) / 1000000 elapsed\_x,  
( SUM(q.iowait\_delta) / DECODE(SUM(q.executions\_delta),0,1,NULL,1,SUM(q.executions\_delta) ) ) / 1000000 iowait\_x,  
( SUM(q.clwait\_delta) / DECODE(SUM(q.executions\_delta),0,1,NULL,1,SUM(q.executions\_delta) ) ) / 1000000 clwait\_x,  
( SUM(q.apwait\_delta) / DECODE(SUM(q.executions\_delta),0,1,NULL,1,SUM(q.executions\_delta) ) ) / 1000000 apwait\_x,  
( SUM(q.ccwait\_delta) / DECODE(SUM(q.executions\_delta),0,1,NULL,1,SUM(q.executions\_delta) ) ) / 1000000 ccwait\_x,  
SUM(q.direct\_writes\_delta) / DECODE(SUM(q.executions\_delta),0,1,NULL,1,SUM(q.executions\_delta) ) direct\_writes\_x,  
( SUM(q.plsexec\_time\_delta) / DECODE(SUM(q.executions\_delta),0,1,NULL,1,SUM(q.executions\_delta) ) ) / 1000000 plsexec\_time\_x,  
( SUM(q.javexec\_time\_delta) / DECODE(SUM(q.executions\_delta),0,1,NULL,1,SUM(q.executions\_delta) ) ) / 1000000 javaexec\_time\_x  
FROM  
dba\_hist\_snapshot s,  
dba\_hist\_sqlstat q  
WHERE  
s.dbid = q.dbid  
AND s.instance\_number = q.instance\_number  
AND s.snap\_id = q.snap\_id  
AND TO\_CHAR( s.begin\_interval\_time,’yyyy/mm/dd HH24:MI:SS’) BETWEEN ‘2019/03/26 20:00:00’ AND ‘2019/04/01 23:59:59’  
GROUP BY Q.DBID, Q.INSTANCE\_NUMBER, Q.SQL\_ID

) Q, DBA\_HIST\_SQLTEXT T  
WHERE Q.DBID = T.DBID  
AND Q.SQL\_ID = T.SQL\_ID  
AND Q.CPU\_X > 2  
AND Q.EXECS > 1  
–and T.SQL\_TEXT like ‘select all df1.r\_object\_id%’  
and module in ( ‘documentum.exe’, ‘jdbc thin client’ ) order by q.execs desc

```html
<article class="post-611 post type-post status-publish format-standard hentry category-rdbms tag-oralce tag-sql tag-tunning"><div class="post-inner group">
<h1 class="post-title entry-title">문제 있는 쿼리 찾기</h1>
<p class="post-byline">
   by   <span class="vcard author">
<span class="fn"><a href="https://appi77.github.io/my-tips/author/appi77/" rel="author" title="박경원이(가) 작성한 글">박경원</a></span>
</span>
   ·
                                Published <time class="published" datetime="2019년 4월 1일">2019년 4월 1일</time>
              · Updated <time class="updated" datetime="2019년 4월 1일">2019년 4월 1일</time></p>
<div class="clear"></div>
<div class="entry themeform">
<div class="entry-inner">
<p>SELECT<br/>
q.cpu_x,<br/>
q.execs,<br/>
t.sql_text,<br/>
q.*<br/>
FROM ( SELECT<br/>
q.dbid,<br/>
q.instance_number,<br/>
q.sql_id,<br/>
MAX(q.optimizer_mode) optmode,<br/>
MAX(q.module) module,<br/>
MAX(q.action) action,<br/>
MAX(q.force_matching_signature) force_matching_signature,<br/>
MAX(q.parsing_schema_name) parse_schema,<br/>
SUM(q.executions_delta) execs,<br/>
SUM(q.disk_reads_delta) dreads,<br/>
SUM(q.buffer_gets_delta) bgets,<br/>
SUM(q.rows_processed_delta) rows_processed,<br/>
SUM(q.cpu_time_delta) cpu,<br/>
SUM(q.elapsed_time_delta) elapsed,<br/>
SUM(q.iowait_delta) iowait,<br/>
SUM(q.clwait_delta) clwait,<br/>
SUM(q.apwait_delta) apwait,<br/>
SUM(q.ccwait_delta) ccwait,<br/>
SUM(q.direct_writes_delta) direct_writes,<br/>
SUM(q.plsexec_time_delta) plsexec_time,<br/>
SUM(q.javexec_time_delta) javaexec_time,<br/>
SUM(q.disk_reads_delta) / DECODE(SUM(q.executions_delta),0,1,NULL,1,SUM(q.executions_delta) ) dreads_x,<br/>
SUM(q.buffer_gets_delta) / DECODE(SUM(q.executions_delta),0,1,NULL,1,SUM(q.executions_delta) ) bgets_x,<br/>
SUM(q.rows_processed_delta) / DECODE(SUM(q.executions_delta),0,1,NULL,1,SUM(q.executions_delta) ) rows_x,<br/>
( SUM(q.cpu_time_delta) / DECODE(SUM(q.executions_delta),0,1,NULL,1,SUM(q.executions_delta) ) ) / 1000000 cpu_x,<br/>
( SUM(q.elapsed_time_delta) / DECODE(SUM(q.executions_delta),0,1,NULL,1,SUM(q.executions_delta) ) ) / 1000000 elapsed_x,<br/>
( SUM(q.iowait_delta) / DECODE(SUM(q.executions_delta),0,1,NULL,1,SUM(q.executions_delta) ) ) / 1000000 iowait_x,<br/>
( SUM(q.clwait_delta) / DECODE(SUM(q.executions_delta),0,1,NULL,1,SUM(q.executions_delta) ) ) / 1000000 clwait_x,<br/>
( SUM(q.apwait_delta) / DECODE(SUM(q.executions_delta),0,1,NULL,1,SUM(q.executions_delta) ) ) / 1000000 apwait_x,<br/>
( SUM(q.ccwait_delta) / DECODE(SUM(q.executions_delta),0,1,NULL,1,SUM(q.executions_delta) ) ) / 1000000 ccwait_x,<br/>
SUM(q.direct_writes_delta) / DECODE(SUM(q.executions_delta),0,1,NULL,1,SUM(q.executions_delta) ) direct_writes_x,<br/>
( SUM(q.plsexec_time_delta) / DECODE(SUM(q.executions_delta),0,1,NULL,1,SUM(q.executions_delta) ) ) / 1000000 plsexec_time_x,<br/>
( SUM(q.javexec_time_delta) / DECODE(SUM(q.executions_delta),0,1,NULL,1,SUM(q.executions_delta) ) ) / 1000000 javaexec_time_x<br/>
FROM<br/>
dba_hist_snapshot s,<br/>
dba_hist_sqlstat q<br/>
WHERE<br/>
s.dbid = q.dbid<br/>
AND s.instance_number = q.instance_number<br/>
AND s.snap_id = q.snap_id<br/>
AND TO_CHAR( s.begin_interval_time,’yyyy/mm/dd HH24:MI:SS’) BETWEEN ‘2019/03/26 20:00:00’ AND ‘2019/04/01 23:59:59’<br/>
GROUP BY Q.DBID, Q.INSTANCE_NUMBER, Q.SQL_ID</p>
<p>) Q, DBA_HIST_SQLTEXT T<br/>
WHERE Q.DBID = T.DBID<br/>
AND Q.SQL_ID = T.SQL_ID<br/>
AND Q.CPU_X &gt; 2<br/>
AND Q.EXECS &gt; 1<br/>
–and T.SQL_TEXT like ‘select all df1.r_object_id%’<br/>
and module in ( ‘documentum.exe’, ‘jdbc thin client’ ) order by q.execs desc</p>
<nav class="pagination group"></nav></div>
<div class="clear"></div>
</div>
</div>
</article>
```
