---
title: "No Title"
date: "2019-04-01"
---

[RDBMS](https://appi77.github.io/my-tips/category/si-technology/rdbms/)

2019년 4월 1일

 by 
[박경원](https://appi77.github.io/my-tips/author/appi77/ "박경원이(가) 작성한 글")
 · Published 2019년 4월 1일

[문제 있는 쿼리 찾기](https://appi77.github.io/my-tips/si-technology/rdbms/%eb%ac%b8%ec%a0%9c-%ec%9e%88%eb%8a%94-%ec%bf%bc%eb%a6%ac-%ec%b0%be%ea%b8%b0/ "Permalink to 문제 있는 쿼리 찾기")
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------

SELECT q.cpu\_x, q.execs, t.sql\_text, q.\* FROM ( SELECT q.dbid, q.instance\_number, q.sql\_id, MAX(q.optimizer\_mode) optmode, MAX(q.module) module, MAX(q.action) action, MAX(q.force\_matching\_signature) force\_matching\_signature, MAX(q.parsing\_schema\_name) parse\_schema, SUM(q.executions\_delta) execs, SUM(q.disk\_reads\_delta) dreads, SUM(q.buffer\_gets\_delta) bgets, SUM(q.rows\_processed\_delta) rows\_processed, SUM(q.cpu\_time\_delta) cpu, SUM(q.elapsed\_time\_delta) elapsed, SUM(q.iowait\_delta)...

```html
<article class="group grid-item post-611 post type-post status-publish format-standard hentry category-rdbms tag-oralce tag-sql tag-tunning" id="post-611"><div class="post-inner post-hover">
<div class="post-thumbnail">
<a href="https://appi77.github.io/my-tips/si-technology/rdbms/%eb%ac%b8%ec%a0%9c-%ec%9e%88%eb%8a%94-%ec%bf%bc%eb%a6%ac-%ec%b0%be%ea%b8%b0/">
</a>
</div>
<div class="post-meta group">
<p class="post-category"><a href="https://appi77.github.io/my-tips/category/si-technology/rdbms/" rel="category tag">RDBMS</a></p>
<p class="post-date">
<time class="published updated" datetime="2019-04-01 14:49:35">2019년 4월 1일</time></p>
<p class="post-byline" style="display:none"> by    <span class="vcard author">
<span class="fn"><a href="https://appi77.github.io/my-tips/author/appi77/" rel="author" title="박경원이(가) 작성한 글">박경원</a></span>
</span> · Published <span class="published">2019년 4월 1일</span>
</p>
</div>
<h2 class="post-title entry-title">
<a href="https://appi77.github.io/my-tips/si-technology/rdbms/%eb%ac%b8%ec%a0%9c-%ec%9e%88%eb%8a%94-%ec%bf%bc%eb%a6%ac-%ec%b0%be%ea%b8%b0/" rel="bookmark" title="Permalink to 문제 있는 쿼리 찾기">문제 있는 쿼리 찾기</a>
</h2>
<div class="entry excerpt entry-summary">
<p>SELECT q.cpu_x, q.execs, t.sql_text, q.* FROM ( SELECT q.dbid, q.instance_number, q.sql_id, MAX(q.optimizer_mode) optmode, MAX(q.module) module, MAX(q.action) action, MAX(q.force_matching_signature) force_matching_signature, MAX(q.parsing_schema_name) parse_schema, SUM(q.executions_delta) execs, SUM(q.disk_reads_delta) dreads, SUM(q.buffer_gets_delta) bgets, SUM(q.rows_processed_delta) rows_processed, SUM(q.cpu_time_delta) cpu, SUM(q.elapsed_time_delta) elapsed, SUM(q.iowait_delta)...</p>
</div>
</div>
</article>
```
