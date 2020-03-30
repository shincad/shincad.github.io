---
layout: post
title:  "raspberry pi samba 설정"
date:   2020-03-30
comments: true
categories: companywork
---

* samba 설치

* sudo apt-get install samba samba-common

* 공유폴더생성

  * mkdir /download

* /etc/samba/smb.conf 수정

  * global 아래 wins support = yes

* smb.conf 아래부분에 다음 줄 추가

  ```
  [raspberrypi]
  path=/download
  browseable=Yes
  writeable=Yes
  only guest=no
  guest ok = no
  create mask=0777
  directory mask=0777
  public=no
  ```

* sudo smbpasswd -a pi

  * samba 계정 및 패스워드생성

* service smbd restart

