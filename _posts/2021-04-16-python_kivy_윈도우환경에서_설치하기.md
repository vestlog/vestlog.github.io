---
categories:
  - 'Blog'
tags:
  - '기타'
last_modified_at: '2025-05-30T16:04:11+09:00'
title: '[2025-08-13] - Post'
excerpt: ''
layout: 'post'
lang: 'ko'
permalink: '/posts/2021-04-16-python_kivy_윈도우환경에서_설치하기/'
alt_en: '/en/posts/2021-04-16-python_kivy_윈도우환경에서_설치하기/'
---

<div class="lang-panel lang-ko" lang="ko">
## [PYTHON] KIVY 윈도우환경에서 설치하기

코딩정보/Python

2021-04-16 13:00:30

* * *

안녕하세요

코딩연습생입니다

하 요즘은 24시간이 부족하네요ㅎㅎㅎ

주식 분석용 AI도 관리하고..블로그 포스팅.. 가상화폐 자동 매매 봇..ㅎㅎㅎ

이번생 한번 잘 살아볼려고 정말 아둥바둥 하네요ㅋㅋㅋ

이번에 가상화폐 자동 매매 봇을 돌리면서 서버와 클라이언트를 분리해서

좀 대중성(?)을 주어볼려고 생각해낸 아이디어가 클라이언트를 앱으로 제공하는걸 구상중인데

파이썬으로 앱에 쉽게 접근하는 방법으로 키비(kivy)가 많이 거론되네요

그래서 저도 키비를 한번 시도해 볼려고 합니다

그전에 해야 할게 당연히 키비 설치 방법이겠죠ㅎ

**_※ 해당 PC에 파이썬이 설치되어 있다는 가정하여 진행됩니다_**

1\. 콘솔에서 아래 명령어를 실행하여 pip, wheel, virtualenv를 확인합니다

    
    
    python -m pip install --upgrade pip wheel setuptools virtualenv

![](/assets/images/python_kivy_윈도우환경에서_설치하기/img.png)

2\. 기본 종속성을 설치합니다

    
    
    python -m pip install docutils pygments pypiwin32 kivy_deps.sdl2 kivy_deps.glew kivy_deps.gstreamer

![](/assets/images/python_kivy_윈도우환경에서_설치하기/img_1.png)

3\. python 3.5 이상에서는 glew 대신 angle backend를 사용할 수도 있다 따라서 다음과 같은 명령어로 설치할 수 있다

    
    
    python -m pip install kivy_deps.angle

![](/assets/images/python_kivy_윈도우환경에서_설치하기/img_2.png)

4\. 키비(kivy)를 설치 한다

    
    
    python -m pip install kivy

![](/assets/images/python_kivy_윈도우환경에서_설치하기/img_3.png)

5\. 키비(kivy) 예제를 설치한다

    
    
    python -m pip install kivy_examples

![](/assets/images/python_kivy_윈도우환경에서_설치하기/img_4.png)

  


</div>
<div class="lang-panel lang-en" lang="en">
(*No embedded English lines found. Add translations later.*)

</div>
