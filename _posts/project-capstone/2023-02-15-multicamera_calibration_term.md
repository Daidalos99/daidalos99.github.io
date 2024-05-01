---
layout: post
title: [논문용어정리]A Convenient Multi-Camera Self-Calibration for Virtual Environments
date:   2023-02-15
excerpt: 논문을 읽고 모르는 용어들을 정리하였다.
categories: [project-capstone]
comments: true
---
[용어정리] A Convenient Multi-Camera Self-Calibration for Virtual Environments 
---

나는 아직 선형대수학에 대한 지식도 해박하지 못하고, 또 컴퓨터비전을 잘 알지도 못하기 때문에 이 논문을 읽으면서 용어적인 제약이 꽤 있었다.
따라서, 본 논문을 한번 읽고, 모르는 용어에 대하여 한번 짚고 넘어가고자 한다. 후에 이 논문을 읽을 분(이 계실진 모르지만..)에게 도움이 되면 좋겠다.
여러 용어들은 Linear Algebra, Camera Geometry, Epipolar Geometry 등으로 분류하여 정리하고자 하였다.  
선형대수학 용어 정리에는 아래 링크(로스카츠의 AI 머신러닝 블로그의 정철원님 게시물)를 참고하였다.  
[losskatsu.github.io](https://losskatsu.github.io/linear-algebra/rank-dim/#%EC%B0%A8%EC%9B%90dimension)

## Linear Algebra
- **Linear / Non Linear**
- **Euclidian Stratification**
- **Projective**
- **SVD(Singular Value Decomposition)**
- **Symmetric**
- **Factorization(rank-n factorization)**
- **Intersection**
- **Basis(기저)**  
    위키백과에 따르면, 기저는 다음과 같은 뜻을 지닌다.
    > 선형대수학에서, 어떤 벡터 공간의 기저(basis)는 **그 벡터 공간을 선형생성하는 선형독립인 벡터들**이다. 달리 말해, 벡터 공간의 임의의 벡터에게 선형결합으로서 유일한 표현을 부여하는 벡터들이다.  

    즉, 2차원 좌표평면을 예로 든다고 하면 \\((1,0),(0,1)\\)의 경우 여기에 각각 실수를 곱하고 더하면(이 벡터조합을 이용하면), 2차원 좌표평면의 **어떤 벡터든지 나타낼 수 있다**. 따라서 이는 2차원 좌표평면 나타내는 **기저(basis)**벡터라고 할 수 있다. \\((x,0),(0,y)\\)의 꼴이라면 모두 기저(basis)가 될 수 있지만, 기저를 구성하는 벡터의 수는 유일하다. 2차원의 경우 좌표평면을 구성하는 기저벡터는 2개이다. **기저는 벡터공간을 생성하는 선형독립인 벡터이다.**  
- **Subspace**  
    부분공간은 기저벡터로 만들 수 있는 전체 벡터공간의 일부분이다. 전체 공간이 3차원이면 그 기저벡터 3개중 일부인 2개 혹은 1개를 사용해서 만든 선이나 면이 부분공간이 될 것이다.  
- **Span**  
    전체 벡터공간이 5차원이고, 3개의 기저 벡터 집합을 \\(S\\)라고 하고, 집합 \\(S\\)에 속하는 기저 벡터들로 구성되는 3차원 부분 공간을 \\(W\\)라고 했을 때 \\(S\\)는 부분 공간 \\(W\\)를 span한다고 말하고 \\(W = span(S)\\) 라고 표현한다. 위의 예에서는 전체가 5차원 이지만 기저벡터가 3차원까지만 표현 가능하므로, span되는 공간은 \\(W = span(S) = 3\\)차원이라고 할 수 있다.     
- **Rank**  
    어떠한 행렬이 있을 때, 그 행렬의 열벡터에 의해 span된 벡터공간의 차원(위키)을 의미한다. 한 행렬의 행공간과 열공간은 차원이 같다고 할 수 있는데, 이러한 특성 떄문에 아래와 같은 성질이 성립한다.  
    \\[rank(A) = rank(A^T)\\] 

    즉, 행렬 \\(A\\)의 랭크와 그 전치행렬의 랭크는 같다는 것이다.  
    다음으로, 행렬 A가 \\((n*m)\\)일때, \\(n=rank(A)\;or\;m=rank(A^T)\\)이면 **full rank**라고 한다.
- **Sub-matrix**
- **Matrix Decomposition**
- **(2D) Correlation**

## Camera Geometry
- **Orthogonal**
- **Skew**
- **Focal Length**
- **Square Pixel**
- **Occlusion**
- **Intrinsic, Extrinsic Matrix**


## Epipolar Geometry
- **Coplanar(ity)**
- **Functional Matrix**
- **Homography**
- **Epipole**
- **Epipolar Geometry**
- **Base-line**

## Image Processing Algorithm
- **RANSAC(pairwise RANSAC analysis, RANSAC 7-point algorithm)**

## Etc.
- **Working Volume**
- **Reconstruction**
- **Bundle Adjustment(BA)**
  

용어 정리를 마치고 보니 Tmi가 아닌가 싶기도 하지만, 덕분에 선형 대수학 및 비전 분야의 여러 언어를 다시금 상기시키는 계기가 되었다.