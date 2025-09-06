---
title: "폐쇄망 속도"
date: "No Date"
---

폐쇄망 속도
======

by 
[박경원](https://appi77.github.io/my-tips/author/appi77/ "박경원이(가) 작성한 글")
·
Published 2017년 1월 13일
· Updated 2018년 10월 25일

Microsoft 루트 인증서 프로그램에서 인증서를 자동으로 업데이트 확인 취소  
reg add HKLM\Software\Policies\Microsoft\SystemCertificates\AuthRoot /v DisableRootAutoUpdate /t REG\_DWORD /d 1 /f

서버의 인증서 해지 확인  
reg add HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Internet Settings /v CertificateRevocation /t REG\_DWORD /d 0 /f

다운로드한 프로그램의 해지 확인  
reg add “HKCU\Software\Microsoft\Internet Explorer\Download” /v CheckExeSignatures /t REG\_SZ /d no /f

▣ 인터넷차단된 환경입니다.  
IE를 이용하여 내부사이트 접속시 접속지연 현상이 나타날 수 있습니다.  
이는 IE 자체적으로 접속하려는 사이트에서 제공하는 ActiveX 등의 Singing 과정과  
인증서 체인검증 등의 행위를 내부적으로 시도하고 있고  
이 시도하는 과정이 인터넷을 통해 하려다 보니 타임아웃 시간동안 IE가 대기하고 있기 때문입니다.  
이를 다소 해결할 수 있는 방법입니다.

IE에서 체인검증시 아래와 같은 URL로 접근 하면서 대기함  
http://ctldl.windowsupdate.com/msdownload/update/v3/static/trustedr/en/authrootstl.cab?랜덤값

Windows 7 만 해당됨  
시작 > 제어판 > 관리도구 > 로컬보안정책 > 공개키정책 > 인증서 경로 유효성 검사 설정 속성 > 네트워크 검색 탭 >  
이 정책 설정 정의 선택 > Microsoft 루트 인증서 프로그램에서 인증서 자동 업데이트 항목 해제 > 적용

▣ 인터넷차단환경입니다.  
IE이용시 http://urs.microsoft.com:443 접속되면서 속도지연이 발생합니다.  
이는 스마트필터기능을 해제하시면 됩니다.

대상 브라우저: Internet Explorer 8,9

F10 메뉴호출 > 도구 > SmartScreen필터 > SmartScreen 필터 켜기 선택 후  
SmartScreen 필터 해제

```html
<article class="post-229 post type-post status-publish format-standard hentry category-si-technology category-23"><div class="post-inner group">
<h1 class="post-title entry-title">폐쇄망 속도</h1>
<p class="post-byline">
   by   <span class="vcard author">
<span class="fn"><a href="https://appi77.github.io/my-tips/author/appi77/" rel="author" title="박경원이(가) 작성한 글">박경원</a></span>
</span>
   ·
                                Published <time class="published" datetime="2017년 1월 13일">2017년 1월 13일</time>
              · Updated <time class="updated" datetime="2018년 10월 25일">2018년 10월 25일</time></p>
<div class="clear"></div>
<div class="entry themeform">
<div class="entry-inner">
<p>Microsoft 루트 인증서 프로그램에서 인증서를 자동으로 업데이트 확인 취소<br/>
reg add HKLM\Software\Policies\Microsoft\SystemCertificates\AuthRoot /v DisableRootAutoUpdate /t REG_DWORD /d 1 /f</p>
<p>서버의 인증서 해지 확인<br/>
reg add HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Internet Settings /v CertificateRevocation /t REG_DWORD /d 0 /f</p>
<p>다운로드한 프로그램의 해지 확인<br/>
reg add “HKCU\Software\Microsoft\Internet Explorer\Download” /v CheckExeSignatures /t REG_SZ /d no /f</p>
<p>▣ 인터넷차단된 환경입니다.<br/>
IE를 이용하여 내부사이트 접속시 접속지연 현상이 나타날 수 있습니다.<br/>
이는 IE 자체적으로 접속하려는 사이트에서 제공하는 ActiveX 등의 Singing 과정과<br/>
인증서 체인검증 등의 행위를 내부적으로 시도하고 있고<br/>
이 시도하는 과정이 인터넷을 통해 하려다 보니 타임아웃 시간동안 IE가 대기하고 있기 때문입니다.<br/>
이를 다소 해결할 수 있는 방법입니다.</p>
<p>IE에서 체인검증시 아래와 같은 URL로 접근 하면서 대기함<br/>
http://ctldl.windowsupdate.com/msdownload/update/v3/static/trustedr/en/authrootstl.cab?랜덤값</p>
<p>Windows 7 만 해당됨<br/>
시작 &gt; 제어판 &gt; 관리도구 &gt; 로컬보안정책 &gt; 공개키정책 &gt; 인증서 경로 유효성 검사 설정 속성 &gt; 네트워크 검색 탭 &gt;<br/>
이 정책 설정 정의 선택 &gt; Microsoft 루트 인증서 프로그램에서 인증서 자동 업데이트 항목 해제 &gt; 적용</p>
<p>▣ 인터넷차단환경입니다.<br/>
IE이용시 http://urs.microsoft.com:443 접속되면서 속도지연이 발생합니다.<br/>
이는 스마트필터기능을 해제하시면 됩니다.</p>
<p>대상 브라우저: Internet Explorer 8,9</p>
<p>F10 메뉴호출 &gt; 도구 &gt; SmartScreen필터 &gt; SmartScreen 필터 켜기 선택 후<br/>
SmartScreen 필터 해제</p>
<nav class="pagination group"></nav></div>
<div class="clear"></div>
</div>
</div>
</article>
```
