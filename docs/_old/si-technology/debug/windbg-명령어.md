---
title: "windbg 명령어"
date: "No Date"
---

windbg 명령어
==========

by 
[박경원](https://appi77.github.io/my-tips/author/appi77/ "박경원이(가) 작성한 글")
·
Published 2018년 10월 25일
· Updated 2019년 2월 25일

#### ▶ WinDbg 에는 3 종류의 명령어가 있다.

1. 일반 명령 : 일반적으로 사용하는 디버깅에 관련된 명령어 들이다. 브레이크 설정(bp), 타겟 제어(p,g) 등등
2. 메타 명령 : 디버거에 관련된 명령이다. 명령어 앞에 . 이 붙는다. 디버깅 심벌 경로 설정 (.sympath ), 모듈 심벌 로드 (.reload ) 등등
3. 확장 명령 : 외부 dll 로 제작된 명령이다(일종의 플러그인 ). 명령어 앞에 ! 이 붙는다. 예외상황분석( !analyze –v ) , 프로세스 구조체 보기 ( !peb ) 등등

#### ▶ 주요 명령어

* **k : stack trace**  
  현재 스레드의 callstack을 출력

**k + [옵션] (예 : kbn)**

![](https://appi77.github.io/my-tips/wordpress/wp-content/uploads/2018/10/img_5bd29f90b246f.png)  
# : 프레임번호  
ChildEBP : Child 함수의 EBP  
RetAddr : Child 함수의 리턴어드레스  
Args to Child : Chile 함수에 전달된 아규먼트  
맨우측 : Child 함수의 주소.심볼

* **~ : thread control**  
  해당 thread로 Context 스위치 또는 해당 thread에 대한 정보 표시

**~ + 스레드 번호 + 명령 (예 : ~7s )**

~. : 모든 스레드의 정보 표시  
~\* : 모든 스레드의 정보 표시(more)  
~\*k : 모든 스레드의 Call Stack 표시  
~7 : 7번 스레드의 정보 표시  
~7s : 7번 스레드로 Context Switch. 이후 해당 스레드 Context에서 변수 조회나 Call Stack 확인 등이 가능  
~7k : 7번 스레드의 Call Stack 표시  
~# : 예외를 일으킨 쓰레드 표시

* **stack trace 에 사용되는 명령어들**

1. 전체 Thread 확인 : ~  
   suspend 값 확인( 0이면 동작중인 Thread)
2. 전체 Thread의 간략한 정보 확인 : ~\*
3. 해당 Thread 로 Context Switch : ~[TID]s, ~스레드번호s
4. 현재 Thread의 Call Stack 표시(frame 번호 확득) : kbn or kvn
5. 해당 Call Stack frame 으로 Context 이동 : .frame /c [frame 번호]
6. 로컬 변수 확인 : dv
7. Call Stack frame reset : .cxr
8. 이전 프레임(프레임 번호 큰 쪽)으로 이동할 때는 .frame /c 반복 실행, 나중 프레임(프레임 번  
   호가 작은 쪽)으로 되돌아가려면 .cxr 후 다시 .frame /c

<http://kskang.tistory.com/58>

#### ▶ 명령어표

출처: [http://darpangs.tistory.com/entry/WinDbg-명령어-정리-1](http://darpangs.tistory.com/entry/WinDbg-%EB%AA%85%EB%A0%B9%EC%96%B4-%EC%A0%95%EB%A6%AC-1)

|  |  |  |  |
| --- | --- | --- | --- |
| ommand | option | usage | Desc |
| 종료 |  |  |  |
| q |  |  | 디버깅 종료 |
| qd |  |  | 디버깅 종료;연결해제 |
| 디버깅 환경정보 |  |  |  |
| vertarget |  |  | 타겟 컴퓨터 정보 표시 |
| version |  |  | 디버그 환경 정보 표시 |
| .lastevent |  |  | 마지막 디버그 이벤트 정보 표시 |
| || |  |  | 디버깅 세션 정보 표시 |
| sumble & sorurce |  |  |  |
| .symfix |  |  | MS 심볼경로 설정 |
| .sympath |  |  | 심볼경로 확인/설정 |
| .sym noisy |  |  | 심볼파일 검색 과정을 출력 |
| .srcpath |  |  | 소스경로 설정 |
| .srcnoisy |  | .srcnoisy 1 | 소스경로 검색 과정을 출력 |
| 모듈 |  |  |  |
| lm |  | l | 로드된 모듈만 표시 |
|  |  | m [pattern] | 패턴과 일치되는 모듈만 표시 |
|  |  | v | 모듈 상세정보 표시 |
| !lmi | !lmi ntdll.dll |  | 모듈 상세정보 표시 |
| .reload |  | /f [m\_name] | 심볼을 즉시 로드 |
| x | X ntdll!\* | /v | 심볼 타입을 표시. |
|  | X \*!\*abc\* | /t | 데이터 타입을 표시 |
|  |  | /n | 이름순으로 정렬 |
| ln |  | ln [address] | 해당 주소에 근접한 심볼의 정보 표시 |
| 레지스터 |  |  |  |
| r |  |  | 레지스터 정보 표시 |
| r $proc |  |  | 현재 프로세스의 PEB주소( user-mode) |
|  |  |  | 현재 프로세스의 EPROcESS주소( kernel-mode) |
| r $thread |  |  | 현재 스레드의 TEB주소( user-mode) |
|  |  |  | 현재 스레드의 ETHREAD주소( kernel-mode) |
| r $tpid |  |  | 현재 프로세스 ID(PID) |
| r $tid |  |  | 현재 스레드 ID(TID) |
| 언어셈블 |  |  |  |
| u |  |  | 언어셈블 |
|  |  | f | 언어셈블(함수전체) |
|  |  | b | 언어셈블(ip이전의 8개 명령어) |
| 콜스택 |  |  |  |
| k |  | [n] | 콜스택 정보표시 |
|  |  | p | 함수정보 출력 |
|  |  | b | 인자표시 |
|  |  | n | 프레임번호 |
|  |  | v | FPO정보 표시 |
|  |  | f | 스택 사용량 표시 |
| break point |  |  |  |
| bp | bp 0x123456 |  | bp 설정 |
| bl |  |  | bp 리스트 출력 |
| bc | bc \* | [frame\_no] |  | bp 삭제 |
| bd,be | bc \* | [frame\_no] |  | bp disable/enable |
| bm | bm notepad!\*Win\* |  | 패턴과 일치하는 모든심볼에 bp설정 |
| bu | bu aaa!bbb |  | 로드되지 않은 심볼에 대한 bp설정 |
| ba |  |  | 특정 주소에 access시 bp |
| 지역변수 |  |  |  |
| dv | dv modulr!test\* |  |  |
|  |  | /i | 심볼유형과 인자유형 표시 |
|  |  | /V | 변수저장 위치 표시( register or address ) |
| 데이터유형 |  |  |  |
| dt | df \_EPROCESS 0xaddr |  | 주소를 특정 데이터 형으로 변환해서 표시 |
| du |  |  | Unicode string 표시 |
| da |  |  | Ansi string 표시 |
| dc |  |  |  |
| db |  |  |  |
| dy |  |  |  |
|  |  |  |  |
| !address | !address |  |  |
|  | !address [address] |  |  |
| 프로세스 & 스레드 정보 |  |  |  |
| !peb |  |  | PEB(Process Environment Block)표시 |
| !teb |  |  | TEB(Thread Environment Block) 표시 |
|  |  |  |  |
| !gle |  |  | API의 마지막 에러코드 표시 |
| 실행 제어 |  |  |  |
| t |  |  | Trace |
| ~.t |  |  | 다른 스레드를 중지시킨 상태에서 하나의 statementt실행 |
| g |  |  |  |
| p |  |  | Step Over |
| gu | gu |  | 현재함수가 복귀할 때 까지 실행 |
|  | ~0 gu |  | 스레드 0을 제외한 모든 스레드를 freeze함 |
| wt |  |  | 내부에서 호출된 함수와 함수호출 횟수등의 정보 표시 |
| .cxr |  |  | 컨텍스트 변경 |
| !ready |  |  |  |
| .thread |  |  |  |
| !thread |  |  |  |
| .trap |  |  |  |
| .process |  |  |  |
| !process |  |  |  |
| ed |  |  |  |
| eb | eb .-6 90 90 90 90 90 90 |  | 6byte를 NOP(0x90)으로 변경 |
| !error | !error [error code] |  | 에러코드 정보표시 |

출처: <http://jangpd007.tistory.com/203> [참 놀라운 세상]

```html
<article class="post-364 post type-post status-publish format-standard hentry category-debug"><div class="post-inner group">
<h1 class="post-title entry-title">windbg 명령어</h1>
<p class="post-byline">
   by   <span class="vcard author">
<span class="fn"><a href="https://appi77.github.io/my-tips/author/appi77/" rel="author" title="박경원이(가) 작성한 글">박경원</a></span>
</span>
   ·
                                Published <time class="published" datetime="2018년 10월 25일">2018년 10월 25일</time>
              · Updated <time class="updated" datetime="2019년 2월 25일">2019년 2월 25일</time></p>
<div class="clear"></div>
<div class="entry themeform">
<div class="entry-inner">
<h4 align="left"><span lang="EN-US">▶ </span><span style="font-size: 1rem;">WinDbg 에는 3 종류의 명령어가 있다.</span></h4>
<ol><li>일반 명령 : 일반적으로 사용하는 디버깅에 관련된 명령어 들이다. 브레이크 설정(bp), 타겟 제어(p,g) 등등</li>
<li>메타 명령 : 디버거에 관련된 명령이다. 명령어 앞에 . 이 붙는다. 디버깅 심벌 경로 설정 (.sympath ), 모듈 심벌 로드 (.reload ) 등등</li>
<li>확장 명령 : 외부 dll 로 제작된 명령이다(일종의 플러그인 ). 명령어 앞에 ! 이 붙는다. 예외상황분석( !analyze –v ) , 프로세스 구조체 보기 ( !peb ) 등등</li>
</ol><h4 align="left"><span lang="EN-US"> </span><span lang="EN-US">▶ </span><span lang="EN-US">주요 </span><span style="font-size: 1rem;">명령어</span></h4>
<ul><li><strong>k : stack trace</strong><br/>
현재 스레드의 callstack을 출력</li>
</ul><p style="padding-left: 30px;"><strong>k + [옵션] (예 : kbn)</strong></p>
<p id="QYiRbkF" style="padding-left: 60px;"><img alt="" class="alignnone size-full wp-image-391" sizes="(max-width: 575px) 100vw, 575px" src="https://appi77.github.io/my-tips/wordpress/wp-content/uploads/2018/10/img_5bd29f90b246f.png" srcset="https://appi77.github.io/my-tips/wordpress/wp-content/uploads/2018/10/img_5bd29f90b246f.png 575w,https://appi77.github.io/my-tips/wordpress/wp-content/uploads/2018/10/img_5bd29f90b246f-300x76.png 300w"/><br/>
# : 프레임번호<br/>
ChildEBP : Child 함수의 EBP<br/>
RetAddr : Child 함수의 리턴어드레스<br/>
Args to Child : Chile 함수에 전달된 아규먼트<br/>
맨우측 : Child 함수의 주소.심볼</p>
<ul><li><strong>~ : thread control</strong><br/>
해당 thread로 Context 스위치 또는 해당 thread에 대한 정보 표시</li>
</ul><p style="padding-left: 30px;"><strong>~ + 스레드 번호 + 명령 (예 : ~7s )</strong></p>
<p id="QYiRbkF" style="padding-left: 60px;">~. : 모든 스레드의 정보 표시<br/>
~* : 모든 스레드의 정보 표시(more)<br/>
~*k : 모든 스레드의 Call Stack 표시<br/>
~7 : 7번 스레드의 정보 표시<br/>
~7s : 7번 스레드로 Context Switch. 이후 해당 스레드 Context에서 변수 조회나 Call Stack 확인 등이 가능<br/>
~7k : 7번 스레드의 Call Stack 표시<br/><span style="color: #ff0000;">~# : 예외를 일으킨 쓰레드 표시</span></p>
<ul><li><strong>stack trace 에 사용되는 명령어들</strong></li>
</ul><ol><li>전체 Thread 확인 : ~<br/>
suspend 값 확인( 0이면 동작중인 Thread)</li>
<li>전체 Thread의 간략한 정보 확인 : ~*</li>
<li>해당 Thread 로 Context Switch : ~[TID]s, ~스레드번호s</li>
<li>현재 Thread의 Call Stack 표시(frame 번호 확득) : kbn or kvn</li>
<li>해당 Call Stack frame 으로 Context 이동 : .frame /c [frame 번호]</li>
<li>로컬 변수 확인 : dv</li>
<li>Call Stack frame reset : .cxr</li>
<li>이전 프레임(프레임 번호 큰 쪽)으로 이동할 때는 .frame /c 반복 실행, 나중 프레임(프레임 번<br/>
호가 작은 쪽)으로 되돌아가려면 .cxr 후 다시 .frame /c</li>
</ol><p><a href="http://kskang.tistory.com/58">http://kskang.tistory.com/58</a></p>
<div id="megamenu-wp-page">
<div class="hfeed site" id="page">
<div class="wrapper" id="main">
<div class="site-content" id="primary">
<div id="content" role="main">
<article class="post-362 post type-post status-publish format-standard hentry category-debug" id="post-362"><div class="entry-content">
<h4 align="left"><span lang="EN-US">▶ </span><span style="font-size: 1rem;">명령어표</span></h4>
</div>
</article></div>
</div>
</div>
</div>
</div>
<p>출처: <a href="http://darpangs.tistory.com/entry/WinDbg-%EB%AA%85%EB%A0%B9%EC%96%B4-%EC%A0%95%EB%A6%AC-1">http://darpangs.tistory.com/entry/WinDbg-명령어-정리-1</a></p>
<p><span id="more-364"></span></p>
<table border="0" cellpadding="0" cellspacing="0" width="786"><tbody><tr><td height="22" style="text-align: left;" width="72">ommand</td>
<td style="text-align: left;" width="188">option</td>
<td style="text-align: left;" width="97">usage</td>
<td style="text-align: left;" width="429">Desc</td>
</tr><tr><td class="xl69" height="22">종료</td>
<td class="xl69"></td>
<td class="xl69"></td>
<td class="xl69"></td>
</tr><tr><td class="xl66" height="22">q</td>
<td class="xl66"></td>
<td class="xl66"></td>
<td class="xl66">디버깅 종료</td>
</tr><tr><td class="xl66" height="22">qd</td>
<td class="xl66"></td>
<td class="xl66"></td>
<td class="xl66">디버깅 종료;연결해제</td>
</tr><tr><td class="xl68" height="22">디버깅 환경정보</td>
<td class="xl65"></td>
<td class="xl65"></td>
<td class="xl65"></td>
</tr><tr><td class="xl66" height="22">vertarget</td>
<td class="xl66"></td>
<td class="xl66"></td>
<td class="xl66">타겟 컴퓨터 정보 표시</td>
</tr><tr><td class="xl66" height="22">version</td>
<td class="xl66"></td>
<td class="xl66"></td>
<td class="xl66">디버그 환경 정보 표시</td>
</tr><tr><td class="xl66" height="22">.lastevent</td>
<td class="xl66"></td>
<td class="xl66"></td>
<td class="xl66">마지막 디버그 이벤트 정보 표시</td>
</tr><tr><td class="xl66" height="22">||</td>
<td class="xl66"></td>
<td class="xl66"></td>
<td class="xl66">디버깅 세션 정보 표시</td>
</tr><tr><td class="xl68" height="22">sumble &amp; sorurce</td>
<td class="xl65"></td>
<td class="xl65"></td>
<td class="xl65"></td>
</tr><tr><td class="xl66" height="22">.symfix</td>
<td class="xl66"></td>
<td class="xl66"></td>
<td class="xl66">MS 심볼경로 설정</td>
</tr><tr><td class="xl66" height="22">.sympath</td>
<td class="xl66"></td>
<td class="xl66"></td>
<td class="xl66">심볼경로 확인/설정</td>
</tr><tr><td class="xl66" height="22">.sym noisy</td>
<td class="xl66"></td>
<td class="xl66"></td>
<td class="xl66">심볼파일 검색 과정을 출력</td>
</tr><tr><td class="xl66" height="22">.srcpath</td>
<td class="xl66"></td>
<td class="xl66"></td>
<td class="xl66">소스경로 설정</td>
</tr><tr><td class="xl66" height="22">.srcnoisy</td>
<td class="xl66"></td>
<td class="xl66">.srcnoisy 1</td>
<td class="xl66">소스경로 검색 과정을 출력</td>
</tr><tr><td class="xl68" height="22">모듈</td>
<td class="xl65"></td>
<td class="xl65"></td>
<td class="xl65"></td>
</tr><tr><td class="xl66" height="22">lm</td>
<td class="xl66"></td>
<td class="xl66">l</td>
<td class="xl66">로드된 모듈만 표시</td>
</tr><tr><td class="xl66" height="22"></td>
<td class="xl66"></td>
<td class="xl66">m [pattern]</td>
<td class="xl66">패턴과 일치되는 모듈만 표시</td>
</tr><tr><td class="xl66" height="22"></td>
<td class="xl66"></td>
<td class="xl66">v</td>
<td class="xl66">모듈 상세정보 표시</td>
</tr><tr><td class="xl66" height="22">!lmi</td>
<td class="xl66">!lmi ntdll.dll</td>
<td class="xl66"></td>
<td class="xl66">모듈 상세정보 표시</td>
</tr><tr><td class="xl66" height="22">.reload</td>
<td class="xl66"></td>
<td class="xl66">/f [m_name]</td>
<td class="xl66">심볼을 즉시 로드</td>
</tr><tr><td class="xl66" height="22">x</td>
<td class="xl66">X ntdll!*</td>
<td class="xl66">/v</td>
<td class="xl66">심볼 타입을 표시.</td>
</tr><tr><td class="xl66" height="22"></td>
<td class="xl66">X *!*abc*</td>
<td class="xl66">/t</td>
<td class="xl66">데이터 타입을 표시</td>
</tr><tr><td class="xl66" height="22"></td>
<td class="xl66"></td>
<td class="xl66">/n</td>
<td class="xl66">이름순으로 정렬</td>
</tr><tr><td class="xl66" height="22">ln</td>
<td class="xl66"></td>
<td class="xl66">ln [address]</td>
<td class="xl66">해당 주소에 근접한 심볼의 정보 표시</td>
</tr><tr><td class="xl66" height="22">레지스터</td>
<td class="xl66"></td>
<td class="xl66"></td>
<td class="xl66"></td>
</tr><tr><td class="xl66" height="22">r</td>
<td class="xl66"></td>
<td class="xl66"></td>
<td class="xl66">레지스터 정보 표시</td>
</tr><tr><td class="xl66" height="22">r $proc</td>
<td class="xl66"></td>
<td class="xl66"></td>
<td class="xl66">현재 프로세스의 PEB주소( user-mode)</td>
</tr><tr><td class="xl66" height="22"></td>
<td class="xl66"></td>
<td class="xl66"></td>
<td class="xl66">현재 프로세스의 EPROcESS주소( kernel-mode)</td>
</tr><tr><td class="xl66" height="22">r $thread</td>
<td class="xl66"></td>
<td class="xl66"></td>
<td class="xl66">현재 스레드의 TEB주소( user-mode)</td>
</tr><tr><td class="xl66" height="22"></td>
<td class="xl66"></td>
<td class="xl66"></td>
<td class="xl66">현재 스레드의 ETHREAD주소( kernel-mode)</td>
</tr><tr><td class="xl66" height="22">r $tpid</td>
<td class="xl66"></td>
<td class="xl66"></td>
<td class="xl66">현재 프로세스 ID(PID)</td>
</tr><tr><td class="xl66" height="22">r $tid</td>
<td class="xl66"></td>
<td class="xl66"></td>
<td class="xl66">현재 스레드 ID(TID)</td>
</tr><tr><td class="xl66" height="22">언어셈블</td>
<td class="xl66"></td>
<td class="xl66"></td>
<td class="xl66"></td>
</tr><tr><td class="xl66" height="22">u</td>
<td class="xl66"></td>
<td class="xl66"></td>
<td class="xl66">언어셈블</td>
</tr><tr><td class="xl66" height="22"></td>
<td class="xl66"></td>
<td class="xl66">f</td>
<td class="xl66">언어셈블(함수전체)</td>
</tr><tr><td class="xl66" height="22"></td>
<td class="xl66"></td>
<td class="xl66">b</td>
<td class="xl66">언어셈블(ip이전의 8개 명령어)</td>
</tr><tr><td class="xl68" height="22">콜스택</td>
<td class="xl65"></td>
<td class="xl65"></td>
<td class="xl65"></td>
</tr><tr><td class="xl66" height="22">k</td>
<td class="xl66"></td>
<td class="xl66">[n]</td>
<td class="xl66">콜스택 정보표시</td>
</tr><tr><td class="xl66" height="22"></td>
<td class="xl66"></td>
<td class="xl66">p</td>
<td class="xl66">함수정보 출력</td>
</tr><tr><td class="xl66" height="22"></td>
<td class="xl66"></td>
<td class="xl66">b</td>
<td class="xl66">인자표시</td>
</tr><tr><td class="xl66" height="22"></td>
<td class="xl66"></td>
<td class="xl66">n</td>
<td class="xl66">프레임번호</td>
</tr><tr><td class="xl66" height="22"></td>
<td class="xl66"></td>
<td class="xl66">v</td>
<td class="xl66">FPO정보 표시</td>
</tr><tr><td class="xl66" height="22"></td>
<td class="xl66"></td>
<td class="xl66">f</td>
<td class="xl66">스택 사용량 표시</td>
</tr><tr><td class="xl66" height="22">break point</td>
<td class="xl66"></td>
<td class="xl66"></td>
<td class="xl66"></td>
</tr><tr><td class="xl66" height="22">bp</td>
<td class="xl66">bp 0x123456</td>
<td class="xl66"></td>
<td class="xl66">bp 설정</td>
</tr><tr><td class="xl66" height="22">bl</td>
<td class="xl66"></td>
<td class="xl66"></td>
<td class="xl66">bp 리스트 출력</td>
</tr><tr><td class="xl66" height="22">bc</td>
<td class="xl66">bc * | [frame_no]</td>
<td class="xl66"></td>
<td class="xl66">bp 삭제</td>
</tr><tr><td class="xl66" height="22">bd,be</td>
<td class="xl66">bc * | [frame_no]</td>
<td class="xl66"></td>
<td class="xl66">bp disable/enable</td>
</tr><tr><td class="xl66" height="22">bm</td>
<td class="xl66">bm notepad!*Win*</td>
<td class="xl66"></td>
<td class="xl66">패턴과 일치하는 모든심볼에 bp설정</td>
</tr><tr><td class="xl66" height="22">bu</td>
<td class="xl66">bu aaa!bbb</td>
<td class="xl66"></td>
<td class="xl66">로드되지 않은 심볼에 대한 bp설정</td>
</tr><tr><td class="xl66" height="22">ba</td>
<td class="xl66"></td>
<td class="xl66"></td>
<td class="xl66">특정 주소에 access시 bp</td>
</tr><tr><td class="xl68" height="22">지역변수</td>
<td class="xl65"></td>
<td class="xl65"></td>
<td class="xl65"></td>
</tr><tr><td class="xl66" height="22">dv</td>
<td class="xl66">dv modulr!test*</td>
<td class="xl66"></td>
<td class="xl66"></td>
</tr><tr><td class="xl66" height="22"></td>
<td class="xl66"></td>
<td class="xl66">/i</td>
<td class="xl66">심볼유형과 인자유형 표시</td>
</tr><tr><td class="xl66" height="22"></td>
<td class="xl66"></td>
<td class="xl66">/V</td>
<td class="xl66">변수저장 위치 표시( register or address )</td>
</tr><tr><td class="xl67" height="22">데이터유형</td>
<td class="xl65"></td>
<td class="xl65"></td>
<td class="xl65"></td>
</tr><tr><td class="xl66" height="22">dt</td>
<td class="xl66">df _EPROCESS 0xaddr</td>
<td class="xl66"></td>
<td class="xl66">주소를 특정 데이터 형으로 변환해서 표시</td>
</tr><tr><td class="xl66" height="22">du</td>
<td class="xl66"></td>
<td class="xl66"></td>
<td class="xl66">Unicode string 표시</td>
</tr><tr><td class="xl66" height="22">da</td>
<td class="xl66"></td>
<td class="xl66"></td>
<td class="xl66">Ansi string 표시</td>
</tr><tr><td class="xl66" height="22">dc</td>
<td class="xl66"></td>
<td class="xl66"></td>
<td class="xl66"></td>
</tr><tr><td class="xl66" height="22">db</td>
<td class="xl66"></td>
<td class="xl66"></td>
<td class="xl66"></td>
</tr><tr><td class="xl66" height="22">dy</td>
<td class="xl66"></td>
<td class="xl66"></td>
<td class="xl66"></td>
</tr><tr><td class="xl66" height="22"></td>
<td class="xl66"></td>
<td class="xl66"></td>
<td class="xl66"></td>
</tr><tr><td class="xl66" height="22">!address</td>
<td class="xl66">!address</td>
<td class="xl66"></td>
<td class="xl66"></td>
</tr><tr><td class="xl66" height="22"></td>
<td class="xl66">!address [address]</td>
<td class="xl66"></td>
<td class="xl66"></td>
</tr><tr><td class="xl67" height="22">프로세스 &amp; 스레드 정보</td>
<td class="xl65"></td>
<td class="xl65"></td>
<td class="xl65"></td>
</tr><tr><td class="xl66" height="22">!peb</td>
<td class="xl66"></td>
<td class="xl66"></td>
<td class="xl66">PEB(Process Environment Block)표시</td>
</tr><tr><td class="xl66" height="22">!teb</td>
<td class="xl66"></td>
<td class="xl66"></td>
<td class="xl66">TEB(Thread Environment Block) 표시</td>
</tr><tr><td class="xl66" height="22"></td>
<td class="xl66"></td>
<td class="xl66"></td>
<td class="xl66"></td>
</tr><tr><td class="xl66" height="22">!gle</td>
<td class="xl66"></td>
<td class="xl66"></td>
<td class="xl66">API의 마지막 에러코드 표시</td>
</tr><tr><td class="xl68" height="22">실행 제어</td>
<td class="xl65"></td>
<td class="xl65"></td>
<td class="xl65"></td>
</tr><tr><td class="xl66" height="22">t</td>
<td class="xl66"></td>
<td class="xl66"></td>
<td class="xl66">Trace</td>
</tr><tr><td class="xl66" height="22">~.t</td>
<td class="xl66"></td>
<td class="xl66"></td>
<td class="xl66">다른 스레드를 중지시킨 상태에서 하나의 statementt실행</td>
</tr><tr><td class="xl66" height="22">g</td>
<td class="xl66"></td>
<td class="xl66"></td>
<td class="xl66"></td>
</tr><tr><td class="xl66" height="22">p</td>
<td class="xl66"></td>
<td class="xl66"></td>
<td class="xl66">Step Over</td>
</tr><tr><td class="xl66" height="22">gu</td>
<td class="xl66">gu</td>
<td class="xl66"></td>
<td class="xl66">현재함수가 복귀할 때 까지 실행</td>
</tr><tr><td class="xl66" height="22"></td>
<td class="xl66">~0 gu</td>
<td class="xl66"></td>
<td class="xl66">스레드 0을 제외한 모든 스레드를 freeze함</td>
</tr><tr><td class="xl66" height="22">wt</td>
<td class="xl66"></td>
<td class="xl66"></td>
<td class="xl66">내부에서 호출된 함수와 함수호출 횟수등의 정보 표시</td>
</tr><tr><td class="xl66" height="22">.cxr</td>
<td class="xl66"></td>
<td class="xl66"></td>
<td class="xl66">컨텍스트 변경</td>
</tr><tr><td class="xl66" height="22">!ready</td>
<td class="xl66"></td>
<td class="xl66"></td>
<td class="xl66"></td>
</tr><tr><td class="xl66" height="22">.thread</td>
<td class="xl66"></td>
<td class="xl66"></td>
<td class="xl66"></td>
</tr><tr><td class="xl66" height="22">!thread</td>
<td class="xl66"></td>
<td class="xl66"></td>
<td class="xl66"></td>
</tr><tr><td class="xl66" height="22">.trap</td>
<td class="xl66"></td>
<td class="xl66"></td>
<td class="xl66"></td>
</tr><tr><td class="xl66" height="22">.process</td>
<td class="xl66"></td>
<td class="xl66"></td>
<td class="xl66"></td>
</tr><tr><td class="xl66" height="22">!process</td>
<td class="xl66"></td>
<td class="xl66"></td>
<td class="xl66"></td>
</tr><tr><td class="xl66" height="22">ed</td>
<td class="xl66"></td>
<td class="xl66"></td>
<td class="xl66"></td>
</tr><tr><td class="xl66" height="22">eb</td>
<td class="xl66">eb .-6 90 90 90 90 90 90</td>
<td class="xl66"></td>
<td class="xl66">6byte를 NOP(0x90)으로 변경</td>
</tr><tr><td class="xl66" height="22">!error</td>
<td class="xl66">!error [error code]</td>
<td class="xl66"></td>
<td class="xl66">에러코드 정보표시</td>
</tr></tbody></table><p>출처: <a href="http://jangpd007.tistory.com/203">http://jangpd007.tistory.com/203</a> [참 놀라운 세상]</p>
<nav class="pagination group"></nav></div>
<div class="clear"></div>
</div>
</div>
</article>
```
