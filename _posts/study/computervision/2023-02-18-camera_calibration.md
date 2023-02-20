---
layout: post
title: Camera Calibration 
description: >
  카메라 켈리브레이션에 대해 정리해본다.
grouped: true

categories: 
  - study
  - computervision
tags: 
  - 카메라기하학
  - 카메라캘리브레이션
  - 멀티카메라
 
date: 2023-02-15
last_modified_at: 2023-02-18
comments: true
published: true
---
Camera Calibration
---
<!-- ![GitHub Logo](/images/logo.png) -->

이 포스트에는 1년 전쯤 학부연구생을 하며 Camera Calibration에 대해 공부했던 내용들을 정리하였다.

![slide01](/assets/img/study/computervision/camera_calibration/slide01.PNG)  
Camera Calibration이란 위와 같이 3차원인 세상을 2차원인 이미지로 담는 과정에서 발생하는 왜곡을 보정하는 것이라 할 수 있다.
이를 반드시 거쳐야만이 2d의 이미지가 실제 3d상의 공간좌표와 일치할 수 있으며, 이 과정은 영상 처리 및 컴퓨터 비전 분야에서 반드시 필요하다.  

![slide02](/assets/img/study/computervision/camera_calibration/slide02.PNG)  
Camera Calibration의 개념 이전에 카메라의 작동원리부터 알아야 한다. 고전적인 카메라는  
이미 많이 알려져 있듯이 바늘 구멍을 통해 외부의 상이 거꾸로 투영되는 형식이다.
이때, 바늘구멍(렌즈)으로부터 상이 맺히는 곳(이미지 센서)까지의 거리가 초점거리 f 이다.  
렌즈를 사용하는 카메라는 영상 왜곡의 가능성이 있기에, Camera Calibration이 필요하다.  