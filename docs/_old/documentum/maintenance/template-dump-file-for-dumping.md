---
title: "template dump file for dumping"
date: "No Date"
---

template dump file for dumping
==============================

by 
[박경원](https://appi77.github.io/my-tips/author/appi77/ "박경원이(가) 작성한 글")
·
2016년 6월 30일

iapi 툴에서 Object를 덤프하는 방법  
#  
# This is a generic template dump file for dumping a x.x docbase.  
#  
# The following types are dumped:  
#  
# dm\_sysobject  
# dm\_assembly  
# dm\_format  
# dm\_user  
# dm\_group  
# dm\_relation  
# dm\_relation\_type  
# dmi\_queue\_item  
# dmi\_registry  
# dmr\_containment  
# dmr\_content  
#  
# If you have added any new types that do not inherit from documentum  
# base types, you must add them into the script.  
#  
# NOTE: If you have altered any system types: (ie sysobject, user,…)  
# Make sure that you perform the alter types on any target docbase  
# before loading the dump file created by this script.  
#  
create,c,dm\_dump\_record  
set,c,l,file\_name  
d:\dump\dumpfile.txt  
#  
# NOTE: specify a path to a dump file.  
# This path must be recognizable on the server machine  
#  
set,c,l,include\_content  
T  
append,c,l,type  
dm\_sysobject  
append,c,l,predicate  
1 = 1  
append,c,l,type  
dm\_assembly  
append,c,l,predicate  
1 = 1  
append,c,l,type  
dm\_format  
append,c,l,predicate  
1 = 1  
append,c,l,type  
dm\_user  
append,c,l,predicate  
1 = 1  
append,c,l,type  
dm\_group  
append,c,l,predicate  
1 = 1  
append,c,l,type  
dm\_relation  
append,c,l,predicate  
1 = 1  
append,c,l,type  
dm\_relation\_type  
append,c,l,predicate  
1 = 1  
append,c,l,type  
dmi\_queue\_item  
append,c,l,predicate  
1 = 1  
append,c,l,type  
dmi\_registry  
append,c,l,predicate  
1 = 1  
append,c,l,type  
dmr\_containment  
append,c,l,predicate  
1 = 1  
append,c,l,type  
dmr\_content  
append,c,l,predicate  
1 = 1  
append,c,l,type  
dm\_acl  
append,c,l,predicate  
1 = 1  
#  
# NOTE: also dump any user defined non-sysobject types.  
#  
save,c,l  
getmessage,c

```html
<article class="post-30 post type-post status-publish format-standard hentry category-maintenance"><div class="post-inner group">
<h1 class="post-title entry-title">template dump file for dumping</h1>
<p class="post-byline">
   by   <span class="vcard author">
<span class="fn"><a href="https://appi77.github.io/my-tips/author/appi77/" rel="author" title="박경원이(가) 작성한 글">박경원</a></span>
</span>
   ·
                                <time class="published" datetime="2016년 6월 30일">2016년 6월 30일</time></p>
<div class="clear"></div>
<div class="entry themeform">
<div class="entry-inner">
<p>iapi 툴에서 Object를 덤프하는 방법<br/>
#<br/>
# This is a generic template dump file for dumping a x.x docbase.<br/>
#<br/>
# The following types are dumped:<br/>
#<br/>
# dm_sysobject<br/>
# dm_assembly<br/>
# dm_format<br/>
# dm_user<br/>
# dm_group<br/>
# dm_relation<br/>
# dm_relation_type<br/>
# dmi_queue_item<br/>
# dmi_registry<br/>
# dmr_containment<br/>
# dmr_content<br/>
#<br/>
# If you have added any new types that do not inherit from documentum<br/>
# base types, you must add them into the script.<br/>
#<br/>
# NOTE: If you have altered any system types: (ie sysobject, user,…)<br/>
# Make sure that you perform the alter types on any target docbase<br/>
# before loading the dump file created by this script.<br/>
#<br/>
create,c,dm_dump_record<br/>
set,c,l,file_name<br/>
d:\dump\dumpfile.txt<br/>
#<br/>
# NOTE: specify a path to a dump file.<br/>
# This path must be recognizable on the server machine<br/>
#<br/>
set,c,l,include_content<br/>
T<br/>
append,c,l,type<br/>
dm_sysobject<br/>
append,c,l,predicate<br/>
1 = 1<br/>
append,c,l,type<br/>
dm_assembly<br/>
append,c,l,predicate<br/>
1 = 1<br/>
append,c,l,type<br/>
dm_format<br/>
append,c,l,predicate<br/>
1 = 1<br/>
append,c,l,type<br/>
dm_user<br/>
append,c,l,predicate<br/>
1 = 1<br/>
append,c,l,type<br/>
dm_group<br/>
append,c,l,predicate<br/>
1 = 1<br/>
append,c,l,type<br/>
dm_relation<br/>
append,c,l,predicate<br/>
1 = 1<br/>
append,c,l,type<br/>
dm_relation_type<br/>
append,c,l,predicate<br/>
1 = 1<br/>
append,c,l,type<br/>
dmi_queue_item<br/>
append,c,l,predicate<br/>
1 = 1<br/>
append,c,l,type<br/>
dmi_registry<br/>
append,c,l,predicate<br/>
1 = 1<br/>
append,c,l,type<br/>
dmr_containment<br/>
append,c,l,predicate<br/>
1 = 1<br/>
append,c,l,type<br/>
dmr_content<br/>
append,c,l,predicate<br/>
1 = 1<br/>
append,c,l,type<br/>
dm_acl<br/>
append,c,l,predicate<br/>
1 = 1<br/>
#<br/>
# NOTE: also dump any user defined non-sysobject types.<br/>
#<br/>
save,c,l<br/>
getmessage,c</p>
<nav class="pagination group"></nav></div>
<div class="clear"></div>
</div>
</div>
</article>
```
