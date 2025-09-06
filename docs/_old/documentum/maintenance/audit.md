---
title: "audit"
date: "No Date"
---

audit
=====

by 
[박경원](https://appi77.github.io/my-tips/author/appi77/ "박경원이(가) 작성한 글")
·
2016년 6월 30일

▣ purge\_audit

[검증된 방식]

EXECUTE purge\_audit WITH DELETE\_MODE=’PREDICATE’  
, dql\_predicate=’dm\_audittrail WHERE time\_stamp < ”2016/06/01 00:00:00” AND event\_source=”System Unspecific”’  
, purge\_non\_archived=TRUE,commit\_size=5000

[매뉴얼 있지만 안되는 방식]

EXECUTE purge\_audit WITH DELETE\_MODE=’DATE\_RANGE’  
, DATE\_START=’01/01/2003 00:00:00 AM’, DATE\_END=’06/01/2016 00:00:00 AM’  
, purge\_non\_archived=TRUE,commit\_size=5000  
EXECUTE purge\_audit WITH DELETE\_MODE=’ALL\_VERSIONS’  
, object\_id=’5f1876a980000100′  
, purge\_non\_archived=TRUE,commit\_size=5000

```html
<article class="post-59 post type-post status-publish format-standard hentry category-maintenance"><div class="post-inner group">
<h1 class="post-title entry-title">audit</h1>
<p class="post-byline">
   by   <span class="vcard author">
<span class="fn"><a href="https://appi77.github.io/my-tips/author/appi77/" rel="author" title="박경원이(가) 작성한 글">박경원</a></span>
</span>
   ·
                                <time class="published" datetime="2016년 6월 30일">2016년 6월 30일</time></p>
<div class="clear"></div>
<div class="entry themeform">
<div class="entry-inner">
<p>▣ purge_audit</p>
<p>[검증된 방식]</p>
<p>EXECUTE purge_audit WITH DELETE_MODE=’PREDICATE’<br/>
, dql_predicate=’dm_audittrail WHERE time_stamp &lt; ”2016/06/01 00:00:00” AND event_source=”System Unspecific”’<br/>
, purge_non_archived=TRUE,commit_size=5000</p>
<p>[매뉴얼 있지만 안되는 방식]</p>
<p>EXECUTE purge_audit WITH DELETE_MODE=’DATE_RANGE’<br/>
, DATE_START=’01/01/2003 00:00:00 AM’, DATE_END=’06/01/2016 00:00:00 AM’<br/>
, purge_non_archived=TRUE,commit_size=5000<br/>
EXECUTE purge_audit WITH DELETE_MODE=’ALL_VERSIONS’<br/>
, object_id=’5f1876a980000100′<br/>
, purge_non_archived=TRUE,commit_size=5000</p>
<p> </p>
<nav class="pagination group"></nav></div>
<div class="clear"></div>
</div>
</div>
</article>
```
