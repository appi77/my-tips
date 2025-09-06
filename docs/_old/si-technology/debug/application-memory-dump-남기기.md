---
title: "Memory Dump(crash dump) 남기기"
date: "No Date"
---

Memory Dump(crash dump) 남기기
===========================

by 
[박경원](https://appi77.github.io/my-tips/author/appi77/ "박경원이(가) 작성한 글")
·
Published 2018년 10월 26일
· Updated 2018년 10월 26일

덤프파일을 남기기 위해 Taskmgr, WinDbg, Post Mortem Debugging, Dr.Watson,시스템 오류 덤프 등을 상황에 맞게 사용 한다.

```
상황에 따른 메모리 덤프(크래시 덤프) 파일을 생성 방법
- application의 hang이나 오류 시 Taskmgr 사용
- application의 비정상종료 시 WinDbg 을 기본디버거로 등록하여 사용
- OS나 응용 프로그램에 문제가 발생하여 PC가 다운 시 %SystemRoot%\Minidump 확인
```

▶ Taskmgr

vista 이후 windows에서는 작업관리자에서 덤프파일를 의도적으로 생성할 수 있다.  
생성되는 위치는 C:\Users\{user\_name}\AppData\Local\Temp\{process\_name}.DMP 이다.

▶ WinDbg

[windbg](https://appi77.github.io/my-tips/download/windbg-for-dump/) 을 다운 받고 관리자 권한 커맨드창에서 “windbg.exe -I” 명령으로 기본 디버거로 등록 한다.  
등록 확인 :  “HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\AeDebug”  
등록 삭제 : “Debugger” 와 “Auto” Value 삭제

기본디버거가 등록된 후 오류가 발생하면 자동으로 실행된 WinDbg의 command 창에서 “.dump /ma c:\temp\my.dmp” 을 실행하여 덤프파일을 생성한다.

▶ Post Mortem Debugging

Visual Studio가 설치된 PC에서 실행중인 프로세스가 비정상종료되면  Just-In-Time Debugger가 실행되고 문제된 프로세스가 자동으로 Attach된다. 디버거를 사용하여 메모리 덤프를 작성한다.

▶ Dr.Watson

[Dr.Watson](https://appi77.github.io/my-tips/download/dr-watson/) 을 다운 받아  “drwtsn32 -i” 으로 기본 디버거로 등록한다.  
등록 확인 :  “HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\AeDebug”  
등록 삭제 : “Debugger” 와 “Auto” Value 삭제

![](https://appi77.github.io/my-tips/wordpress/wp-content/uploads/2018/10/img_5bd256b8e524a.png)Dr.Watson을 실행하여 “크래시 덤프 유형” 을 “전체”로 선택합니다.

기본디버거가 등록된 후 오류가 발생하면 로그 파일 경로에 덤프파일이 생성됩니다.

▶ 시스템 오류의 메모리 덤프파일(memory dump)

컴퓨터 작업 도중에 OS나 응용 프로그램에 문제가 발생하여 PC가 다운되는 시스템 오류가 발생하면 %SystemRoot%\Minidump 폴더에 자동으로 덤프파일이 생성된다.  
메모리 덤프파일을 비활성화하거나 디버깅 정보 쓰기를 변경하고 싶으면 시작 및 복구 창에서 조정한다.  
![](https://appi77.github.io/my-tips/wordpress/wp-content/uploads/2018/10/img_5bd26425994cb.png)

```html
<article class="post-368 post type-post status-publish format-standard hentry category-debug"><div class="post-inner group">
<h1 class="post-title entry-title">Memory Dump(crash dump) 남기기</h1>
<p class="post-byline">
   by   <span class="vcard author">
<span class="fn"><a href="https://appi77.github.io/my-tips/author/appi77/" rel="author" title="박경원이(가) 작성한 글">박경원</a></span>
</span>
   ·
                                Published <time class="published" datetime="2018년 10월 26일">2018년 10월 26일</time>
              · Updated <time class="updated" datetime="2018년 10월 26일">2018년 10월 26일</time></p>
<div class="clear"></div>
<div class="entry themeform">
<div class="entry-inner">
<p>덤프파일을 남기기 위해 T<span style="font-size: small;"><span lang="EN-US">askmgr, WinDbg, </span></span>Post Mortem Debugging, Dr.Watson,시스템 오류 덤프 등을 상황에 맞게 사용 한다.</p>
<pre>상황에 따른 메모리 덤프(크래시 덤프) 파일을 생성 방법
- application의 hang이나 오류 시 Taskmgr 사용
- application의 비정상종료 시 WinDbg 을 기본디버거로 등록하여 사용
- OS나 응용 프로그램에 문제가 발생하여 PC가 다운 시 %SystemRoot%\Minidump 확인</pre>
<p><span id="more-368"></span><br/><span style="font-size: small;"><span lang="EN-US">▶ Taskmgr</span></span></p>
<p>vista 이후 windows에서는 작업관리자에서 덤프파일를 의도적으로 생성할 수 있다.<br/>
생성되는 위치는 <span style="font-size: 1rem;">C:\Users\{user_name}\AppData\Local\Temp\{process_name}.DMP 이다.</span></p>
<p><span style="font-size: small;"><span lang="EN-US">▶ </span></span>WinDbg</p>
<p><a href="https://appi77.github.io/my-tips/download/windbg-for-dump/">windbg</a> 을 다운 받고 관리자 권한 커맨드창에서 “windbg.exe -I” 명령으로 기본 디버거로 등록 한다.<br/>
등록 확인 :  “HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\AeDebug”<br/>
등록 삭제 : “Debugger” 와 “Auto” Value 삭제</p>
<p>기본디버거가 등록된 후 오류가 발생하면 자동으로 실행된 WinDbg의 command 창에서 “.dump /ma c:\temp\my.dmp” 을 실행하여 덤프파일을 생성한다.</p>
<p><span style="font-size: small;"><span lang="EN-US">▶ </span></span>Post Mortem Debugging</p>
<p>Visual Studio가 설치된 PC에서 실행중인 프로세스가 비정상종료되면  Just-In-Time Debugger가 실행되고 문제된 프로세스가 자동으로 Attach된다. 디버거를 사용하여 메모리 덤프를 작성한다.</p>
<p><span style="font-size: small;"><span lang="EN-US">▶ </span></span>Dr.Watson</p>
<p><a href="https://appi77.github.io/my-tips/download/dr-watson/">Dr.Watson</a> 을 다운 받아  “drwtsn32 -i” 으로 기본 디버거로 등록한다.<br/>
등록 확인 :  “HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\AeDebug”<br/>
등록 삭제 : “Debugger” 와 “Auto” Value 삭제</p>
<p id="zjYwhhS"><img alt="" class="size-full wp-image-371 alignleft" sizes="(max-width: 451px) 100vw, 451px" src="https://appi77.github.io/my-tips/wordpress/wp-content/uploads/2018/10/img_5bd256b8e524a.png" srcset="https://appi77.github.io/my-tips/wordpress/wp-content/uploads/2018/10/img_5bd256b8e524a.png 451w,https://appi77.github.io/my-tips/wordpress/wp-content/uploads/2018/10/img_5bd256b8e524a-100x100.png 100w,https://appi77.github.io/my-tips/wordpress/wp-content/uploads/2018/10/img_5bd256b8e524a-150x150.png 150w,https://appi77.github.io/my-tips/wordpress/wp-content/uploads/2018/10/img_5bd256b8e524a-297x300.png 297w"/>Dr.Watson을 실행하여 “크래시 덤프 유형” 을 “전체”로 선택합니다.</p>
<p>기본디버거가 등록된 후 오류가 발생하면 로그 파일 경로에 덤프파일이 생성됩니다.</p>
<p> </p>
<p> </p>
<p> </p>
<p> </p>
<p> </p>
<p> </p>
<p>▶ 시스템 오류의 메모리 덤프파일(memory dump)</p>
<p>컴퓨터 작업 도중에 OS나 응용 프로그램에 문제가 발생하여 PC가 다운되는 시스템 오류가 발생하면 %SystemRoot%\Minidump 폴더에 자동으로 덤프파일이 생성된다.<br/>
메모리 덤프파일을 비활성화하거나 디버깅 정보 쓰기를 변경하고 싶으면 시작 및 복구 창에서 조정한다.<br/><img alt="" class="alignnone size-full wp-image-380" sizes="(max-width: 453px) 100vw, 453px" src="https://appi77.github.io/my-tips/wordpress/wp-content/uploads/2018/10/img_5bd26425994cb.png" srcset="https://appi77.github.io/my-tips/wordpress/wp-content/uploads/2018/10/img_5bd26425994cb.png 453w,https://appi77.github.io/my-tips/wordpress/wp-content/uploads/2018/10/img_5bd26425994cb-287x300.png 287w" style="font-size: 1rem;"/></p>
<nav class="pagination group"></nav></div>
<div class="clear"></div>
</div>
</div>
</article>
```
