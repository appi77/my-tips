---
title: "dump & load"
date: "No Date"
---

dump & load
===========

by 
[박경원](https://appi77.github.io/my-tips/author/appi77/ "박경원이(가) 작성한 글")
·
2016년 6월 30일

iapi dump 예 :  
#  
create,c,dm\_dump\_record  
set,c,l,file\_name  
c:\dump\dumpfile.txt  
set,c,l,include\_content  
T  
append,c,l,type  
dm\_sysobject  
append,c,l,predicate  
folder(‘/WebPublisher Configuration/Common’)  
append,c,l,type  
dm\_user  
append,c,l,predicate  
1 = 1  
save,c,l  
getmessage,c  
iapi load 예 :  
trace,c,10  
create,c,dm\_load\_record  
set,c,l,file\_name  
c:\temp\dumpfile.txt  
set,c,l,relocate  
T  
dump,c,l  
save,c,l  
dump,c,l  
getmessage,c,1 (note-this is a one)  
destroy,c,l  
exit

```html
<article class="post-32 post type-post status-publish format-standard hentry category-maintenance"><div class="post-inner group">
<h1 class="post-title entry-title">dump &amp; load</h1>
<p class="post-byline">
   by   <span class="vcard author">
<span class="fn"><a href="https://appi77.github.io/my-tips/author/appi77/" rel="author" title="박경원이(가) 작성한 글">박경원</a></span>
</span>
   ·
                                <time class="published" datetime="2016년 6월 30일">2016년 6월 30일</time></p>
<div class="clear"></div>
<div class="entry themeform">
<div class="entry-inner">
<p>iapi dump 예 :<br/>
#<br/>
create,c,dm_dump_record<br/>
set,c,l,file_name<br/>
c:\dump\dumpfile.txt<br/>
set,c,l,include_content<br/>
T<br/>
append,c,l,type<br/>
dm_sysobject<br/>
append,c,l,predicate<br/>
folder(‘/WebPublisher Configuration/Common’)<br/>
append,c,l,type<br/>
dm_user<br/>
append,c,l,predicate<br/>
1 = 1<br/>
save,c,l<br/>
getmessage,c<br/>
iapi load 예 :<br/>
trace,c,10<br/>
create,c,dm_load_record<br/>
set,c,l,file_name<br/>
c:\temp\dumpfile.txt<br/>
set,c,l,relocate<br/>
T<br/>
dump,c,l<br/>
save,c,l<br/>
dump,c,l<br/>
getmessage,c,1 (note-this is a one)<br/>
destroy,c,l<br/>
exit</p>
<nav class="pagination group"></nav></div>
<div class="clear"></div>
</div>
</div>
</article>
```
