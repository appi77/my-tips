---
title: "No Title"
date: "2019-10-14"
---

[Linux](https://appi77.github.io/my-tips/category/si-technology/linux/)

2019년 10월 14일

 by 
[박경원](https://appi77.github.io/my-tips/author/appi77/ "박경원이(가) 작성한 글")
 · Published 2019년 10월 14일
· Last modified 2019년 10월 15일

[Samba4 Active Directory 설치](https://appi77.github.io/my-tips/si-technology/linux/samba4-active-directory-%ec%84%a4%ec%b9%98/ "Permalink to Samba4 Active Directory 설치")
------------------------------------------------------------------------------------------------------------------------------------------------------------------------

[참고] https://www.tecmint.com/install-samba4-active-directory-ubuntu/ https://helia.ee/koolitus/linuxi-materjalid/debian/create-active-directory-infrastructure-samba4-ubuntu/ 설정 후 DNS를 자동 업데이트 하기 위해서는 vi /etc/samba/smb.conf nsupdate command = nsupdate allow dns updates = nonsecure 추가해야 함 sudo systemctl restart samba-ad-dc.service samba\_dnsupdate –verbose –all-names 오류가 없어야 함 수정...

```html
<article class="group grid-item post-1554 post type-post status-publish format-standard hentry category-linux" id="post-1554"><div class="post-inner post-hover">
<div class="post-thumbnail">
<a href="https://appi77.github.io/my-tips/si-technology/linux/samba4-active-directory-%ec%84%a4%ec%b9%98/">
</a>
</div>
<div class="post-meta group">
<p class="post-category"><a href="https://appi77.github.io/my-tips/category/si-technology/linux/" rel="category tag">Linux</a></p>
<p class="post-date">
<time class="published updated" datetime="2019-10-14 11:43:18">2019년 10월 14일</time></p>
<p class="post-byline" style="display:none"> by    <span class="vcard author">
<span class="fn"><a href="https://appi77.github.io/my-tips/author/appi77/" rel="author" title="박경원이(가) 작성한 글">박경원</a></span>
</span> · Published <span class="published">2019년 10월 14일</span>
     · Last modified <span class="updated">2019년 10월 15일</span> </p>
</div>
<h2 class="post-title entry-title">
<a href="https://appi77.github.io/my-tips/si-technology/linux/samba4-active-directory-%ec%84%a4%ec%b9%98/" rel="bookmark" title="Permalink to Samba4 Active Directory 설치">Samba4 Active Directory 설치</a>
</h2>
<div class="entry excerpt entry-summary">
<p>[참고] https://www.tecmint.com/install-samba4-active-directory-ubuntu/ https://helia.ee/koolitus/linuxi-materjalid/debian/create-active-directory-infrastructure-samba4-ubuntu/ 설정 후 DNS를 자동 업데이트 하기 위해서는 vi /etc/samba/smb.conf nsupdate command = nsupdate allow dns updates = nonsecure 추가해야 함 sudo systemctl restart samba-ad-dc.service samba_dnsupdate –verbose –all-names 오류가 없어야 함 수정...</p>
</div>
</div>
</article>
```
