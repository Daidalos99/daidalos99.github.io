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

이 포스트에는 1년 전쯤 학부연구생을 하며 **Camera Calibration**에 대해 공부했던 내용들을 정리하였다.

![slide01](/assets/img/study/computervision/camera_calibration/slide01.PNG)  

Camera Calibration이란 위와 같이 **3차원인 세상을 2차원인 이미지로** 담는 과정에서 발생하는 **왜곡을 보정하는 것**이라 할 수 있다.
이를 반드시 거쳐야만이 2d의 이미지가 실제 3d상의 공간좌표와 일치할 수 있으며, 이 과정은 영상 처리 및 컴퓨터 비전 분야에서 반드시 필요하다.  
  
  
  

![slide02](/assets/img/study/computervision/camera_calibration/slide02.PNG)  

Camera Calibration의 개념 이전에 카메라의 작동원리부터 알아야 한다. 고전적인 카메라는  
이미 많이 알려져 있듯이 바늘 구멍을 통해 외부의 상이 거꾸로 투영되는 형식이다.  
이때, 바늘구멍(렌즈)으로부터 상이 맺히는 곳(이미지 센서)까지의 거리가 초점거리 f 이다.  
렌즈를 사용하는 카메라는 영상 왜곡의 가능성이 있기에, Camera Calibration이 필요하다.
또한, **실제 3차원 좌표계에서는 위쪽이 z축이지만, 카메라 좌표계(이미지 좌표계와 다름!!)에서는 광축(앞쪽)방향을 z축으로 둔다.**  
  



![slide03](/assets/img/study/computervision/camera_calibration/slide03.PNG)  

현대의 카메라에서는 바늘구멍 대신 렌즈를 사용하기에 왜곡이 발생한다.
이때, 볼록렌즈의 사용으로 인해 발생하는 왜곡을 **방사왜곡**, 렌즈와 이미지센서의 중심이 틀어져서 발생하는 왜곡을 **접선 왜곡**이라고 한다.  
  



![coordinates](/assets/img/study/computervision/camera_calibration/coordinats.jpg)  

밑으로 넘어가기 전, 우선 좌표계에 대한 이해가 필요하다. 실제 세계의 물체를 카메라로 찍었을 때,  
그 이미지가 출력되는 과정은 다음과 같다. 먼저 **세계 좌표계(world coordinates)**에서 **카메라 좌표계(camera coordinates)**로  
한번 변환이 된다. 위에서 말했듯, 세계 좌표계는 위쪽이 z, 카메라 좌표계는 앞쪽을 z축으로 한다.  
카메라 좌표계로 변환된 이미지는 이미지센서에 투영이 되는데 이를 **이미지 좌표계(image coordinates)**라 한다.
  
이미지 좌표계는 원점(0, 0)이 왼쪽 위에 있는 좌상 좌표계를 사용하며, y축의 (+)방향이 아래쪽이다.  
따라서, 카메라 좌표계(3d)에서 이미지 좌표계(2d)로의 변환이 한번 더 필요할 것이다.
  



![slide04](/assets/img/study/computervision/camera_calibration/slide04.PNG)  

위는 Camera Calibration에서 사용되는 **Camera Matrix**이다. 이 행렬의 우항부터 뜯어보자.  
우항의 세번째 행렬은 3차원 열벡터이며, 이의 4번째 원소 '1'은 scale을 나타낸다. 세계 좌표계야 당연히  
1의 비율을 가질 것이기에 1로 고정될 것이다. 이제, 이 앞에 위에서 필요하다고 한 변환들이 곱해져 나아가는 형태가 된다.