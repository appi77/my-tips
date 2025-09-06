---
title: "Crash Dump Files"
date: "No Date"
---

Crash Dump Files
================

by 
[박경원](https://appi77.github.io/my-tips/author/appi77/ "박경원이(가) 작성한 글")
·
Published 2018년 10월 25일
· Updated 2018년 11월 2일

Crash Dump Files은 특정한 시점의 메모리, 어플리케이션, 운영체제와 관련된 데이터를 가지고 있는 파일이다.  user-mode 크래쉬 덤프 파일은 어플리케이션에 오류가 발생했을 때 생성되고 kernel-mode 크래쉬 덤프 파일은 윈도우 자체에 오류가 발생했을 때 생성된다.

**1 .Kernel-Mode Dump files**

bcdedit /debug ON

**2.User-Mode Dump files**

User-Mode Dump 파일은 Full User-Mode Dump, Minidump 가 있음

▶ **Full User-Mode Dumps**full user-mode dump는 기본적인 user-mode 덤프 파일이다.  
이 파일은 프로세스의 전체 메모리 공간, 프로그램의 실행 파일 이미지, 핸들 테이블, 그 밖에 디버깅에 유용한 여러 정보를 포함한다.  
full user-mode dump 파일은 minidump로 축소시킬 수 있다. 단순히 디버거에 덤프 파일을 로드하고 ‘.dump’ 커맨드를 사용하여 새로운 minidump 형식의 덤프 파일을 저장한다.  
note. minidump라는 이름에도 불구하고, 가장 큰 minidump는 실제로 full user-mode dump보다 더 많은 정보를 가진다. 예를 들면, .dump /mf 혹은 .dump /ma는 .dump /f보다 더 크고 많은 정보를 가진 덤프 파일을 생성한다.  
user mode에서는 .dump /m[MiniOptions]이 가장 좋은 선택이다. 이 옵션 스위치를 사용하여 생성된 덤프 파일은 크기가 다양할 수 있다. 적절한 MiniOptions을 사용하여 포함될 정보를 명확하게 조절할 수 있다.

**▶ Minidumps**

어떤 프로세스와 관련된 메모리에서 선택된 부분적인 정보를 가지고 있는 user-mode dump 파일을 minidump라고 부른다. minidump 파일의 크기와 내용은 덤프의 대상이 되는 프로그램과 덤프를 만드는 어플리케이션에 따라서 다양하다. minidump 파일은 아주 크고 전체 메모리와 핸들 테이블을 포함하는 경우도 있고, 어쩔 때는 이보다 확연히 작을 수도 있다. 예를 들면, minidump 파일은 싱글 스레드에 대한 정보 혹은 실제로 참조되고 있는 모듈의 스택에 존재하는 정보만을 가지고 있을 수도 있다. 가장 큰 minidump 파일은 실제로 full user-dump보다 더 많은 정보를 가지고 있기 때문에 ‘minidump’라는 이름은 오해를 가져올 소지가 있다. 예를 들면, .dump /mf 혹은 .dump /ma는 .dump /f보다 더 많은 정보를 가지고 있는 덤프 파일을 만들어 낼 것이다. 이러한 이유 때문에, user-mode 덤프 파일을 생성할 때는 .dump /f보다는 .dump /m[MiniOption]를 사용하길 권장한다.

만약 디버거를 사용해서 minidump 파일을 생성하려고 한다면, 좀 더 정밀하게 포함되는 정보를 선택할 수 있다. 단순히 .dump /m 커맨드를 사용한다면 target process를 구성하는 로드된 모듈, thread 정보, 그리고 스택 정보에 대한 기본적인 정보만을 포함한 덤프를 만들어 낸다. 이것은 다음 옵션들에 의해서 변경될 수 있다.

|  |  |
| --- | --- |
| 옵션 | 덤프에 미치는 영향 |
| /ma | minidump의 모든 추가적인 옵션을 사용하는 것과 같은 효과를 낸다. /ma 옵션은 /mfFhut와 같다. 이것은 full memory data, 핸들 데이터, 로딩되지 않은 모듈 정보, 기본적인 메모리 정보,그리고 thread time 정보를 덤프 파일에 포함시킨다. |
| /mf | minidump 파일에 full memory data를 추가한다. target 어플리케이션이 소유하는 모든 접근 가능한 commit된 페이지를 포함한다. |
| /mF | minidump 파일에 메모리에 대한 모든 기본적인 정보를 추가한다. 이것은 유효한 메모리에 대한 정보만이 아니라 모든 메모리에 대한 기본적인 정보를 포함시킨다. 이것은 minidump를 가지고 디버깅을 할 때, 디버거가 프로세스에 대한 완전한 virtual memory layout을 재구성할 수 있도록 해준다. |
| /mh | minidump에 target process와 관련된 핸들에 대한 정보를 추가한다 |
| /mu | minidump에 로딩되지 않은 모듈에 대한 정보를 추가한다. 이것은 오직 Windows Server 2003과 그 이후 버전의 윈도우에서만 사용할 수 있다. |
| /mt | minidump에 추가적인 thread 정보를 추가한다. 여기에는 minidump를 디버깅할 때 .ttime 커맨드에 의해서 표시되는 thread time이 포함된다. |
| /mi | Secondary memory를 minidump 파일에 추가한다. secondary memory라는 것은 스택이나 backing store에 있는 포인터에 의해서 참조되는 메모리와 그 포인터가 가르키는 주소 근처의 약간의 지역을 뜻한다. (역자주: backing store는 paging이나 swapping 시스템에 의해서 main memory에서 밀려 난 데이터들을 저장하는, 일반적으로 하드디스크의 특정 부분을 의미한다.) |
| /mp | Process Environment Block(PEB)와 Thread Environment Block(TEB) 데이터를 minidump에 추가한다. 이것은 어플리케이션의 프로세스나 thread에 관련된 Windows 시스템 정보에 접근할 필요가 있을 때 유용하다. |
| /mw | 모든 commit된 read-write private page를 minidump에 추가한다. |
| /md | executable 이미지에 있는 모든 read-write 데이터 세그먼트를 minidump에 추가한다. |
| /mc | 이미지에 있는 코드 섹션을 추가한다. |
| /mr | minidump에서 스택 추적(stack trace)을 재생성하는데 불필요한 스택이나 store memory의 일부분을 제거한다. 또한 로컬 변수나 다른 데이터 타입의 값들도 삭제된다. 이 옵션은 minidump를 더 작게 만들지는 않는다.(이러한 메모리 섹션은 단지 0으로 채워진다.) 이 옵션은 다른 어플리케이션의 privacy를 보호하기 원할 때 유용하다. |
| /mR | minidump에서 full module path를 삭제한다. 오직 모듈 이름만 포함된다. 이 옵션은 사용자의 디렉토리 구조에 관련된 privacy를 보호하기를 원할 때 유용하다. |
| /mk “FileName” | Windows Vista only) user-mode minidump에 더하여 kernel-mode minidump도 생성한다. kernel-mode minidump는 user-mode minidump에 저장되어 있는 thread에 대한 dump로 제한된다. FileName은 따옴표로 둘러 싸여야 한다. |

