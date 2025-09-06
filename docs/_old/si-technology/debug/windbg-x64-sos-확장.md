---
title: "windbg – x64 SOS 확장"
date: "No Date"
---

windbg – x64 SOS 확장
===================

by 
[박경원](https://appi77.github.io/my-tips/author/appi77/ "박경원이(가) 작성한 글")
·
Published 2018년 11월 23일
· Updated 2019년 2월 25일

▶ 32비트 툴로 덤프받았는지 확인

64비트 머신에서 32비트 프로세스 덤프를 제대로 받았는지 확인  
크래시 덤프를로드 한 후 필요한 버전을 확인 합니다.  
>!peb  
… 중략  
PROCESSOR\_ARCHITECTURE=AMD64  
이렇게 나오면 잘못된것임  
PROCESSOR\_ARCHITECTURE=x86  
PROCESSOR\_ARCHITEW6432=AMD64  
이렇게 나오면 정상

64비트 윈도우에서 32비트 프로세스의 덤프를 받기위해서  
C:\Windows\SysWOW64\Taskmgr.exe  
을 사용합니다.

▶ 크래시 덤프 .NET버전 확인

덤프를 분석하는 PC와 .NET버전이 다를 경우  
크래시 덤프를로드 한 후 필요한 버전을 확인 합니다.  
>lm vm clr

.NET 3.5 이하에서는  
>lm vm mscorwks  
FileVersion: 2.0.50727.8762

이 버전이 포함 된 MS 업데이트를위한 google :  
sos.dll 2.0.50727.8762  
해당 파일을 확보한다.

>cordll -ve -u -l  
CLRDLL: C:\Windows\Microsoft.NET\Framework\v2.0.50727\mscordacwks.dll:2.0.50727.9035 f:0  
doesn’t match desired version 2.0.50727.8762 f:0  
CLRDLL: Loaded DLL \\xxx.xxx.xxx.xxx\ossymbols\mscordacwks\_x86\_x86\_2.0.50727.8762.dll\58E464915b0000\mscordacwks\_x86\_x86\_2.0.50727.8762.dll  
Automatically loaded SOS Extension  
CLR DLL status: Loaded DLL \\xxx.xxx.xxx.xxx\ossymbols\mscordacwks\_x86\_x86\_2.0.50727.8762.dll\58E464915b0000\mscordacwks\_x86\_x86\_2.0.50727.8762.dll

▶ windbg 6.12에서 sos.dll 및 mscordacwks.dll 적용방법

windbg를 새로 실행하거나  
Debug->Detach Debuggee / File->Clear Workspace(clear all) 후 Open Crash Dump..를 통해 덤프파일을 열기 한다.  
> !sym noisy  
> .load C:\windbg\sos\sos.2.0.50727.8784.dll

> !clrstack  
~OSSymbols\mscordacwks\_AMD64\_x86\_2.0.50727.8784.dll\5AB42E295b0000\mscordacwks\_AMD64\_x86\_2.0.50727.8784.dll not found  
경로에 파일을 찾을 수 없다고 한다.  
mscordacwks.dll 을 mscordacwks\_AMD64\_x86\_2.0.50727.8784.dll로 수정해서 해당 경로에 복사한다.

처음부터 다시 반복하면 오류없이 sos.dll이 load 된다.

>.reload

▶ windbg “.loadby sos” 명령어  
.NET 4.0 응용 프로그램을 디버깅할 때  
0:000> .loadby sos clr  
.NET 3.5 이하 응용 프로그램을 디버깅할 때  
0:000> .loadby sos mscorwks

0:000> !clrstack  
SOS does not support the current target architecture.  
이땐 다음 명령어로 확인 해본다  
0:000> .chain

Extension DLL search Path:  
C:\Program Files (x86)\Windows Kits\10\Debuggers\x86\WINXP;C:\Program Files (x86)\Win~  
Extension DLL chain:  
C:\Windows\Microsoft.NET\Framework\v2.0.50727\sos: image 2.0.50727.9035, API 1.0.0, built Wed Aug 29 21:02:45 2018  
[path: C:\Windows\Microsoft.NET\Framework\v2.0.50727\sos.dll]  
\\xxx.xxx.xxx.xxx\ossymbols\SOS\_x86\_x86\_2.0.50727.8762.dll\58E464915b0000\SOS\_x86\_x86\_2.0.50727.8762.dll: image 2.0.50727.8762, API 1.0.0, built Tue Apr 4 20:41:39 2017  
[path: \\xxx.xxx.xxx.xxx\ossymbols\SOS\_x86\_x86\_2.0.50727.8762.dll\58E464915b0000\SOS\_x86\_x86\_2.0.50727.8762.dll]  
dbghelp: image 10.0.17763.132, API 10.0.6,  
[path: C:\Program Files (x86)\Windows Kits\10\Debuggers\x86\dbghelp.dll]  
ext: image 10.0.17763.132, API 1.0.0,  
[path: C:\Program Files (x86)\Windows Kits\10\Debuggers\x86\winext\ext.dll]  
exts: image 10.0.17763.132, API 1.0.0,  
[path: C:\Program Files (x86)\Windows Kits\10\Debuggers\x86\WINXP\exts.dll]  
uext: image 10.0.17763.132, API 1.0.0,  
[path: C:\Program Files (x86)\Windows Kits\10\Debuggers\x86\winext\uext.dll]  
ntsdexts: image 10.0.17763.132, API 1.0.0,  
[path: C:\Program Files (x86)\Windows Kits\10\Debuggers\x86\WINXP\ntsdexts.dll]

0:000>!pe         => sos !PrintException을 확인 할 수 있음

```html
<article class="post-476 post type-post status-publish format-standard hentry category-debug"><div class="post-inner group">
<h1 class="post-title entry-title">windbg – x64 SOS 확장</h1>
<p class="post-byline">
   by   <span class="vcard author">
<span class="fn"><a href="https://appi77.github.io/my-tips/author/appi77/" rel="author" title="박경원이(가) 작성한 글">박경원</a></span>
</span>
   ·
                                Published <time class="published" datetime="2018년 11월 23일">2018년 11월 23일</time>
              · Updated <time class="updated" datetime="2019년 2월 25일">2019년 2월 25일</time></p>
<div class="clear"></div>
<div class="entry themeform">
<div class="entry-inner">
<p><span lang="EN-US">▶</span> 32비트 툴로 덤프받았는지 확인</p>
<p>64비트 머신에서 32비트 프로세스 덤프를 제대로 받았는지 확인<br/>
크래시 덤프를로드 한 후 필요한 버전을 확인 합니다.<br/>
&gt;!peb<br/>
… 중략<br/>
PROCESSOR_ARCHITECTURE=AMD64<br/>
이렇게 나오면 잘못된것임<br/>
PROCESSOR_ARCHITECTURE=x86<br/>
PROCESSOR_ARCHITEW6432=AMD64<br/>
이렇게 나오면 정상</p>
<p>64비트 윈도우에서 32비트 프로세스의 덤프를 받기위해서<br/>
C:\Windows\SysWOW64\Taskmgr.exe<br/>
을 사용합니다.</p>
<p><span lang="EN-US">▶</span> 크래시 덤프 .NET버전 확인</p>
<p>덤프를 분석하는 PC와 .NET버전이 다를 경우<br/>
크래시 덤프를로드 한 후 필요한 버전을 확인 합니다.<br/>
&gt;lm vm clr</p>
<p>.NET 3.5 이하에서는<br/>
&gt;lm vm mscorwks<br/>
FileVersion: 2.0.50727.8762</p>
<p>이 버전이 포함 된 MS 업데이트를위한 google :<br/>
sos.dll 2.0.50727.8762<br/>
해당 파일을 확보한다.</p>
<p>&gt;cordll -ve -u -l<br/>
CLRDLL: C:\Windows\Microsoft.NET\Framework\v2.0.50727\mscordacwks.dll:2.0.50727.9035 f:0<br/>
doesn’t match desired version 2.0.50727.8762 f:0<br/>
CLRDLL: Loaded DLL \\xxx.xxx.xxx.xxx\ossymbols\mscordacwks_x86_x86_2.0.50727.8762.dll\58E464915b0000\mscordacwks_x86_x86_2.0.50727.8762.dll<br/>
Automatically loaded SOS Extension<br/>
CLR DLL status: Loaded DLL \\xxx.xxx.xxx.xxx\ossymbols\mscordacwks_x86_x86_2.0.50727.8762.dll\58E464915b0000\mscordacwks_x86_x86_2.0.50727.8762.dll</p>
<p><span lang="EN-US">▶</span> windbg 6.12에서 sos.dll 및 mscordacwks.dll 적용방법</p>
<p>windbg를 새로 실행하거나<br/>
Debug-&gt;Detach Debuggee / File-&gt;Clear Workspace(clear all) 후 Open Crash Dump..를 통해 덤프파일을 열기 한다.<br/>
&gt; !sym noisy<br/>
&gt; .load C:\windbg\sos\sos.2.0.50727.8784.dll</p>
<p>&gt; !clrstack<br/>
~OSSymbols\mscordacwks_AMD64_x86_2.0.50727.8784.dll\5AB42E295b0000\mscordacwks_AMD64_x86_2.0.50727.8784.dll not found<br/>
경로에 파일을 찾을 수 없다고 한다.<br/>
mscordacwks.dll 을 mscordacwks_AMD64_x86_2.0.50727.8784.dll로 수정해서 해당 경로에 복사한다.</p>
<p>처음부터 다시 반복하면 오류없이 sos.dll이 load 된다.</p>
<p>&gt;.reload</p>
<p><span lang="EN-US">▶</span> windbg “.loadby sos” 명령어<br/>
.NET 4.0 응용 프로그램을 디버깅할 때<br/>
0:000&gt; .loadby sos clr<br/>
.NET 3.5 이하 응용 프로그램을 디버깅할 때<br/>
0:000&gt; .loadby sos mscorwks</p>
<p>0:000&gt; !clrstack<br/>
SOS does not support the current target architecture.<br/>
이땐 다음 명령어로 확인 해본다<br/><span style="font-size: 1rem;">0:000&gt; .chain</span></p>
<p>Extension DLL search Path:<br/>
C:\Program Files (x86)\Windows Kits\10\Debuggers\x86\WINXP;C:\Program Files (x86)\Win~<br/>
Extension DLL chain:<br/>
C:\Windows\Microsoft.NET\Framework\v2.0.50727\sos: image 2.0.50727.9035, API 1.0.0, built Wed Aug 29 21:02:45 2018<br/>
[path: C:\Windows\Microsoft.NET\Framework\v2.0.50727\sos.dll]<br/>
\\xxx.xxx.xxx.xxx\ossymbols\SOS_x86_x86_2.0.50727.8762.dll\58E464915b0000\SOS_x86_x86_2.0.50727.8762.dll: image 2.0.50727.8762, API 1.0.0, built Tue Apr 4 20:41:39 2017<br/>
[path: \\xxx.xxx.xxx.xxx\ossymbols\SOS_x86_x86_2.0.50727.8762.dll\58E464915b0000\SOS_x86_x86_2.0.50727.8762.dll]<br/>
dbghelp: image 10.0.17763.132, API 10.0.6,<br/>
[path: C:\Program Files (x86)\Windows Kits\10\Debuggers\x86\dbghelp.dll]<br/>
ext: image 10.0.17763.132, API 1.0.0,<br/>
[path: C:\Program Files (x86)\Windows Kits\10\Debuggers\x86\winext\ext.dll]<br/>
exts: image 10.0.17763.132, API 1.0.0,<br/>
[path: C:\Program Files (x86)\Windows Kits\10\Debuggers\x86\WINXP\exts.dll]<br/>
uext: image 10.0.17763.132, API 1.0.0,<br/>
[path: C:\Program Files (x86)\Windows Kits\10\Debuggers\x86\winext\uext.dll]<br/>
ntsdexts: image 10.0.17763.132, API 1.0.0,<br/>
[path: C:\Program Files (x86)\Windows Kits\10\Debuggers\x86\WINXP\ntsdexts.dll]</p>
<p></p>
<p><span style="font-size: 1rem;">0:000&gt;!pe         =&gt; sos !PrintException을 확인 할 수 있음</span></p>
<nav class="pagination group"></nav></div>
<div class="clear"></div>
</div>
</div>
</article>
```
