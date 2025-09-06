---
title: "Linux 에 Content Server 설치 환경설정"
date: "No Date"
---

Linux 에 Content Server 설치 환경설정
==============================

by 
[박경원](https://appi77.github.io/my-tips/author/appi77/ "박경원이(가) 작성한 글")
·
Published 2016년 7월 1일
· Updated 2016년 7월 1일

/usr/sbin/groupadd docs  
/usr/sbin/useradd -m -g docs dmadmin  
passwd dmadmin

mkdir -p /opt/documentum  
mkdir -p /opt/dctm\_client  
mkdir -p /data/dmdata  
chown -R dmadmin:docs /opt/documentum /data/dmdata /opt/dctm\_client  
chmod -R 775 /opt/documentum /data/dmdata /opt/dctm\_client

.bash\_profile

export ORACLE\_HOME=/opt/ora/oracle/product/10.2.0/db\_1  
export TNS\_ADMIN=$ORACLE\_HOME/network/admin  
export DOCUMENTUM=/opt/documentum  
export DM\_HOME=$DOCUMENTUM/product/6.0  
export DOCUMENTUM\_SHARED=/opt/dctm\_client

export LANG=ko\_KR.eucKR

DHCP로 아이피 가져온것 host파일에 적용하기  
vi /usr/local/bin/hosts.sh

#!/bin/bash

ifconfig | grep inet\ addr | grep -v ‘127.0.0.1’ |awk -F ‘ +||:+’ ‘{print $4}’ > /tmp/ethx-addresses  
gethostname=`hostname|awk -F’.’ ‘{print $1}’`  
grep $gethostname /etc/hosts | grep -v ‘127.0.0.1’ | grep -v “#”| awk -F’ +’ ‘{print $1}’>/tmp/myhost-addresses  
lineas=`wc -l /tmp/ethx-addresses| cut -d’ ‘ -f1`  
lineasetmyhosts=`wc -l /tmp/myhost-addresses| cut -d’ ‘ -f1`  
for i in `seq 1 $lineas` ;do  
ip=`head -n $i /tmp/ethx-addresses | tail -1`  
if [ $i -le $lineasetmyhosts ]; then  
ipetcmyhost=`head -n $i /tmp/myhost-addresses | awk ‘{print $1}’`  
cat /etc/hosts | sed “s/$ipetcmyhost/$ip/g” > /tmp/chhosts ; cat /tmp/chhosts > /etc/hosts  
else  
ip=`head -n $i /tmp/ethx-addresses | tail -1`  
echo “$ip $gethostname” >> /etc/hosts

fi  
done

/etc/sysconfig/network-scripts/ifup  
if [ -n “${DYNCONFIG}” ]; then  
.  
.  
.  
.  
/usr/local/bin/hosts.sh

# end dynamic device configuration  
else

```html
<article class="post-100 post type-post status-publish format-standard hentry category-install"><div class="post-inner group">
<h1 class="post-title entry-title">Linux 에 Content Server 설치 환경설정</h1>
<p class="post-byline">
   by   <span class="vcard author">
<span class="fn"><a href="https://appi77.github.io/my-tips/author/appi77/" rel="author" title="박경원이(가) 작성한 글">박경원</a></span>
</span>
   ·
                                Published <time class="published" datetime="2016년 7월 1일">2016년 7월 1일</time>
              · Updated <time class="updated" datetime="2016년 7월 1일">2016년 7월 1일</time></p>
<div class="clear"></div>
<div class="entry themeform">
<div class="entry-inner">
<p>/usr/sbin/groupadd docs<br/>
/usr/sbin/useradd -m -g docs dmadmin<br/>
passwd dmadmin</p>
<p>mkdir -p /opt/documentum<br/>
mkdir -p /opt/dctm_client<br/>
mkdir -p /data/dmdata<br/>
chown -R dmadmin:docs /opt/documentum /data/dmdata /opt/dctm_client<br/>
chmod -R 775 /opt/documentum /data/dmdata /opt/dctm_client</p>
<p>.bash_profile</p>
<p>export ORACLE_HOME=/opt/ora/oracle/product/10.2.0/db_1<br/>
export TNS_ADMIN=$ORACLE_HOME/network/admin<br/>
export DOCUMENTUM=/opt/documentum<br/>
export DM_HOME=$DOCUMENTUM/product/6.0<br/>
export DOCUMENTUM_SHARED=/opt/dctm_client</p>
<p>export LANG=ko_KR.eucKR</p>
<p>DHCP로 아이피 가져온것 host파일에 적용하기<br/>
vi /usr/local/bin/hosts.sh</p>
<p>#!/bin/bash</p>
<p>ifconfig | grep inet\ addr | grep -v ‘127.0.0.1’ |awk -F ‘ +||:+’ ‘{print $4}’ &gt; /tmp/ethx-addresses<br/>
gethostname=`hostname|awk -F’.’ ‘{print $1}’`<br/>
grep $gethostname /etc/hosts | grep -v ‘127.0.0.1’  | grep -v “#”| awk -F’ +’ ‘{print $1}’&gt;/tmp/myhost-addresses<br/>
lineas=`wc -l /tmp/ethx-addresses| cut -d’ ‘ -f1`<br/>
lineasetmyhosts=`wc -l /tmp/myhost-addresses| cut -d’ ‘ -f1`<br/>
for i in `seq 1 $lineas` ;do<br/>
    ip=`head -n $i /tmp/ethx-addresses | tail -1`<br/>
    if [ $i -le $lineasetmyhosts ]; then<br/>
       ipetcmyhost=`head -n $i /tmp/myhost-addresses | awk ‘{print $1}’`<br/>
        cat  /etc/hosts | sed “s/$ipetcmyhost/$ip/g” &gt; /tmp/chhosts ; cat /tmp/chhosts &gt; /etc/hosts<br/>
    else<br/>
        ip=`head -n $i /tmp/ethx-addresses | tail -1`<br/>
        echo “$ip       $gethostname” &gt;&gt; /etc/hosts</p>
<p>    fi<br/>
done</p>
<p>/etc/sysconfig/network-scripts/ifup<br/>
if [ -n “${DYNCONFIG}” ]; then<br/>
	.<br/>
	.<br/>
	.<br/>
	.<br/>
 /usr/local/bin/hosts.sh</p>
<p># end dynamic device configuration<br/>
else</p>
<nav class="pagination group"></nav></div>
<div class="clear"></div>
</div>
</div>
</article>
```