이 옵션들은 혼합되어 사용될 수 있다. 예를 들면, .dump /mfiu 커맨드는 확실히 용량이 큰 minidump를 만드는데 사용할 수 있고, .dump /mrR은 사용자의 privacy를 보호할 수 있는 minidump를 만드는데 사용할 수 있다. 더욱 완전하고 자세한 문법을 위해서는 .dump 커맨드에 대한 섹션을 참조하시오.(이후에 번역하겠음).

minidump 파일의 자세한 내부 구조는 Microsoft Windows SDK에 있는 DbgHelp reference에 있다

출처 : <http://sixthman.tistory.com/77> 

**▶ Windows 버전별로 Crash Dump 생성하는 법**

1. Windows XP를 사용하는 경우

  – 윈도우 시작 -> 실행 -> 입력창에서 “drwtsn32″을 실행

– “크래시 덤프” 의 경로로 설정된 경로로 \*.dmp 파일이 생성됨

2. Windows Vista / Windows7 / Windows8 경우 (덤프를 남기는 기능이 기본적으로 꺼져있음)

 – 다음 경로의 레지스트리를 등록함(\*첨부 파일 참조-미니 덤프 생성하는 레지스트리)

레지스트리 위치 : HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps

|  |  |  |  |
| --- | --- | --- | --- |
| Value | 설명 | Type | Default value |
| DumpFolder | 덤프파일이 저장될 폴더 경로 | REG\_EXPAND\_SZ | %LOCALAPPDATA%\CrashDumps |
| DumpCount | 폴더에 저장되는 덤프파일의 최대 개수 | REG\_DWORD | 5 |
| DumpType | 1: 미니 덤프  2: 전체 덤프 | REG\_DWORD | 1 |

