---
categories:
  - 'Blog'
tags:
  - 'Nvidia'
  - 'CUDA'
  - 'CUDA'
  - 'tensorflow'
  - 'cuDNN'
last_modified_at: '2025-05-30T16:04:00+09:00'
title: '[2025-08-13] - Post'
excerpt: ''
layout: 'post'
lang: 'ko'
permalink: '/posts/2020-02-06-nvidia_cuda_윈도우에서_cuda_설치_하기/'
alt_en: '/en/posts/2020-02-06-nvidia_cuda_윈도우에서_cuda_설치_하기/'
---

## [Nvidia CUDA] 윈도우에서 CUDA 설치 하기

코딩정보/Nvidia CUDA

2020-02-06 14:09:33

* * *

안녕하세요

요즘 딥러닝 구현을 위해 열심히 공부 중인 코딩연습생입니다ㅎㅎ

Anaconda3 설치 부터 하나씩 배워가며 포스팅을 진행하고 있는데요

과정중에 하나인 CUDA에 대해 포스팅 해보도록 하겠습니다

제일 먼저 CUDA가 무엇인지가 궁금하실 겁니다 물론 이 포스팅을 검색해서 오신 분이시라면

당연히 알고 계실꺼지만 혹시 처음 오시는 분 또는 아직 개념 공부를 하고 있는 분들을 위해 간략하게

정의하자면 다음과 같습니다

CUDA란?

\- CUDA (Computed Unified Device Architecture) 는 NVIDIA 사에서 개발한 GPU (Graphic
Processing Unit)

개발 툴이다.

CUDA는 전통적으로 CPU가 처리하였던 응용 프로그램의 계산을 GPU로 병렬처리 하도록 하는 기술의 일종

![](/assets/images/nvidia_cuda_윈도우에서_cuda_설치_하기/img.png)

사실 이번 포스팅에서 CUDA가 무엇인지 몰라도 크게 문제는 되지 않습니다

그냥 개념 정보만 알고 있어도 시작에 반이 끝난것이죠ㅎㅎ

이제 포스팅의 주제로 돌아와서 CUDA를 설치 하는 방법에 대해 설명 하겠습니다

먼저 Nvidia에서 제공해주는 Toolkit과 cuDNN SDK를 설치해야 합니다

1) CUDA Toolkit Archive

\- 저의 경우에는 CUDA 8.0을 설치 하였습니다

<https://developer.nvidia.com/cuda-toolkit-archive>

[ CUDA Toolkit Archive Previous releases of the CUDA Toolkit, GPU Computing
SDK, documentation and developer drivers can be found using the links below.
Please select the release you want from the list below, and be sure to check
www.nvidia.com/drivers for more recent production developer.nvidia.com
](https://developer.nvidia.com/cuda-toolkit-archive)

![](/assets/images/nvidia_cuda_윈도우에서_cuda_설치_하기/img_1.png)

2) cuDNN SDK

\- cuDNN의 경우 Nvidia에 로그인하셔야지만 다운로드가 되오니 로그인해서 다운로드 하세요

\- cuDNN의 경우 6.0 버전의 Windows10 버전용을 다운로드 했습니다

<https://developer.nvidia.com/rdp/cudnn-download>

불러오는 중입니다...

![](/assets/images/nvidia_cuda_윈도우에서_cuda_설치_하기/img_2.png)

3) 다운로드 받은 CUDA 파일을 설치 합니다

\- 설치 화면은 생략하겠습니다 별 다른 이슈가 없이 그냥 Next로 설치하면 됩니다

\- 저의 경우 디폴트 경로에 설치하였습니다

(C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v8.0)

4) cuDNN 라이브러리 DLL 등록

\- 다운로드 받은 cuDNN 압축 해제를 하면 다음과 같은 폴더 3개로 구성되어 있습니다

![](/assets/images/nvidia_cuda_윈도우에서_cuda_설치_하기/img_3.png)

\- CUDA가 설치되어 있는 폴더로 이동하여 동일 폴더 항목으로 세부 파일을 복사해 줍니다

![](/assets/images/nvidia_cuda_윈도우에서_cuda_설치_하기/img_4.png)

(cuDNN 폴더 안에 세부 파일을 -> CUDA 설치경로에 동일한 폴더 안으로 복사)

이렇게 해주시면 CUDA와 cuDNN 설치가 완료 되어 집니다

마지막으로 확인 하셔야 할것은 환경변수에 경로 설정이 올바르게 생성 되었는지만 확인하시면 됩니다

윈도우10에서 바로실행을 실행시킵니다

(아래 그림처럼 sysdm.cpl이라고 치시고 실행 시킵니다)

![](/assets/images/nvidia_cuda_윈도우에서_cuda_설치_하기/img_5.png)

시스템속성창에서 고급 -> 환경 변수를 선택 합니다

![](/assets/images/nvidia_cuda_윈도우에서_cuda_설치_하기/img_6.png)

CUDA_PATH와 CUDA_PATH_V8_0이 생성되었는지 확인 합니다

(CUDA_PATH_V8_0은 CUDA 버전에 따라 이름이 다를 수 있습니다)

![](/assets/images/nvidia_cuda_윈도우에서_cuda_설치_하기/img_7.png)

환경 변수 생성까지 확인하셨다면 Tensorflow GPU를 사용하기 위한 CUDA 설치가 완료 된 것입니다

  

#Nvidia CUDA #CUDA #CUDA toolkit #tensorflow #cuDNN

