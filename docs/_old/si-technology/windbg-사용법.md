---
title: "Windbg 사용 및 분석 방법"
date: "No Date"
---

Windbg 사용 및 분석 방법
=================

by 
[박경원](https://appi77.github.io/my-tips/author/appi77/ "박경원이(가) 작성한 글")
·
Published 2018년 10월 23일
· Updated 2019년 4월 20일

#### ▶ 심볼 경로 설정 방법(택1)

1. 환경변수설정에

   ```
   _NT_SYMBOL_PATH=srv*\\nas_hostname\edm5\DEBUG\windbg\OSSymbols_win7*https://msdl.microsoft.com/download/symbols;\\nas_hostname\edm5\DEBUG\windbg\MySymbols*https://mywebserver/symbols;C:\Windows\system32
   ```
2. Windbg의 File-> Symbol File Path(Ctrl+S) 에

   ```
   srv*\\nas_hostname\edm5\DEBUG\windbg\OSSymbols_win7*https://msdl.microsoft.com/download/symbols;\\nas_hostname\edm5\DEBUG\windbg\MySymbols*https://mywebserver/symbols;C:\Windows\system32
   ```

#### ▶ 심볼 복사 방법

1. command 에서 추가

   ```
   .sympath+ C:\Temp\dump
   => exe의 pdb파일 \\nas_hostname\edm5\DEBUG\windbg\MySymbols\symbols\exe에복사한다=> dll의 pdb파일 \\nas_hostname\edm5\DEBUG\windbg\MySymbols\symbols\dll에 복사한다
   ```

#### ▶ 심볼 확인 및 열기

* 모든 모듈의 심볼 확인 가능
  > lm
* 심볼 모두 올리기
  > ld \*
* 심볼 하나만 다시 올리기
  > ld ntdll
* 모듈과 심볼 확인
  >lmvm ntdll

#### ▶심볼 올리기 및 내리기

* 심볼이 맞지않아도 강제로 심볼 로드하기
  .reload /i SmartDisk.exe
* 심볼 모두 올리기
  .reload /f SmartDisk.exe
* 모든 심볼 올리기
  .reload /f
* 심볼 모두 내리기
  .reload /u (심볼 모두 내리기)
* 특정모듈 심볼 내리기
  .reload /u SmartDisk.exe

#### ▶ 소스 경로 설정 방법

Windbg의 File-> Source File Path(Ctrl+P) 에 소스폴더 지정

#### ▶ 덤프파일 분석 방법

```
> !analyze -a
DEFAULT_BUCKET_ID: 항목 확인
BUGCHECK_STR: 항목 확인 
ERROR_CODE 도 참고
```

예)  
DEFAULT\_BUCKET\_ID: BREAKPOINT\_NOSOS  
ERROR\_CODE: (NTSTATUS) 0x80000003  
BUGCHECK\_STR: BREAKPOINT\_NOSOS  
인 경우는 Application이 hang에 걸려 강제로 덤프한 경우이므로  
**!analyze -v -hang 으로 확인**

**BUGCHECK\_STR에 0x35 형태로 버그코드가 있을 경우**  
<https://docs.microsoft.com/en-us/windows-hardware/drivers/debugger/bug-check-code-reference2> 참조

!wow64exts.k : 콜스택을 x86 모드로 변환해서 보여줍니다.

!wow64exts.sw : 디버깅 모드를 x86모드로 변환합니다. (이후 k 를 입력하면 정상적인 x86 콜스택이 정상적으로 보입니다.) 동일한 효과 => **.load wow64exts** ; **.effmach x86**

~\*kb : 전체 스레드 및 스택 보기

#### ▶ 실제 분석했던 BUGCHECK\_STR 목록

```
BUGCHECK_STR : ACCESS_VIOLATION 액세스 위반 
BUGCHECK_STR:  APPLICATION_HANG 프로세스 멈춤

DEFAULT_BUCKET_ID: DRIVE_FAULT 드라이브 충돌 이거나 혹은 백신과의 충돌
```

#### ▶ 버전별 다운로드 정리

https://debugging.wellisolutions.de/windbg-versions/

