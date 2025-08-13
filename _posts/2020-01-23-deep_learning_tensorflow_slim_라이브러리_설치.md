---
categories:
  - 'Blog'
tags:
  - '딥러닝'
  - '라이브러리설치'
  - '이미지셋다운로드'
  - 'download_and_convert_data.py'
  - 'tansorflow'
last_modified_at: '2025-05-30T16:03:59+09:00'
title: '[2025-08-13] - Post'
excerpt: ''
layout: 'post'
lang: 'ko'
permalink: '/posts/2020-01-23-deep_learning_tensorflow_slim_라이브러리_설치/'
alt_en: '/en/posts/2020-01-23-deep_learning_tensorflow_slim_라이브러리_설치/'
---

## [Deep Learning] Tensorflow slim 라이브러리 설치

코딩정보/Deep Learning

2020-01-23 14:42:06

* * *

안녕하세요

이번 시간 포스팅 내용은 텐소플로우에 모델을 추가하고 학습할수 있게 하기 위한

slim 라이브러리 설치 방법입니다

해당 포스팅을 검색해서 찾아오셨다면 이미 기본 적인 내용을 알고 오셨으리라 생각합니다

그럼 slim 라이브러리 설비 방법에 대해 포스팅해드리겠습니다

환경으로는

1)Anaconda3

2)Tensorflow 1.13.1

3)이미지모델라이브러리

Anaconda3 + Tensorflow 설치 방법은 저번 포스팅에 올려있으니 확인하시면 될거 같습니다

<https://codingman.tistory.com/77?category=741547>

[ [Deep Learning] Anaconda3 + Tensorflow 사용하기 안녕하세요 코딩연습생 입니다ㅠ 개발 블로그를 운영하면서
이것저것 많이 정보를 올리고 있는데 해보고자 하는 연습물이 잘 안풀려서 요즘 1일 1포스팅이 잘 안 이루어지고 있습니다ㅠ 대충 포스팅 글
올리기에.. codingman.tistory.com ](https://codingman.tistory.com/77)

그럼 이미지 모델 라이브러리 다운로드와 적용 방법에 대해 포스팅 하겠습니다

1\. 깃헙에 가서 모델 라이브러리를 다운로드 받습니다

(아래 링크를 클릭하면 해당 싸이트로 이동합니다)

<https://github.com/tensorflow/models>

[ tensorflow/models Models and examples built with TensorFlow. Contribute to
tensorflow/models development by creating an account on GitHub. github.com
](https://github.com/tensorflow/models)

2\. 다운로드 받은 모델 라이브러리 중 해당 위치의 파일을 열어 줍니다

(Model\models-master\models-master\research\slim\download_and_convert_data.py)

(저는 Anaconda3에 포함되어 있는 spyder를 이용해서 열었습니다)

![](/assets/images/deep_learning_tensorflow_slim_라이브러리_설치/img.png)

3\. download_and_convert_data.py 파일 내용중 210번 줄의 내용을 주석 처리 합니다

![](/assets/images/deep_learning_tensorflow_slim_라이브러리_설치/img_1.png)

4\. 파이썬의 텐서플로우를 통해 TFRecord 포멧으로 변환 해줍니다

1) 가상환경을 활성해 해줍니다

2) 모델 라이브러리가 설치된 경로를 지정해 줍니다

(DOS를 사용해 보신 분이라면 명령어가 비슷해서 쉽가 하 실수 있을거 같습니다)

3) TFRecord 생성 명령어를 실행

    
    
    python download_and_convert_data.py --dataset_name=flowers --dataset_dir=/tmp/flowers

![](/assets/images/deep_learning_tensorflow_slim_라이브러리_설치/img_2.png)

[오류 처리]

1\. 실행 시 다음과 같은 오류가 발생할 수 있습니다

\- ModuleNotFoundError: No module named 'contextlib2'

![](/assets/images/deep_learning_tensorflow_slim_라이브러리_설치/img_3.png)

그럴경우 다음 명령어를 실행해 줍니다

    
    
    pip install contextlib2

![](/assets/images/deep_learning_tensorflow_slim_라이브러리_설치/img_4.png)

2\. 다음 오류가 발생할 수 있습니다

\- ModuleNotFoundError: No module named 'PIL'

![](/assets/images/deep_learning_tensorflow_slim_라이브러리_설치/img_5.png)

다음 명령어를 실행 줍니다

    
    
    pip install pillow

![](/assets/images/deep_learning_tensorflow_slim_라이브러리_설치/img_6.png)

3\. 해당 오류가 나탈날 경우 입니다

\- AttributeError: module
'[tensorflow.python.util.compat'](tensorflow.python.util.compat') has no
attribute 'v1'

이 경우 기존 설치된 tensorflow를 삭제하고 다운 그레이드를 해야 합니다

다음 명령어를 실행해 줍니다

    
    
    pip uninstall tensorflow

![](/assets/images/deep_learning_tensorflow_slim_라이브러리_설치/img_7.png)

다음 명령어를 실행해 줍니다

    
    
    pip install tensorflow==1.13.1

![](/assets/images/deep_learning_tensorflow_slim_라이브러리_설치/img_8.png)

TFRecord 포맷 생성 명령어를 다시 실행해 줍니다

    
    
    python download_and_convert_data.py --dataset_name=flowers --dataset_dir=/tmp/flowers

![](/assets/images/deep_learning_tensorflow_slim_라이브러리_설치/img_9.png)

다음과 같은 문구가 뜬다면 설치에 정상 성공 하신겁니다

"Finished converting the Flowers dataset!"

  

#딥러닝 #라이브러리설치 #이미지셋다운로드 #download_and_convert_data.py #tansorflow

