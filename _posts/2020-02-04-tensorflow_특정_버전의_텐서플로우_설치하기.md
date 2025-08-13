---
categories:
  - 'Blog'
tags:
  - 'tensorflow'
  - '텐서플로우'
  - 'tensorflow'
  - '텐서플로우'
  - 'tensorflow'
last_modified_at: '2025-05-30T16:03:59+09:00'
title: '[2025-08-13] - Post'
excerpt: ''
layout: 'post'
lang: 'ko'
permalink: '/posts/2020-02-04-tensorflow_특정_버전의_텐서플로우_설치하기/'
alt_en: '/en/posts/2020-02-04-tensorflow_특정_버전의_텐서플로우_설치하기/'
---

## [Tensorflow] 특정 버전의 텐서플로우 설치하기

코딩정보/TensorFlow

2020-02-04 10:55:05

* * *

안녕하세요

이번 포스팅은 Anaconda에서 특정 버전의 텐서플로우를 설치 하는 방법을 설명 하도록 하겠습니다

CUDA나 CNN등을 사용할때 참 많은 환경 조건을 따집니다

그중에서 Python의 버전과 텐서플로우의 버전에 따라 참 많은 오류가 발생하게 되는데요

그럴때 Phthon의 버전에 알맞는 텐서플로우 버전을 지정해서 설치 할 수 있는 방법을 설명 드리겟습니다

1\. Anaconda 명령 프롬프트 실행

\- 관리자 권한으로 실행하시기 바랍니다

![](/assets/images/tensorflow_특정_버전의_텐서플로우_설치하기/img.jpg)

2\. 다음 명령어를 실행하여 텐서플로우를 설치합니다

\- 저는 Python 3.6 버전과 호환이 가능한 1.9버전을 설치 합니다

\- tensorflow-gpu는 gpu를 사용하는 텐서플로우 입니다

\- 일반 cpu를 사용할 경우 그냥 tensorflow로 치시면 됩니다

    
    
    conda install tensorflow-gpu=1.9.0

![](/assets/images/tensorflow_특정_버전의_텐서플로우_설치하기/img_1.jpg)

3\. 최종 확인 명령어

\- 'Y'를 입력하여 다음 단계를 진행해 주세요

![](/assets/images/tensorflow_특정_버전의_텐서플로우_설치하기/img_2.jpg)

4\. 설치 진행

\- 최종 설치가 완료 될 때까지 기다려 주세요

\- 설치시 까지 수분이 소요 됩니다

![](/assets/images/tensorflow_특정_버전의_텐서플로우_설치하기/img_3.jpg)

5\. 설치 완료 확인

\- 설치가 완료 되어 지면 다음과 같이 'done'가 나타납니다

![](/assets/images/tensorflow_특정_버전의_텐서플로우_설치하기/img_4.jpg)

6\. 텐서플로우 테스트 해보기

\- tensorflow가 정상적으로 설치되고 실행되는지 확인을 합니다

\- 명령 프롬프트에 하나씩 구문을 실행 합니다

    
    
    import tensorflow as tf
    hello = tf.constant('Hello, Tensorflow!')
    sess = tf.Session()
    print(sess.run(hello))

![](/assets/images/tensorflow_특정_버전의_텐서플로우_설치하기/img_5.jpg)

b'Hello, Tensorflow!'라고 뜨신다면 정상 설치가 된것입니다

  

#tensorflow #텐서플로우 #tensorflow 특정 버전 #텐서플로우 테스트 #tensorflow 실행하기

