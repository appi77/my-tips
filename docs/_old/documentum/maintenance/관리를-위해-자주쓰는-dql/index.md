---
title: "관리를 위해 자주쓰는 DQL"
date: "No Date"
---

관리를 위해 자주쓰는 DQL
===============

by 
[박경원](https://appi77.github.io/my-tips/author/appi77/ "박경원이(가) 작성한 글")
·
Published 2016년 6월 30일
· Updated 2016년 7월 1일

DEFAULT STORAGE변경 :  
alter type “dm\_document” set default storage ‘filestore\_01’

Find Filestore path :  
SELECT file\_system\_path FROM dm\_location WHERE object\_name IN  
(SELECT root FROM dm\_filestore WHERE name IN  
(SELECT a\_storage\_type FROM dm\_document WHERE r\_object\_id = ‘’)  
)

Index 추가 :  
EXECUTE make\_index WITH type\_name=’ud\_document’,  
attribute=’c\_creation\_date’,  
attribute=’c\_group\_name’,  
index\_name=’UD\_WF\_EVENT\_NAME\_IX’  
INDEX\_SPACE=’DM\_PILOT’ –Repository Configuration Properties / Index Store 확인  
–use\_id\_col=true 를 넣으면 r\_object\_id가 자동으로 들어가는데 멀티 컬럼 인덱스인 경우 맨 앞으로만 들어감

EXECUTE make\_index WITH type\_name=’dm\_sysobject’,  
attribute=’r\_creation\_date’,  
attribute=’group\_name’

Index 삭제 :  
EXECUTE drop\_index for ‘1f1eb06580000d08′;

Index 추가 예 :  
EXECUTE make\_index WITH type\_name=’dm\_sysobject’,  
attribute=’a\_status’,  
attribute=’r\_creation\_date’,  
attribute=’owner\_name’,  
attribute=’group\_name’,  
attribute=’title’,INDEX\_SPACE=’DM\_PILOT’

```html
<article class="post-36 post type-post status-publish format-standard hentry category-maintenance"><div class="post-inner group">
<h1 class="post-title entry-title">관리를 위해 자주쓰는 DQL</h1>
<p class="post-byline">
   by   <span class="vcard author">
<span class="fn"><a href="https://appi77.github.io/my-tips/author/appi77/" rel="author" title="박경원이(가) 작성한 글">박경원</a></span>
</span>
   ·
                                Published <time class="published" datetime="2016년 6월 30일">2016년 6월 30일</time>
              · Updated <time class="updated" datetime="2016년 7월 1일">2016년 7월 1일</time></p>
<div class="clear"></div>
<div class="entry themeform">
<div class="entry-inner">
<p>DEFAULT STORAGE변경 :<br/>
alter type “dm_document” set default storage ‘filestore_01’</p>
<p>Find Filestore path :<br/>
SELECT file_system_path FROM dm_location WHERE object_name IN<br/>
(SELECT root FROM dm_filestore WHERE name IN<br/>
(SELECT a_storage_type FROM dm_document WHERE r_object_id = ‘<r_object_id>’)<br/>
)</r_object_id></p>
<p>Index 추가 :<br/>
EXECUTE make_index WITH type_name=’ud_document’,<br/>
attribute=’c_creation_date’,<br/>
attribute=’c_group_name’,<br/>
index_name=’UD_WF_EVENT_NAME_IX’<br/>
INDEX_SPACE=’DM_PILOT’ –Repository Configuration Properties / Index Store 확인<br/>
–use_id_col=true 를 넣으면 r_object_id가 자동으로 들어가는데 멀티 컬럼 인덱스인 경우 맨 앞으로만 들어감</p>
<p>EXECUTE make_index WITH type_name=’dm_sysobject’,<br/>
attribute=’r_creation_date’,<br/>
attribute=’group_name’</p>
<p>Index 삭제 :<br/>
EXECUTE drop_index for ‘1f1eb06580000d08′;</p>
<p>Index 추가 예 :<br/>
EXECUTE make_index WITH type_name=’dm_sysobject’,<br/>
attribute=’a_status’,<br/>
attribute=’r_creation_date’,<br/>
attribute=’owner_name’,<br/>
attribute=’group_name’,<br/>
attribute=’title’,INDEX_SPACE=’DM_PILOT’</p>
<nav class="pagination group"></nav></div>
<div class="clear"></div>
</div>
</div>
</article>
```
