---
title: "Documentum content server hostname 변경"
date: "No Date"
---

Documentum content server hostname 변경
=====================================

by 
[박경원](https://appi77.github.io/my-tips/author/appi77/ "박경원이(가) 작성한 글")
·
2016년 7월 3일

Documentum content server hostname 변경  
Symptoms

For copying a Repository and changing the hostname

Resolution

To make a copy of an environment – even if it is a vm image, you need to consider the instructions in copying a repository mentioned in Content server installation guide Copy Repository section.

Install with the same user, db, etc.

Need to then change the hostname in a few of the db tables.  
Verify that the database tables have the correct value for the test system host name by checking the following values:  
\*  r\_host\_name in dm\_server\_config\_s  
\*  host\_name in dm\_mount\_point\_s  
\*  target\_server in dm\_job\_s  
\*  projection\_targets in dm\_server\_config\_r  
Then the hostname in the [server.ini](http://server.ini), [dmcl.ini](http://dmcl.ini) files

```html
<article class="post-145 post type-post status-publish format-standard hentry category-trouble"><div class="post-inner group">
<h1 class="post-title entry-title">Documentum content server hostname 변경</h1>
<p class="post-byline">
   by   <span class="vcard author">
<span class="fn"><a href="https://appi77.github.io/my-tips/author/appi77/" rel="author" title="박경원이(가) 작성한 글">박경원</a></span>
</span>
   ·
                                <time class="published" datetime="2016년 7월 3일">2016년 7월 3일</time></p>
<div class="clear"></div>
<div class="entry themeform">
<div class="entry-inner">
<p>Documentum content server hostname 변경<br/>
Symptoms</p>
<p>For copying a Repository and changing the hostname</p>
<p>Resolution</p>
<p>To make a copy of an environment – even if it is a vm image, you need to consider the instructions in copying a repository mentioned in Content server installation guide Copy Repository section.</p>
<p>Install with the same user, db, etc.</p>
<p>Need to then change the hostname in a few of the db tables.<br/>
Verify that the database tables have the correct value for the test system host name by checking the following values:<br/>
*  r_host_name in dm_server_config_s<br/>
*  host_name in dm_mount_point_s<br/>
*  target_server in dm_job_s<br/>
*  projection_targets in dm_server_config_r<br/>
Then the hostname in the <a href="http://server.ini">server.ini</a>, <a href="http://dmcl.ini">dmcl.ini</a> files</p>
<nav class="pagination group"></nav></div>
<div class="clear"></div>
</div>
</div>
</article>
```