```html
<article class="post-300 post type-post status-publish format-standard hentry category-debug category-si-technology"><div class="post-inner group">
<h1 class="post-title entry-title">Windbg 사용 및 분석 방법</h1>
<p class="post-byline">
   by   <span class="vcard author">
<span class="fn"><a href="https://appi77.github.io/my-tips/author/appi77/" rel="author" title="박경원이(가) 작성한 글">박경원</a></span>
</span>
   ·
                                Published <time class="published" datetime="2018년 10월 23일">2018년 10월 23일</time>
              · Updated <time class="updated" datetime="2019년 4월 20일">2019년 4월 20일</time></p>
<div class="clear"></div>
<div class="entry themeform">
<div class="entry-inner">
<h4>▶ 심볼 경로 설정 방법(택1)</h4>
<ol><li>환경변수설정에
<pre>_NT_SYMBOL_PATH=srv*\\nas_hostname\edm5\DEBUG\windbg\OSSymbols_win7*https://msdl.microsoft.com/download/symbols;\\nas_hostname\edm5\DEBUG\windbg\MySymbols*https://mywebserver/symbols;C:\Windows\system32</pre>
</li>
<li>Windbg의 File-&gt; Symbol File Path(Ctrl+S) 에
<pre>srv*\\nas_hostname\edm5\DEBUG\windbg\OSSymbols_win7*https://msdl.microsoft.com/download/symbols;\\nas_hostname\edm5\DEBUG\windbg\MySymbols*https://mywebserver/symbols;C:\Windows\system32</pre>
</li>
</ol><h4>▶ 심볼 복사 방법</h4>
<ol><li>command 에서 추가
<pre>.sympath+ C:\Temp\dump
=&gt; exe의 pdb파일 \\nas_hostname\edm5\DEBUG\windbg\MySymbols\<span style="color: #0000ff;">symbols\exe</span>에복사한다=&gt; dll의 pdb파일 \\nas_hostname\edm5\DEBUG\windbg\MySymbols\<span style="color: #0000ff;">symbols\dll</span>에 복사한다</pre></li>
</ol><h4>▶ 심볼 확인 및 열기</h4>
<ul><li>모든 모듈의 심볼 확인 가능
&gt; lm</li>
<li>심볼 모두 올리기
&gt; ld *</li>
<li>심볼 하나만 다시 올리기
&gt; ld ntdll</li>
<li>모듈과 심볼 확인
&gt;lmvm ntdll</li>
</ul><h4>▶심볼 올리기 및 내리기</h4>
<ul><li>심볼이 맞지않아도 강제로 심볼 로드하기
.reload /i SmartDisk.exe</li>
<li>심볼 모두 올리기
.reload /f SmartDisk.exe</li>
<li>모든 심볼 올리기
.reload /f</li>
<li>심볼 모두 내리기
.reload /u (심볼 모두 내리기)</li>
<li>특정모듈 심볼 내리기
.reload /u SmartDisk.exe</li>
</ul><h4>▶ 소스 경로 설정 방법</h4>
<p style="padding-left: 30px;">Windbg의 File-&gt; Source File Path(Ctrl+P) 에 소스폴더 지정</p>
<h4>▶ 덤프파일 분석 방법</h4>
<pre>&gt; !analyze -a
DEFAULT_BUCKET_ID: 항목 확인
BUGCHECK_STR: 항목 확인 
ERROR_CODE 도 참고</pre>
<p style="padding-left: 30px;">예)<br/><span style="font-size: 1rem;">DEFAULT_BUCKET_ID: BREAKPOINT_NOSOS<br/></span>ERROR_CODE: (NTSTATUS) 0x80000003<br/>
BUGCHECK_STR: BREAKPOINT_NOSOS<br/>
인 경우는 Application이 hang에 걸려 강제로 덤프한 경우이므로<br/><strong>!analyze -v -hang 으로 확인</strong></p>
<p style="padding-left: 30px;"><strong>BUGCHECK_STR에 0x35 형태로 버그코드가 있을 경우</strong><br/><a href="https://docs.microsoft.com/en-us/windows-hardware/drivers/debugger/bug-check-code-reference2">https://docs.microsoft.com/en-us/windows-hardware/drivers/debugger/bug-check-code-reference2</a> 참조</p>
<p style="padding-left: 30px;">!wow64exts.k : 콜스택을 x86 모드로 변환해서 보여줍니다.</p>
<p style="padding-left: 30px;">!wow64exts.sw : 디버깅 모드를 x86모드로 변환합니다. (이후 k 를 입력하면 정상적인 x86 콜스택이 정상적으로 보입니다.) 동일한 효과 =&gt; <span class="notranslate"><strong>.load wow64exts</strong></span> ; <span class="notranslate"><strong>.effmach x86</strong></span></p>
<p style="padding-left: 30px;">~*kb : 전체 스레드 및 스택 보기</p>
<h4>▶ 실제 분석했던 BUGCHECK_STR 목록</h4>
<pre>BUGCHECK_STR : ACCESS_VIOLATION 액세스 위반 
BUGCHECK_STR:  APPLICATION_HANG 프로세스 멈춤

DEFAULT_BUCKET_ID: DRIVE_FAULT 드라이브 충돌 이거나 혹은 백신과의 충돌</pre>
<h4>▶ 버전별 다운로드 정리</h4>
<p>https://debugging.wellisolutions.de/windbg-versions/</p>
<nav class="pagination group"></nav></div>
<div class="clear"></div>
</div>
</div>
</article>
```
