---
layout: post
title: qt6_opencv4_connect_1
description: >
  Qt6(6.4.2)와 OpenCV4(4.7.0) 연동하기 - 1
grouped: true

categories:
  - etc
tags:
  - qt opencv 연동
  - qt opencv
  - qt6 opencv 연동
  - qt6 opencv
  - qt creator opencv
  - qt 크리에이터 opencv
 
date: 2023-03-09
last_modified_at: 2023-03-09
comments: true
published: true
sitemap :
  changefreq : daily
  priority : 1.0
---
Qt6(6.4.2)와 OpenCV4(4.7.0) 연동하기 - 1
---

캡스톤 설계 프로젝트에서 사용할 gigE 카메라의 영상을 c++ 코드상에서 불러와 확인하기 위해 Qt와 OpenCV를 연동하고자 하였다. 구글 검색했을 때 나오는 여러 게시물들을 찾아봤으나, 왜인지 나에게는 다음과 같은 오류가 뜨면서 계속 make에 실패하였다.
![img1](/assets/img/etc/qt6_opencv4_connect_1/Error2.png)

32bit와 64bit의 아키텍쳐 충돌 문제 같은데, 구글링을 해도 이 오류는 뭔가 해결 방법이 애매하게 나와있고, 또 나와 맞지 않았다.

우선 이 오류가 떴을 때 내가 사용하고자 했던 환경들은 다음과 같다.  
- Windows: 11
- CMake: 3.26.0-rc5
- QV: 6.4.2(MinGW 11.2.0)
- OpenCV: 4.7.0

가만히 생각해 보니 Cmake 버전이 rc(released candidate)라서 불안정해서 이런 오류가 발생했을 수도 있다고 생각하였다. ~~(하지만 이것 때문이라고 확신은 못하겠다.)~~

그래서 Cmake의 버전을 **3.25.0**으로 바꾸고 다시 시작해 보았다.

우선 기본적으로 Qt와 OpenCV를 연동하는 방법은 Qt Wiki에 공식적으로 나와있다. [이 링크](https://wiki.qt.io/How_to_setup_Qt_and_openCV_on_Windows)에서는 Qt5.9와 OpenCV3.2.0을 연동하기 때문에, 내가 연동시킨 것과는 약간 방법이 다를 수 있으나, 전체적인 흐름은 동일하다.

다시 정리하면, 아래의 버전들을 사용할 것이다.
아래 버전들은 현재(3월 9일) 기준으로 cmake, qt, opencv 홈페이지에서 다운받을 수 있는 가장 최신 버전이다.
- Windows: 11
- CMake: 3.25.0-windows-x86_64.msi
- Qt: 6.4.2(MinGW 11.2.0)
- OpenCV: 4.7.0

OpenCV 설치 시 C:\에 바로 설치해주었고, binary를 빌드할 폴더로 C:\ 경로에 opencv-build라는 폴더를 만들어주었다.(Qt Wiki의 방법과 동일)

CMake를 하기전에 시스템 환경 변수에서 PATH를 더블 클릭하고, 아래와 같은 내용들을 추가해 준다.(경로는 개인별로 다를 수 있음)
> C:\MinGW\bin
> C:\MinGW\msys\1.0\bin
> C:\Program Files\CMake\bin

CMake를 실행하고 다음과 같이 경로를 넣어주었다.(개인마다 경로가 조금씩 다를 수 있다.)
> Where is the source code: C:\opencv\sources
  where to build the binaries: C:\opencv-build

Configure를 할 때, 아래와 같이 설정한다.
>Specify the generator for this project: MinGW Makefiles
 Specify native compilers, next
 Compilers C: C:\Qt\Tools\mingw1120_64\bin\gcc.exe
 Compilers C++: C:\Qt\Tools\mingw1120_64\bin\g++.exe
 Finish

이렇게 설정해주고 Configure를 완료하면, 아래와 같이 체크박스들이 막 생길 것이다.
![img2](/assets/img/etc/qt6_opencv4_connect_1/checkbox.png)

다음으로, search를 통해 
- WITH_QT: 체크
- WITH_OPENGL: 체크
- OPENCV_PYTHON3_VERSION: 체크
- ENABLE_PRECOMPILED_HEADERS: 혹시라도 체크되어 있다면 해제

해주었다. Configure를 한번 더 눌러준다.

이렇게 하면 QT6_DIR, QT5_DIR 등이 맨 위에 빨간색으로 뜰 것이다.
나의 경우에는 QT6를 사용하므로, 여기서 QT6_DIR에 다음 경로를 입력해 주었다.
> C:\Qt\6.4.2\mingw_64\lib\cmake\Qt6

Configure를 한번 더 해준다. 별 오류 없이 'Configuring Done'의 메세지를 본다면, Generate를 해준다. 이제, 아까 만들었던 opencv-build 폴더를 보면 Makefile이 생겨있는 것을 확인할 수 있다.

마지막으로, opencv-build 경로에서 cmd를 열어 다음의 명령어를 입력해준다.
> mingw32-make -j 8 (본인의 cpu core가 8개 이하라면 그에 맞게 바꿔주면 될 것이다. 이 작업은 길게는 15분 정도가 소요되었다.)
  mingw32-make install (1분도 안걸렸다.)

'mingw32-make -j 8'을 할때는 다음과 같이 중간중간에 경고메세지가 떴지만 그냥 무시하고 진행했다.
![img3](/assets/img/etc/qt6_opencv4_connect_1/49.png)

![img4](/assets/img/etc/qt6_opencv4_connect_1/64.png)

![img5](/assets/img/etc/qt6_opencv4_connect_1/91.png)

드디어 성공했다!!

'make install'은 별다른 경고 없이 금방 완료되었다.
![img6](/assets/img/etc/qt6_opencv4_connect_1/install.png)

![img7](/assets/img/etc/qt6_opencv4_connect_1/install_complete.png)

install이 끝나면 시스템 변수의 PATH에 'C:\opencv-build\x64\mingw\bin'을 추가해준다.
(경로는 개인별로 다를 수 있음)

이후에 Qt Creator를 통해 설치된 OpenCV를 다시 연결해줘야 한다고 알고 있는데, 이는 곧 이어서 작성할 것이다.


