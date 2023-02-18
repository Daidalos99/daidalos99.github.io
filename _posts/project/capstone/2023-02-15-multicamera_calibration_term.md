---
layout: post
title: A Convinent Multi-Camera Self-Calibration for Virtual Environments 
description: >
  상기 논문을 읽고 모르는 용어들을 정리하였다.
grouped: false

categories: [project, capstone]
tags: 
  - 논문리뷰
  - 카메라캘리브레이션
  - 멀티카메라
 
date: 2023-02-15
last_modified_at: 2023-02-15
comments: true
published: true
---
[용어정리] A Convinent Multi-Camera Self-Calibration for Virtual Environments 
---

나는 아직 선형대수학에 대한 지식도 해박하지 못하고, 또 컴퓨터비전을 잘 알지도 못하기 때문에 이 논문을 읽으면서 용어적인 제약이 꽤 있었다.
따라서, 본 논문을 한번 읽고, 모르는 용어에 대하여 한번 짚고 넘어가고자 한다. 후에 이 논문을 읽을 분(이 계실진 모르지만..)에게 도움이 되면 좋겠다.
여러 용어들은 Linear Algebra, Camera Geometry, Epipolar Geometry 등으로 분류하여 정리하고자 하였다.

### Linear Algebra
- Linear / Non Linear
- Euclidian
- Projective
- SVD(Singular Value Decomposition)
- Symmetric
- Rank
- Factorization(rank-n factorization)
- Intersection
- Basis(기저)
- Sub-matrix
- Matrix Decomposition
- (2D) Correlation

### Camera Geometry
- Orthogonal
- Skew
- Focal Length
- Square Pixel
- Occlusion
- Intrinsic, Extrinsic Matrix


### Epipolar Geometry
- Coplanar(ity)
- Functional Matrix
- Homography
- Epipole
- Epipolar Geometry
- Base-line

### Image Processing Algorithm
- RANSAC(pairwise RANSAC analysis, RANSAC 7-point algorithm)

### Etc.
- Working Volume
- Reconstruction
- Bundle Adjustment(BA)
  

용어 정리를 마치고 보니 Tmi가 아닌가 싶기도 하지만, 덕분에 선형 대수학 및 비전 분야의 여러 언어를 다시금 상기시키는 계기가 되었다.