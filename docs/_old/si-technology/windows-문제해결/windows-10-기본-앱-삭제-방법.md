---
title: "Windows 10 기본 앱 삭제 방법"
date: "No Date"
---

Windows 10 기본 앱 삭제 방법
=====================

by 
[박경원](https://appi77.github.io/my-tips/author/appi77/ "박경원이(가) 작성한 글")
·
Published 2018년 11월 30일
· Updated 2018년 11월 30일

Powershell.exe 실행 후 하당 목록에서 삭제할 프로그램 제거 하시면 됩니다.

(ex. Get-AppxPackage \*3dbuilder\* | Remove-AppxPackage )

3D Builder(3D빌더)  
Get-AppxPackage \*3dbuilder\* | Remove-AppxPackage

Alarms and Clock(알람 앤 클락)  
Get-AppxPackage \*windowsalarms\* | Remove-AppxPackage

Calculator(계산기)  
Get-AppxPackage \*windowscalculator\* | Remove-AppxPackage

Calendar and Mail(캘린더 앤 메일)  
Get-AppxPackage \*windowscommunicationsapps\* | Remove-AppxPackage

Camera(카메라)  
Get-AppxPackage \*windowscamera\* | Remove-AppxPackage

Get Office(오피스)  
Get-AppxPackage \*officehub\* | Remove-AppxPackage

Get Skype(스카이프)  
Get-AppxPackage \*skypeapp\* | Remove-AppxPackage

Get Started  
Get-AppxPackage \*getstarted\* | Remove-AppxPackage

Groove Music(그루브 뮤직)  
Get-AppxPackage \*zunemusic\* | Remove-AppxPackage

Maps(맵스 지도 어플)  
Get-AppxPackage \*windowsmaps\* | Remove-AppxPackage

Microsoft Solitaire Collection  
Get-AppxPackage \*solitairecollection\* | Remove-AppxPackage

Money(머니)  
Get-AppxPackage \*bingfinance\* | Remove-AppxPackage

Movies & TV(무비 앤 티비)  
Get-AppxPackage \*zunevideo\* | Remove-AppxPackage

News(뉴스)  
Get-AppxPackage \*bingnews\* | Remove-AppxPackage

OneNote(원노트)  
Get-AppxPackage \*onenote\* | Remove-AppxPackage

People(피플)  
Get-AppxPackage \*people\* | Remove-AppxPackage

Phone Companion(폰 컴패니언)  
Get-AppxPackage \*windowsphone\* | Remove-AppxPackage

Photos(포토 사진 관리 앱)  
Get-AppxPackage \*photos\* | Remove-AppxPackage

Store(윈도우 앱스토어)  
Get-AppxPackage \*windowsstore\* | Remove-AppxPackage

Sports(스포츠)  
Get-AppxPackage \*bingsports\* | Remove-AppxPackage

Voice Recorder(보이스 레코더)  
Get-AppxPackage \*soundrecorder\* | Remove-AppxPackage

Weather(웨더. 날씨 어플)  
Get-AppxPackage \*bingweather\* | Remove-AppxPackage

Xbox(엑스박스)  
Get-AppxPackage \*xboxapp\* | Remove-AppxPackage

만약 지운것 중에 다시 깔고싶은것들은 윈도우 어플 스토어에서 찾을 수 있는것은 찾으시고.  
한번에 모두 되돌리고 싶다 하시는 분은 아래의 명령어를 입력하시면 됩니다.

Get-AppxPackage -AllUsers| Foreach {Add-AppxPackage -DisableDevelopmentMode -Register “$($\_.InstallLocation)\AppXManifest.xml”}  
\* 첨부파일 다운로드 후 해당 파일을 마우스 우클릭하여 [Powershell에서 실행] 클릭

```html
<article class="post-481 post type-post status-publish format-standard hentry category-windows-"><div class="post-inner group">
<h1 class="post-title entry-title">Windows 10 기본 앱 삭제 방법</h1>
<p class="post-byline">
   by   <span class="vcard author">
<span class="fn"><a href="https://appi77.github.io/my-tips/author/appi77/" rel="author" title="박경원이(가) 작성한 글">박경원</a></span>
</span>
   ·
                                Published <time class="published" datetime="2018년 11월 30일">2018년 11월 30일</time>
              · Updated <time class="updated" datetime="2018년 11월 30일">2018년 11월 30일</time></p>
<div class="clear"></div>
<div class="entry themeform">
<div class="entry-inner">
<p>Powershell.exe 실행 후 하당 목록에서 삭제할 프로그램 제거 하시면 됩니다.</p>
<p>(ex. Get-AppxPackage *3dbuilder* | Remove-AppxPackage )</p>
<p>3D Builder(3D빌더)<br/>
Get-AppxPackage *3dbuilder* | Remove-AppxPackage</p>
<p>Alarms and Clock(알람 앤 클락)<br/>
Get-AppxPackage *windowsalarms* | Remove-AppxPackage</p>
<p>Calculator(계산기)<br/>
Get-AppxPackage *windowscalculator* | Remove-AppxPackage</p>
<p>Calendar and Mail(캘린더 앤 메일)<br/>
Get-AppxPackage *windowscommunicationsapps* | Remove-AppxPackage</p>
<p>Camera(카메라)<br/>
Get-AppxPackage *windowscamera* | Remove-AppxPackage</p>
<p>Get Office(오피스)<br/>
Get-AppxPackage *officehub* | Remove-AppxPackage</p>
<p>Get Skype(스카이프)<br/>
Get-AppxPackage *skypeapp* | Remove-AppxPackage</p>
<p>Get Started<br/>
Get-AppxPackage *getstarted* | Remove-AppxPackage</p>
<p>Groove Music(그루브 뮤직)<br/>
Get-AppxPackage *zunemusic* | Remove-AppxPackage</p>
<p>Maps(맵스 지도 어플)<br/>
Get-AppxPackage *windowsmaps* | Remove-AppxPackage</p>
<p>Microsoft Solitaire Collection<br/>
Get-AppxPackage *solitairecollection* | Remove-AppxPackage</p>
<p>Money(머니)<br/>
Get-AppxPackage *bingfinance* | Remove-AppxPackage</p>
<p>Movies &amp; TV(무비 앤 티비)<br/>
Get-AppxPackage *zunevideo* | Remove-AppxPackage</p>
<p>News(뉴스)<br/>
Get-AppxPackage *bingnews* | Remove-AppxPackage</p>
<p>OneNote(원노트)<br/>
Get-AppxPackage *onenote* | Remove-AppxPackage</p>
<p>People(피플)<br/>
Get-AppxPackage *people* | Remove-AppxPackage</p>
<p>Phone Companion(폰 컴패니언)<br/>
Get-AppxPackage *windowsphone* | Remove-AppxPackage</p>
<p>Photos(포토 사진 관리 앱)<br/>
Get-AppxPackage *photos* | Remove-AppxPackage</p>
<p>Store(윈도우 앱스토어)<br/>
Get-AppxPackage *windowsstore* | Remove-AppxPackage</p>
<p>Sports(스포츠)<br/>
Get-AppxPackage *bingsports* | Remove-AppxPackage</p>
<p>Voice Recorder(보이스 레코더)<br/>
Get-AppxPackage *soundrecorder* | Remove-AppxPackage</p>
<p>Weather(웨더. 날씨 어플)<br/>
Get-AppxPackage *bingweather* | Remove-AppxPackage</p>
<p>Xbox(엑스박스)<br/>
Get-AppxPackage *xboxapp* | Remove-AppxPackage</p>
<p>만약 지운것 중에 다시 깔고싶은것들은 윈도우 어플 스토어에서 찾을 수 있는것은 찾으시고.<br/>
한번에 모두 되돌리고 싶다 하시는 분은 아래의 명령어를 입력하시면 됩니다.</p>
<p>Get-AppxPackage -AllUsers| Foreach {Add-AppxPackage -DisableDevelopmentMode -Register “$($_.InstallLocation)\AppXManifest.xml”}<br/>
* 첨부파일 다운로드 후 해당 파일을 마우스 우클릭하여 [Powershell에서 실행] 클릭</p>
<nav class="pagination group"></nav></div>
<div class="clear"></div>
</div>
</div>
</article>
```
