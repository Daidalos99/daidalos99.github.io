---
layout: post
title: qt_installer_problem
description: >
  QT Online Installer 설치시 속도 느림 문제 해결
grouped: true

categories:
  - etc
tags:
  - qt creator
  - qt online installer
  - qt 설치
  - qt 설치 느림
  - qt 다운
 
date: 2023-03-07
last_modified_at: 2023-03-07
comments: true
published: true
sitemap :
  changefreq : daily
  priority : 1.0
---
QT Online Installer 설치시 속도 느림 문제 해결
---

캡스톤 설계 프로젝트를 위해 QT 6.4.2를 설치하고자 하였는데, offline installer가 따로 없고, online installer만 있었다. 그래서 Online Installer를 사용하려고 하니, 속도가 수 kb/s정도로 거의 수 시간이 소요되는 수준이었다.

이때 Mirror link를 사용하면 속도를 올릴 수 있다.  
미러 링크의 정확한 원리는 잘 모르겠으나, 아마도 멀리있는 QT 원 서버에서 다운을 받으면 오래 걸리니 접속을 원활하게 하고자 세계 각지에 이를 복사해둔 것 같다.
이 방법은 [QT Wiki](https://wiki.qt.io/Main)에 더 자세히 나오므로, 이를 참고해도 좋겠다.

1. 우선 관리자 권한으로 cmd를 실행한다.(그냥 cmd에서 하면 왠지 안될 것 같아 관리자 권한으로 실행함)  
![img01](/assets/img/etc/qt_installer_problem/administrator_cmd.png)

2. qt 설치용 exe파일이 있는 폴더의 경로로 들어간다. 이때, cd, dir 등의 명령어를 잘 모르겠다면, 그냥 파일 관리자로 들어가서 exe파일의 속성을 누른 후, 아래의 사진과 같이 경로를 복사하여 cmd에서 그 경로로 진입한다.
![img02](/assets/img/etc/qt_installer_problem/qt_config.png)

3. cmd에 '.\exe파일이름(확장자 포함) --mirror http://ftp.jaist.ac.jp/pub/qtproject/'을 추가해 준다.  
나의 경우, 파일의 이름이 'qt-unified-windows-x64-4.5.1-online.exe'이므로, '.\qt-unified-windows-x64-4.5.1-online.exe --mirror http://ftp.jaist.ac.jp/pub/qtproject/'를 입력해 준다.  
Mirror Url은 다양하게 있지만, 일본의 Jaist가 가장 빠르기 때문에 이 주소를 입력하였다.  
다른 국가들의 Mirror Url 주소는 [이곳](https://download.qt.io/static/mirrorlist/)에 나와있다.
![img03](/assets/img/etc/qt_installer_problem/cmd.png)

이렇게 하면, 이제 수 mb/s의 속도로 다운되는 것을 확인할 수 있을 것이다.