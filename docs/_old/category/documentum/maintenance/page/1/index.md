---
title: "No Title"
date: "2016-06-30"
---

[Maintenance](https://appi77.github.io/my-tips/category/documentum/maintenance/)

2016년 6월 30일

 by 
[박경원](https://appi77.github.io/my-tips/author/appi77/ "박경원이(가) 작성한 글")
 · Published 2016년 6월 30일

[audit](https://appi77.github.io/my-tips/documentum/maintenance/audit/ "Permalink to audit")
--------------------------------------------------------------------------------------------

▣ purge\_audit [검증된 방식] EXECUTE purge\_audit WITH DELETE\_MODE=’PREDICATE’ , dql\_predicate=’dm\_audittrail WHERE time\_stamp < ”2016/06/01 00:00:00” AND event\_source=”System Unspecific”’ , purge\_non\_archived=TRUE,commit\_size=5000 [매뉴얼 있지만 안되는 방식] EXECUTE purge\_audit WITH DELETE\_MODE=’DATE\_RANGE’ , DATE\_START=’01/01/2003 00:00:00 AM’, DATE\_END=’06/01/2016 00:00:00 AM’...

```html
<article class="group grid-item post-59 post type-post status-publish format-standard hentry category-maintenance" id="post-59"><div class="post-inner post-hover">
<div class="post-thumbnail">
<a href="https://appi77.github.io/my-tips/documentum/maintenance/audit/">
</a>
</div>
<div class="post-meta group">
<p class="post-category"><a href="https://appi77.github.io/my-tips/category/documentum/maintenance/" rel="category tag">Maintenance</a></p>
<p class="post-date">
<time class="published updated" datetime="2016-06-30 20:22:54">2016년 6월 30일</time></p>
<p class="post-byline" style="display:none"> by    <span class="vcard author">
<span class="fn"><a href="https://appi77.github.io/my-tips/author/appi77/" rel="author" title="박경원이(가) 작성한 글">박경원</a></span>
</span> · Published <span class="published">2016년 6월 30일</span>
</p>
</div>
<h2 class="post-title entry-title">
<a href="https://appi77.github.io/my-tips/documentum/maintenance/audit/" rel="bookmark" title="Permalink to audit">audit</a>
</h2>
<div class="entry excerpt entry-summary">
<p>▣ purge_audit [검증된 방식] EXECUTE purge_audit WITH DELETE_MODE=’PREDICATE’ , dql_predicate=’dm_audittrail WHERE time_stamp &lt; ”2016/06/01 00:00:00” AND event_source=”System Unspecific”’ , purge_non_archived=TRUE,commit_size=5000 [매뉴얼 있지만 안되는 방식] EXECUTE purge_audit WITH DELETE_MODE=’DATE_RANGE’ , DATE_START=’01/01/2003 00:00:00 AM’, DATE_END=’06/01/2016 00:00:00 AM’...</p>
</div>
</div>
</article>
```
