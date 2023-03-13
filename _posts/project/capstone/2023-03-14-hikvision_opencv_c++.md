---
layout: post
title: Hikvision 머신비전 카메라 OpenCV/C++
description: >
  Hikvision 머신비전 카메라 OpenCV/C++ Qt로 연동하기
grouped: true

categories: 
  - project
  - capstone
tags: 
  - hikvision
  - 비전카메라
  - 머신비전카메라
  - 산업용카메라
  - C++연동
  - QT연동
  - MV-CA013-20GC
 
date: 2023-03-14
last_modified_at: 2023-03-14
comments: true
published: true
sitemap :
  changefreq : daily
  priority : 1.0
---
Hikvision 머신비전 카메라 OpenCV/C++ Qt로 연동하기
---
이번 캡스톤을 위해 지난번 게시물에서는 Camera Calibration에 대해 다루었다. 
캡스톤에서 사용할 (머신)비전용 카메라는 Hikvision사에서 제작한 MV-CA013-20GC 모델이다.
![img01](/assets/img/project/capstone/hikvision_opencv_c++/mv_ca013_20gc.jpg){: width="200" height="200"}

한국 Hikvision 측에서 공식적으로 판매하는 제품은 아니며(본사는 중국 항저우이다), 기존에는 각종 비전 카메라 판매 업체에서 수입을 해서 팔다가, 이제는 다른 제품으로 교체되며 단종이 된 제품 같다. 

MV-CA013-20GC 카메라는 GigE(Gigabit Ethernet, 데이터를 1기가비트의 속도로 전송)이라는 통신을 사용한다. 머신 비전용 카메라들을 보면 GigE 방식을 많이 사용하는 것 같다. 이러한 산업용 카메라를 사용 시 주의할 점으로는 
1. 랜 허브를 잘 고를 것(기가비트 이더넷의 통신 속도를 보장할 것)
2. 랜선을 잘 보고 살 것(Cat6 이상의 케이블)
   
정도가 있는 것 같다. 랜 허브를 사지 않는다면, 비전용 랜카드, 즉 프레임 그래버(Frame Grabber)를 사용할 수 있으며, 이는 전원 자체를 랜선으로 공급하는 PoE(Power over Ethernet) 방식인 듯 하다. 이름 자체가 프레임 그래버인 만큼, 일반적인 기가비트 랜 허브보다 좋을 것으로 생각되지만, 이번 프로젝트에서는 다수의 카메라를 사용하는 만큼 프레임 그래버 카드도 2장이 필요하고, M-ATX 보드로는 이를 감당할 수 없기에, 그냥 기가비트 랜 허브를 사용하기로 하였다. ~~안되면 PC를 갈아야되나~~

이번 프로젝트에서는 Qt Creator 6로 C++을 사용, OpenCV4를 사용하여 카메라 영상을 받아오고자 하였다. Hikvision 카메라 연결에 대한 게시물이 별로 없었으나, [슈크림네 님의 블로그](https://parkeh-dev.tistory.com/2)에 정리가 상당히 잘 되어 있어서, 코드는 이를 상당부분 참고하였다.

이 블로그에서 알 수 있듯이, Hikvision에서는 MVS라는 카메라 사용 프로그램을 배포하는데, 이를 설치할 때, 카메라 사용 메뉴얼까지 같이 설치되고, 이는 매우 상세하고 친절하여 도움이 많이 되었다.
![img01](/assets/img/project/capstone/hikvision_opencv_c++/mvs.png)