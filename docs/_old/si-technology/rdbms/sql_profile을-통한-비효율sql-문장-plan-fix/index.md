---
title: "SQL_PROFILE을 통한 비효율SQL 문장 plan fix"
date: "No Date"
---

SQL\_PROFILE을 통한 비효율SQL 문장 plan fix
===================================

by 
[박경원](https://appi77.github.io/my-tips/author/appi77/ "박경원이(가) 작성한 글")
·
Published 2019년 3월 28일
· Updated 2019년 3월 29일

— 문제된 SQL 확인  
— SQL\_ID 및 FULL\_TEXT 확인  
SELECT SQL\_ID,

SQL\_TEXT,

SQL\_FULLTEXT

FROM V$SQL

WHERE SQL\_TEXT LIKE ‘%DEPT D%’  
;

— 튜닝된 SQL 실행  
SELECT  
/\*+FIRST\_ROWS\*/ \*  
FROM DUAL  
WHERE  
ROWNUM <= 101  
;  
— Outline Data 추출  
SELECT PLAN\_TABLE\_OUTPUT FROM TABLE(DBMS\_XPLAN.DISPLAY\_CURSOR(NULL, NULL, ‘OUTLINE’));

–Outline Data  
————-

/\*+  
BEGIN\_OUTLINE\_DATA  
IGNORE\_OPTIM\_EMBEDDED\_HINTS  
OPTIMIZER\_FEATURES\_ENABLE(‘11.2.0.4’)  
DB\_VERSION(‘11.2.0.4’)  
OPT\_PARAM(‘\_b\_tree\_bitmap\_plans’ ‘false’)  
OPT\_PARAM(‘\_complex\_view\_merging’ ‘false’)  
OPT\_PARAM(‘\_optim\_peek\_user\_binds’ ‘false’)  
OPT\_PARAM(‘\_optimizer\_push\_pred\_cost\_based’ ‘false’)  
OPT\_PARAM(‘\_optimizer\_null\_aware\_antijoin’ ‘false’)  
OPT\_PARAM(‘\_bloom\_filter\_enabled’ ‘false’)  
OPT\_PARAM(‘\_optimizer\_extended\_cursor\_sharing’ ‘none’)  
OPT\_PARAM(‘\_optimizer\_connect\_by\_cost\_based’ ‘false’)  
OPT\_PARAM(‘\_optimizer\_extended\_cursor\_sharing\_rel’ ‘none’)  
OPT\_PARAM(‘\_optimizer\_adaptive\_cursor\_sharing’ ‘false’)  
OPT\_PARAM(‘\_optimizer\_use\_feedback’ ‘false’)  
OPT\_PARAM(‘star\_transformation\_enabled’ ‘true’)  
FIRST\_ROWS  
OUTLINE\_LEAF(@”SEL$335DD26A”)  
MERGE(@”SEL$3″)  
OUTLINE\_LEAF(@”SEL$1″)  
OUTLINE(@”SEL$2″)  
OUTLINE(@”SEL$3″)  
NO\_ACCESS(@”SEL$1″ “from$\_subquery$\_001″@”SEL$1″)  
INDEX\_RS\_ASC(@”SEL$335DD26A” “BH\_”@”SEL$3” (“DM\_SYSOBJECT\_S”.”I\_CABINET\_ID” “DM\_SYSOBJECT\_S”.”R\_CREATION\_DATE”  
“DM\_SYSOBJECT\_S”.”OWNER\_NAME” “DM\_SYSOBJECT\_S”.”GROUP\_NAME” “DM\_SYSOBJECT\_S”.”TITLE”))  
INDEX(@”SEL$335DD26A” “TT\_”@”SEL$3” (“UD\_DOCUMENT\_S”.”R\_OBJECT\_ID”))  
LEADING(@”SEL$335DD26A” “BH\_”@”SEL$3” “TT\_”@”SEL$3″)  
USE\_NL(@”SEL$335DD26A” “TT\_”@”SEL$3″)  
NLJ\_BATCHING(@”SEL$335DD26A” “TT\_”@”SEL$3”)  
END\_OUTLINE\_DATA  
\*/

–SQL\_PROFILE 등록  
DECLARE  
V\_SQL\_TEXT CLOB;  
BEGIN  
SELECT SQL\_FULLTEXT  
INTO V\_SQL\_TEXT  
FROM V$SQL  
WHERE SQL\_ID = ‘f76yur0mc5qrz’  
AND ROWNUM=1;

DBMS\_SQLTUNE.IMPORT\_SQL\_PROFILE(  
NAME => ‘MY\_PROFILE\_1’,  
DESCRIPTION => ‘MY\_PROFILE\_1’,  
CATEGORY => ‘MY\_PROFILE\_1’,  
SQL\_TEXT => V\_SQL\_TEXT,  
PROFILE => SQLPROF\_ATTR(‘FIRST\_ROWS’  
),  
REPLACE => TRUE,  
FORCE\_MATCH => TRUE — CURSOR\_SHARING 기능 사용  
);  
END;  
/

— SQL\_PROFILE 확인  
select \* from DBA\_SQL\_PROFILES;  
–기존 SQL\_PROFILE 삭제  
EXEC DBMS\_SQLTUNE.DROP\_SQL\_PROFILE(NAME =>’MY\_PROFILE\_1′);  
–SQL\_PROFILE DISABLE  
EXEC DBMS\_SQLTUNE.ALTER\_SQL\_PROFILE (NAME =>’MY\_PROFILE\_1′,ATTRIBUTE\_NAME=>’STATUS’,VALUE=>’DISABLED’);  
— SQL\_PROFILE 활성화  
ALTER SESSION SET SQLTUNE\_CATEGORY = MY\_PROFILE\_1 ;  
— 비활성화  
ALTER SESSION SET SQLTUNE\_CATEGORY = FALSE;

```html
<article class="post-599 post type-post status-publish format-standard hentry category-rdbms"><div class="post-inner group">
<h1 class="post-title entry-title">SQL_PROFILE을 통한 비효율SQL 문장 plan fix</h1>
<p class="post-byline">
   by   <span class="vcard author">
<span class="fn"><a href="https://appi77.github.io/my-tips/author/appi77/" rel="author" title="박경원이(가) 작성한 글">박경원</a></span>
</span>
   ·
                                Published <time class="published" datetime="2019년 3월 28일">2019년 3월 28일</time>
              · Updated <time class="updated" datetime="2019년 3월 29일">2019년 3월 29일</time></p>
<div class="clear"></div>
<div class="entry themeform">
<div class="entry-inner">
<p>— 문제된 SQL 확인<br/>
— SQL_ID 및 FULL_TEXT 확인<br/>
SELECT SQL_ID,</p>
<p>SQL_TEXT,</p>
<p>SQL_FULLTEXT</p>
<p>FROM V$SQL</p>
<p>WHERE SQL_TEXT LIKE ‘%DEPT D%’<br/>
;</p>
<p>— 튜닝된 SQL 실행<br/>
SELECT<br/>
/*+FIRST_ROWS*/ *<br/>
FROM DUAL<br/>
WHERE<br/>
ROWNUM &lt;= 101<br/>
;<br/>
— Outline Data 추출<br/>
SELECT PLAN_TABLE_OUTPUT FROM TABLE(DBMS_XPLAN.DISPLAY_CURSOR(NULL, NULL, ‘OUTLINE’));</p>
<p>–Outline Data<br/>
————-</p>
<p>/*+<br/>
BEGIN_OUTLINE_DATA<br/>
IGNORE_OPTIM_EMBEDDED_HINTS<br/>
OPTIMIZER_FEATURES_ENABLE(‘11.2.0.4’)<br/>
DB_VERSION(‘11.2.0.4’)<br/>
OPT_PARAM(‘_b_tree_bitmap_plans’ ‘false’)<br/>
OPT_PARAM(‘_complex_view_merging’ ‘false’)<br/>
OPT_PARAM(‘_optim_peek_user_binds’ ‘false’)<br/>
OPT_PARAM(‘_optimizer_push_pred_cost_based’ ‘false’)<br/>
OPT_PARAM(‘_optimizer_null_aware_antijoin’ ‘false’)<br/>
OPT_PARAM(‘_bloom_filter_enabled’ ‘false’)<br/>
OPT_PARAM(‘_optimizer_extended_cursor_sharing’ ‘none’)<br/>
OPT_PARAM(‘_optimizer_connect_by_cost_based’ ‘false’)<br/>
OPT_PARAM(‘_optimizer_extended_cursor_sharing_rel’ ‘none’)<br/>
OPT_PARAM(‘_optimizer_adaptive_cursor_sharing’ ‘false’)<br/>
OPT_PARAM(‘_optimizer_use_feedback’ ‘false’)<br/>
OPT_PARAM(‘star_transformation_enabled’ ‘true’)<br/>
FIRST_ROWS<br/>
OUTLINE_LEAF(@”SEL$335DD26A”)<br/>
MERGE(@”SEL$3″)<br/>
OUTLINE_LEAF(@”SEL$1″)<br/>
OUTLINE(@”SEL$2″)<br/>
OUTLINE(@”SEL$3″)<br/>
NO_ACCESS(@”SEL$1″ “from$_subquery$_001″@”SEL$1″)<br/>
INDEX_RS_ASC(@”SEL$335DD26A” “BH_”@”SEL$3” (“DM_SYSOBJECT_S”.”I_CABINET_ID” “DM_SYSOBJECT_S”.”R_CREATION_DATE”<br/>
“DM_SYSOBJECT_S”.”OWNER_NAME” “DM_SYSOBJECT_S”.”GROUP_NAME” “DM_SYSOBJECT_S”.”TITLE”))<br/>
INDEX(@”SEL$335DD26A” “TT_”@”SEL$3” (“UD_DOCUMENT_S”.”R_OBJECT_ID”))<br/>
LEADING(@”SEL$335DD26A” “BH_”@”SEL$3” “TT_”@”SEL$3″)<br/>
USE_NL(@”SEL$335DD26A” “TT_”@”SEL$3″)<br/>
NLJ_BATCHING(@”SEL$335DD26A” “TT_”@”SEL$3”)<br/>
END_OUTLINE_DATA<br/>
*/</p>
<p>–SQL_PROFILE 등록<br/>
DECLARE<br/>
V_SQL_TEXT CLOB;<br/>
BEGIN<br/>
SELECT SQL_FULLTEXT<br/>
INTO V_SQL_TEXT<br/>
FROM V$SQL<br/>
WHERE SQL_ID = ‘f76yur0mc5qrz’<br/>
AND ROWNUM=1;</p>
<p>DBMS_SQLTUNE.IMPORT_SQL_PROFILE(<br/>
NAME =&gt; ‘MY_PROFILE_1’,<br/>
DESCRIPTION =&gt; ‘MY_PROFILE_1’,<br/>
CATEGORY =&gt; ‘MY_PROFILE_1’,<br/>
SQL_TEXT =&gt; V_SQL_TEXT,<br/>
PROFILE =&gt; SQLPROF_ATTR(‘FIRST_ROWS’<br/>
),<br/>
REPLACE =&gt; TRUE,<br/>
FORCE_MATCH =&gt; TRUE — CURSOR_SHARING 기능 사용<br/>
);<br/>
END;<br/>
/</p>
<p>— SQL_PROFILE 확인<br/>
select * from DBA_SQL_PROFILES;<br/>
–기존 SQL_PROFILE 삭제<br/>
EXEC DBMS_SQLTUNE.DROP_SQL_PROFILE(NAME =&gt;’MY_PROFILE_1′);<br/>
–SQL_PROFILE DISABLE<br/>
EXEC DBMS_SQLTUNE.ALTER_SQL_PROFILE (NAME =&gt;’MY_PROFILE_1′,ATTRIBUTE_NAME=&gt;’STATUS’,VALUE=&gt;’DISABLED’);<br/>
— SQL_PROFILE 활성화<br/>
ALTER SESSION SET SQLTUNE_CATEGORY = MY_PROFILE_1 ;<br/>
— 비활성화<br/>
ALTER SESSION SET SQLTUNE_CATEGORY = FALSE;</p>
<nav class="pagination group"></nav></div>
<div class="clear"></div>
</div>
</div>
</article>
```
