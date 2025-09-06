---
title: "symbol 확인 및 로드"
date: "No Date"
---

symbol 확인 및 로드
==============

by 
[박경원](https://appi77.github.io/my-tips/author/appi77/ "박경원이(가) 작성한 글")
·
Published 2018년 10월 29일
· Updated 2018년 11월 22일

▶ symbol 확인  
symbol 이 제대로 로딩되었는지 확인하는 방법

> !sym noisy  
noisy mode – symbol prompts on  
> .reload /f [dll or exe module]  
SYMSRV:  …  – not found  
SYMSRV: https://msdl.microsoft.com/download/symbols/… – not found  
DBGHELP: … – mismatched pdb  
DBGHELP: … – **no symbols loaded**> .reload /f              //모든 모듈 다시 불러온다

심볼이 잘못된 경우 마지막 줄에 no symbols loaded로 표시된다.

또 다른 symbol 정보 확인하는 방법

> !chksym  [dll or exe module]

quiet 모드로 바꾸기 위해서는

!sym quiet  
quiet mode – symbol prompts on  
을 실행한다.

▶ ChkMatch 확인

[ChkMatch.exe](https://appi77.github.io/my-tips/download/chkmatch-exe/)를 다운받는다

c:\{my util}\ChkMatch.exe -c [ExeFile DebugInfoFile]  
…  
…  
Result : Unmatched (reason: Signature mismatch)

-m 옵션과 함께 호출되면 디버그 정보 파일을 수정하려고 시도한다.  
c:\{my util}ChkMatch.exe -m [ExeFile DebugInfoFile]  
Result : Success

참고 <http://www.debuginfo.com/tools/chkmatch.html>

▶ SOS.DLL 오류 시

.load C:\Windows\Microsoft.NET\Framework\v4.0.30319\sos.dll

```html
<article class="post-428 post type-post status-publish format-standard hentry category-debug"><div class="post-inner group">
<h1 class="post-title entry-title">symbol 확인 및 로드</h1>
<p class="post-byline">
   by   <span class="vcard author">
<span class="fn"><a href="https://appi77.github.io/my-tips/author/appi77/" rel="author" title="박경원이(가) 작성한 글">박경원</a></span>
</span>
   ·
                                Published <time class="published" datetime="2018년 10월 29일">2018년 10월 29일</time>
              · Updated <time class="updated" datetime="2018년 11월 22일">2018년 11월 22일</time></p>
<div class="clear"></div>
<div class="entry themeform">
<div class="entry-inner">
<p><span style="font-size: small;"><span lang="EN-US">▶</span></span> symbol 확인<br/>
symbol 이 제대로 로딩되었는지 확인하는 방법</p>
<p style="padding-left: 30px;"><span style="font-size: 1rem;">&gt; !sym noisy<br/></span>noisy mode – symbol prompts on<br/>
&gt; .reload /f [dll or exe module]<br/>
SYMSRV:  …  – not found<br/>
SYMSRV: https://msdl.microsoft.com/download/symbols/… – not found<br/>
DBGHELP: … – mismatched pdb<br/>
DBGHELP: … – <strong>no symbols loaded<br/></strong>&gt; .reload /f              //모든 모듈 다시 불러온다</p>
<p>심볼이 잘못된 경우 마지막 줄에 no symbols loaded로 표시된다.<strong><br/></strong></p>
<p>또 다른 symbol 정보 확인하는 방법</p>
<p style="padding-left: 30px;"><span style="font-size: 1rem;">&gt; !chksym  [dll or exe module]</span></p>
<p><span style="font-size: 1rem;">quiet 모드로 바꾸기 위해서는</span></p>
<p style="padding-left: 30px;"><span style="font-size: 1rem;">!sym quiet<br/></span>quiet mode – symbol prompts on<br/>
을 실행한다.</p>
<p><span style="font-size: small;"><span lang="EN-US">▶</span></span> ChkMatch 확인</p>
<p><a href="https://appi77.github.io/my-tips/download/chkmatch-exe/">ChkMatch.exe</a>를 다운받는다</p>
<p>c:\{my util}\ChkMatch.exe -c [ExeFile DebugInfoFile]<br/>
…<br/>
…<br/>
Result : Unmatched (reason: Signature mismatch)</p>
<p>-m 옵션과 함께 호출되면 디버그 정보 파일을 수정하려고 시도한다.<br/>
c:\{my util}ChkMatch.exe -m [ExeFile DebugInfoFile]<br/>
Result : Success</p>
<p>참고 <a href="http://www.debuginfo.com/tools/chkmatch.html">http://www.debuginfo.com/tools/chkmatch.html</a></p>
<p> </p>
<p class="csharpcode"><span style="font-size: small;"><span lang="EN-US">▶</span></span> SOS.DLL 오류 시</p>
<p class="csharpcode">.load C:\Windows\<span class="skimlinks-unlinked">Microsoft.NET\Framework\v4.0.30319\sos.dll</span></p>
<p> </p>
<p> </p>
<nav class="pagination group"></nav></div>
<div class="clear"></div>
</div>
</div>
</article>
```