– 시스템재부팅

– 오류발생시 탐색기에서 %LOCALAPPDATA%\CrashDumps 경로에 \*.dmp 파일이 생성됨

```html
<article class="post-362 post type-post status-publish format-standard hentry category-debug"><div class="post-inner group">
<h1 class="post-title entry-title">Crash Dump Files</h1>
<p class="post-byline">
   by   <span class="vcard author">
<span class="fn"><a href="https://appi77.github.io/my-tips/author/appi77/" rel="author" title="박경원이(가) 작성한 글">박경원</a></span>
</span>
   ·
                                Published <time class="published" datetime="2018년 10월 25일">2018년 10월 25일</time>
              · Updated <time class="updated" datetime="2018년 11월 2일">2018년 11월 2일</time></p>
<div class="clear"></div>
<div class="entry themeform">
<div class="entry-inner">
<p><span lang="EN-US">Crash Dump Files</span>은 특정한 시점의 메모리, 어플리케이션, 운영체제와 관련된 데이터를 가지고 있는 파일이다<span lang="EN-US">.  </span><span lang="EN-US">user-mode </span>크래쉬 덤프 파일은 어플리케이션에 오류가 발생했을 때 생성되고 <span lang="EN-US">kernel-mode </span>크래쉬 덤프 파일은 윈도우 자체에 오류가 발생했을 때 생성된다.</p>
<p align="left"><span style="font-size: small;"><b><span lang="EN-US">1 .Kernel-Mode Dump files</span></b></span></p>
<p align="left">bcdedit /debug ON</p>
<p align="left"><span style="font-size: small;"><b><span lang="EN-US">2.User-Mode Dump files</span></b></span></p>
<p align="left"><span style="font-size: small;"><span lang="EN-US">User-Mode Dump 파일은 Full User-Mode Dump, </span></span><span style="font-size: small;"><span lang="EN-US">Minidump 가 있음</span></span></p>
<p align="left"><span style="font-size: small;"><span lang="EN-US">▶ </span></span><span style="font-size: small;"><b><span lang="EN-US">Full User-Mode Dumps<br/></span></b></span>full user-mode dump는 기본적인 user-mode 덤프 파일이다.<br/>
이 파일은 프로세스의 전체 메모리 공간, 프로그램의 실행 파일 이미지, 핸들 테이블, 그 밖에 디버깅에 유용한 여러 정보를 포함한다.<br/>
full user-mode dump 파일은 minidump로 축소시킬 수 있다. 단순히 디버거에 덤프 파일을 로드하고 ‘.dump’ 커맨드를 사용하여 새로운 minidump 형식의 덤프 파일을 저장한다.<br/>
note. minidump라는 이름에도 불구하고, 가장 큰 minidump는 실제로 full user-mode dump보다 더 많은 정보를 가진다. 예를 들면, .dump /mf 혹은 .dump /ma는 .dump /f보다 더 크고 많은 정보를 가진 덤프 파일을 생성한다.<br/>
user mode에서는 .dump /m[MiniOptions]이 가장 좋은 선택이다. 이 옵션 스위치를 사용하여 생성된 덤프 파일은 크기가 다양할 수 있다. 적절한 MiniOptions을 사용하여 포함될 정보를 명확하게 조절할 수 있다.</p>
<p align="left"><span style="font-size: small;"><b><span lang="EN-US">▶ Minidumps</span></b></span></p>
<p style="font-weight: 400;">어떤 프로세스와 관련된 메모리에서 선택된 부분적인 정보를 가지고 있는 user-mode dump 파일을 minidump라고 부른다. minidump 파일의 크기와 내용은 덤프의 대상이 되는 프로그램과 덤프를 만드는 어플리케이션에 따라서 다양하다. minidump 파일은 아주 크고 전체 메모리와 핸들 테이블을 포함하는 경우도 있고, 어쩔 때는 이보다 확연히 작을 수도 있다. 예를 들면, minidump 파일은 싱글 스레드에 대한 정보 혹은 실제로 참조되고 있는 모듈의 스택에 존재하는 정보만을 가지고 있을 수도 있다. 가장 큰 minidump 파일은 실제로 full user-dump보다 더 많은 정보를 가지고 있기 때문에 ‘minidump’라는 이름은 오해를 가져올 소지가 있다. 예를 들면, .dump /mf 혹은 .dump /ma는 .dump /f보다 더 많은 정보를 가지고 있는 덤프 파일을 만들어 낼 것이다. 이러한 이유 때문에, user-mode 덤프 파일을 생성할 때는 .dump /f보다는 .dump /m[MiniOption]를 사용하길 권장한다.</p>
<p style="font-weight: 400;">만약 디버거를 사용해서 minidump 파일을 생성하려고 한다면, 좀 더 정밀하게 포함되는 정보를 선택할 수 있다. 단순히 .dump /m 커맨드를 사용한다면 target process를 구성하는 로드된 모듈, thread 정보, 그리고 스택 정보에 대한 기본적인 정보만을 포함한 덤프를 만들어 낸다. 이것은 다음 옵션들에 의해서 변경될 수 있다.</p>
<table style="font-weight: 400;"><tbody><tr><td width="57"> 옵션</td>
<td width="543"> 덤프에 미치는 영향</td>
</tr><tr><td width="57">/ma</td>
<td width="543">minidump의 모든 추가적인 옵션을 사용하는 것과 같은 효과를 낸다. /ma 옵션은 /mfFhut와 같다. 이것은 full memory data, 핸들 데이터, 로딩되지 않은 모듈 정보, 기본적인 메모리 정보,그리고 thread time 정보를 덤프 파일에 포함시킨다.</td>
</tr><tr><td width="57">/mf</td>
<td width="543">minidump 파일에 full memory data를 추가한다. target 어플리케이션이 소유하는 모든 접근 가능한 commit된 페이지를 포함한다.</td>
</tr><tr><td width="57">/mF</td>
<td width="543">minidump 파일에 메모리에 대한 모든 기본적인 정보를 추가한다. 이것은 유효한 메모리에 대한 정보만이 아니라 모든 메모리에 대한 기본적인 정보를 포함시킨다. 이것은 minidump를 가지고 디버깅을 할 때, 디버거가 프로세스에 대한 완전한 virtual memory layout을 재구성할 수 있도록 해준다.</td>
</tr><tr><td width="57">/mh</td>
<td width="543">minidump에 target process와 관련된 핸들에 대한 정보를 추가한다</td>
</tr><tr><td width="57">/mu</td>
<td width="543">minidump에 로딩되지 않은 모듈에 대한 정보를 추가한다. 이것은 오직 Windows Server 2003과 그 이후 버전의 윈도우에서만 사용할 수 있다.</td>
</tr><tr><td width="57">/mt</td>
<td width="543">minidump에 추가적인 thread 정보를 추가한다. 여기에는 minidump를 디버깅할 때 .ttime 커맨드에 의해서 표시되는 thread time이 포함된다.</td>
</tr><tr><td width="57">/mi</td>
<td width="543">Secondary memory를 minidump 파일에 추가한다. secondary memory라는 것은 스택이나 backing store에 있는 포인터에 의해서 참조되는 메모리와 그 포인터가 가르키는 주소 근처의 약간의 지역을 뜻한다. (역자주: backing store는 paging이나 swapping 시스템에 의해서 main memory에서 밀려 난 데이터들을 저장하는, 일반적으로 하드디스크의 특정 부분을 의미한다.)</td>
</tr><tr><td width="57">/mp</td>
<td width="543">Process Environment Block(PEB)와 Thread Environment Block(TEB) 데이터를 minidump에 추가한다. 이것은 어플리케이션의 프로세스나 thread에 관련된 Windows 시스템 정보에 접근할 필요가 있을 때 유용하다.</td>
</tr><tr><td width="57">/mw</td>
<td width="543">모든 commit된 read-write private page를 minidump에 추가한다.</td>
</tr><tr><td width="57">/md</td>
<td width="543">executable 이미지에 있는 모든 read-write 데이터 세그먼트를 minidump에 추가한다.</td>
</tr><tr><td width="57">/mc</td>
<td width="543">이미지에 있는 코드 섹션을 추가한다.</td>
</tr><tr><td width="57">/mr</td>
<td width="543">minidump에서 스택 추적(stack trace)을 재생성하는데 불필요한 스택이나 store memory의 일부분을 제거한다. 또한 로컬 변수나 다른 데이터 타입의 값들도 삭제된다. 이 옵션은 minidump를 더 작게 만들지는 않는다.(이러한 메모리 섹션은 단지 0으로 채워진다.) 이 옵션은 다른 어플리케이션의 privacy를 보호하기 원할 때 유용하다.</td>
</tr><tr><td width="57">/mR</td>
<td width="543">minidump에서 full module path를 삭제한다. 오직 모듈 이름만 포함된다. 이 옵션은 사용자의 디렉토리 구조에 관련된 privacy를 보호하기를 원할 때 유용하다.</td>
</tr><tr><td width="57">/mk “FileName”</td>
<td width="543">Windows Vista only) user-mode minidump에 더하여 kernel-mode minidump도 생성한다. kernel-mode minidump는 user-mode minidump에 저장되어 있는 thread에 대한 dump로 제한된다. FileName은 따옴표로 둘러 싸여야 한다.</td>
</tr></tbody></table><p style="font-weight: 400;">이 옵션들은 혼합되어 사용될 수 있다. 예를 들면, .dump /mfiu 커맨드는 확실히 용량이 큰 minidump를 만드는데 사용할 수 있고, .dump /mrR은 사용자의 privacy를 보호할 수 있는 minidump를 만드는데 사용할 수 있다. 더욱 완전하고 자세한 문법을 위해서는 .dump 커맨드에 대한 섹션을 참조하시오.(이후에 번역하겠음).</p>
<p style="font-weight: 400;">minidump 파일의 자세한 내부 구조는 Microsoft Windows SDK에 있는 DbgHelp reference에 있다</p>
<p>출처 : <span lang="EN-US"><a href="http://sixthman.tistory.com/77" rel="noopener" target="_blank">http://sixthman.tistory.com/77</a> </span></p>
<p> </p>
<p lang="en-US"><span style="font-size: small;"><b><span lang="EN-US">▶ Windows 버전별로 Crash Dump 생성하는 법</span></b></span></p>
<p lang="en-US">1. Windows XP를 사용하는 경우</p>
<p>  – 윈도우 시작 -&gt; 실행 -&gt; 입력창에서 “drwtsn32″을 실행</p>
<p>– “크래시 덤프” 의 경로로 설정된 경로로 *.dmp 파일이 생성됨</p>
<p> </p>
<p lang="en-US">2. Windows Vista / Windows7 / Windows8 경우 (덤프를 남기는 기능이 기본적으로 꺼져있음)</p>
<p lang="en-US"> – 다음 경로의 레지스트리를 등록함(*첨부 파일 참조-미니 덤프 생성하는 레지스트리)</p>
<p> </p>
<p lang="en-US">레지스트리 위치 : HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps</p>
<p> </p>
<div align="left">
<div class="_contentScrollArea">
<div>
<table border="1" cellpadding="0" cellspacing="0" class="__se_tbl_ext _wideContent"><tbody><tr><td>
<p lang="en-US">Value</p>
</td>
<td>설명</td>
<td>
<p lang="en-US">Type</p>
</td>
<td>
<p lang="en-US">Default value</p>
</td>
</tr><tr><td>
<p lang="en-US">DumpFolder</p>
</td>
<td>덤프파일이 저장될 폴더 경로</td>
<td>
<p lang="en-US">REG_EXPAND_SZ</p>
</td>
<td>
<p lang="en-US">%LOCALAPPDATA%\CrashDumps</p>
</td>
</tr><tr><td>
<p lang="en-US">DumpCount</p>
</td>
<td>폴더에 저장되는 덤프파일의 최대 개수</td>
<td>
<p lang="en-US">REG_DWORD</p>
</td>
<td>
<p lang="en-US">5</p>
</td>
</tr><tr><td>
<p lang="en-US">DumpType</p>
</td>
<td>
<p lang="en-US">1: 미니 덤프</p>
<p lang="en-US">2: 전체 덤프</p>
</td>
<td>
<p lang="en-US">REG_DWORD</p>
</td>
<td>
<p lang="en-US">1</p>
</td>
</tr></tbody></table></div>
</div>
</div>
<p> </p>
<p>– 시스템재부팅</p>
<p>– 오류발생시 탐색기에서 %LOCALAPPDATA%\CrashDumps 경로에 *.dmp 파일이 생성됨</p>
<nav class="pagination group"></nav></div>
<div class="clear"></div>
</div>
</div>
</article>
```
