---
categories:
  - 'Blog'
tags:
  - '평가'
  - 'Slim'
  - '학습'
  - '라이브러리'
  - 'deep'
  - 'tensorflow'
  - '실예측정확도'
  - '유사율'
  - '모델학습'
last_modified_at: '2025-05-30T16:04:00+09:00'
title: '[2025-08-13] - Post'
excerpt: ''
layout: 'post'
lang: 'ko'
permalink: '/posts/2020-02-06-deep_learning_slim_라이브러리를_이용한_설치_학습_평가/'
alt_en: '/en/posts/2020-02-06-deep_learning_slim_라이브러리를_이용한_설치_학습_평가/'
---

<div class="lang-panel lang-ko" lang="ko">
## [Deep Learning] slim 라이브러리를 이용한 설치, 학습, 평가

코딩정보/Deep Learning

2020-02-06 14:49:45

* * *

안녕하세요

이번 포스팅은 현재 연습중인 Tensorflow를 통해 pb 파일 생성하기 위한 과정으로

이미지셋을 통한 라이브러리 설치 및 학습 그리고 학습된 라이브러리에 대한 평가 방법에 대한 포스팅을

해볼께요

첫번째로 Anaconda와 텐서플로우 설치를 먼저해야 합니다

설치 방법에 대해서는 아래 링크를 통해 확인하시기 바랍니다

<https://codingman.tistory.com/77>

[ [Deep Learning] Anaconda3 + Tensorflow 사용하기 안녕하세요 코딩연습생 입니다ㅠ 개발 블로그를 운영하면서
이것저것 많이 정보를 올리고 있는데 해보고자 하는 연습물이 잘 안풀려서 요즘 1일 1포스팅이 잘 안 이루어지고 있습니다ㅠ 대충 포스팅 글
올리기에.. codingman.tistory.com ](https://codingman.tistory.com/77)

참고로 이번 포스팅에 사용된 버전 정보는 다음과 같습니다

=============================================================

1) Anaconda3

2) Python 3.7

3) Tensorflow 1.14

4) CUDA 8.0

==============================================================

위의 리스트 순서로 설치를 진행하시면 됩니다

CUDA 설치 방법은 아래 링크 포스팅을 참조해주세요

<https://codingman.tistory.com/81>

[ [Nvidia CUDA] 윈도우에서 CUDA 설치 하기 안녕하세요 요즘 딥러닝 구현을 위해 열심히 공부 중인 코딩연습생입니다ㅎㅎ
Anaconda3 설치 부터 하나씩 배워가며 포스팅을 진행하고 있는데요 과정중에 하나인 CUDA에 대해 포스팅 해보도록 하겠습니다 제일
먼.. codingman.tistory.com ](https://codingman.tistory.com/81)

이렇게 환경 설정을 모두 마치셨으면

다음 진행해야할 것은 Slim 이미지셋 설치와 TFRecord 생성 방법입니다

위의 내용은 아래 포스팅을 참조해서 따라해 주세요

<https://codingman.tistory.com/78>

[ [Deep Learning] Tensorflow slim 라이브러리 설치 안녕하세요 이번 시간 포스팅 내용은 텐소플로우에 모델을 추가하고
학습할수 있게 하기 위한 slim 라이브러리 설치 방법입니다 해당 포스팅을 검색해서 찾아오셨다면 이미 기본 적인 내용을 알고 오셨으리라
생각.. codingman.tistory.com ](https://codingman.tistory.com/78)

내용이 상당히 길기 때문에 포스팅을 나누어 올리고 있습니다

다소 헷갈릴수 있는데 어쩔수 없이 나눠 포스팅한점을 양해 주시기 바랍니다

이제 위의 레코드 파일 생성까지 완료 되셨다면 모든 환경 설정은 끝났습니다

이제 Deep Learning중 학습 방법에 대해서 Slim 모델을 통해 설명하도록 하겠습니다

저도 공부 중에 찾은 내용입니다만 학습 방법에 대해 여러가지 방법이 있습니다

그중에 제가 찾은것은 세가지 방법이 있었는데요

그중에 한가지 방법은 Tensorflow의 구버전으로 사용되는것으로 현재 저희 환경과 맞지 않아 구현이 불가능했습니다

그래서 저희가 설정한 환경에서 동작이 가능한 방법인 두가지를 설명해 드리겠습니다

1) Trainng a model from scratch

\- 저희가 만든 이미지셋을 가지고 신규 모델을 학습 하는 방법

\- Anaconda Prompt를 통해 다음 명령어를 실행

* 명령어 간략 설명

python train_image_classifier.py

\--train_dir=\tmp\train_inception_v1_flowers_logs # 모델 저장될 폴더  
\--dataset_name=flowers # 이미지 셋 이름  
\--dataset_split_name=train # 학습에 사용할 이미지 선택  
\--dataset_dir=\tmp\flowers # 이미지 셋 위치  
\--batch_size=16 # 기본 32이나 메모리 부족 에러 발생 -> 16 설정  
\--model_name=inception_v1 # 사용할 모델 이름

    
    
    python train_image_classifier.py --train_dir=\tmp\train_inception_v1_flowers_logs --dataset_name=flowers --dataset_split_name=train --dataset_dir=\tmp\flowers --batch_size=16 --model_name=inception_v1

오류가 발생하실수 있습니다 오류가 발생하였을 경우 py 파일을 약간 수정해 줍니다

다음 경로에 있는 train_image_classifier.py파일을 Spyder을 통해 열어 줍니다

![](/assets/images/deep_learning_slim_라이브러리를_이용한_설치_학습_평가/img.png)
![](/assets/images/deep_learning_slim_라이브러리를_이용한_설치_학습_평가/img_1.png)

아래와 같이 변경한뒤 저장합니다

![](/assets/images/deep_learning_slim_라이브러리를_이용한_설치_학습_평가/img_2.png)

다시 명령어를 실행 합니다

명령어가 실행되면사 step별 학습을 시작하는것을 보실수 있습니다

![](/assets/images/deep_learning_slim_라이브러리를_이용한_설치_학습_평가/img_3.png)

학습이 GPU의 성능에 따라 차이가 있을수 있지만 상당한 수분이 소요 됩니다

그래서 학습 중간에 중지 하고 싶으시면 Ctrl + C를 누루시면 종료 됩니다

학습이 완료되어 지면 다음과 같은 checkpoint 형식의 log가 생성됩니다

![](/assets/images/deep_learning_slim_라이브러리를_이용한_설치_학습_평가/img_4.png)

이어서 두번째 방식 입니다

2-1) Fine-tuning a model from an existing checkpoint

\- 마지막 layer만 새롭게 학습하는 과정

\- 완성도가 높은 모델을 사용할 수록 정확도가 올라가기 때문에 ImgaeNet에서 미리 학습된 모델을 다운 받아

사용합니다

([http:// ](http://
http://download.tensorflow.org/models/inception_v1_2016_08_28.tar.gz)[http://download.tensorflow.org/models/inception_v1_2016_08_28.tar.gz)](http://download.tensorflow.org/models/inception_v1_2016_08_28.tar.gz)

불러오는 중입니다...

\- 압축을 푼뒤 **inception_v1.ckpt** 파일을 **\tmp\my_checkpoints** 폴더로 복사하세요.

\- 다음 명령어를 1번 방법과 동일하게 실행 시킵니다

    
    
    python train_image_classifier.py
      --train_dir=\tmp\train_inception_v1_flowers_FineTune_logs
      --dataset_name=flowers
      --dataset_split_name=train
      --dataset_dir=\tmp\flowers
      --model_name=inception_v1
      --checkpoint_path=\tmp\my_checkpoints/inception_v1.ckpt
      --checkpoint_exclude_scopes=InceptionV1/Logits
      --trainable_scopes=InceptionV1/Logits
      --max_number_of_steps=1000
      --batch_size=16
      --learning_rate=0.01
      --learning_rate_decay_type=fixed
      --save_interval_secs=60
      --save_summaries_secs=60
      --log_every_n_steps=100
      --optimizer=rmsprop
      --weight_decay=0.00004

\- 1000번의 step이 완료된후 다음과 같이 checkpoint가 생성된 log가 생성됩니다

![](/assets/images/deep_learning_slim_라이브러리를_이용한_설치_학습_평가/img_5.png)

2-2) # Fine-tune all the new layers for 500 steps.

\- 전체 layer 학습하는 과정

    
    
    python train_image_classifier.py
    
    
      --train_dir=\tmp\train_inception_v1_flowers_FineTune_logs\all
      --dataset_name=flowers
      --dataset_split_name=train
      --dataset_dir=\tmp\flowers
    
      --model_name=inception_v1
    
      --checkpoint_path=\tmp\train_inception_v1_flowers_FineTune_logs
      --max_number_of_steps=500
      --batch_size=16
      --learning_rate=0.0001
      --learning_rate_decay_type=fixed
      --save_interval_secs=60
      --save_summaries_secs=60
      --log_every_n_steps=10
      --optimizer=rmsprop
      --weight_decay=0.00004

![](/assets/images/deep_learning_slim_라이브러리를_이용한_설치_학습_평가/img_6.png)

이렇게 생성된 두가지 방법을 통해 3가지의 딥러닝 모델을 학습 시켜 봤습니다

정확도 확인을 위한 평가 방법입니다

1) Flowers로부터 새롭게 만든 모델

![](/assets/images/deep_learning_slim_라이브러리를_이용한_설치_학습_평가/img_7.png)

결과를 보시면 eval/Recall_5[1]의 의미는 5개의 Class 중에 하나라도 맞으면 맞다고 보는 정확도 입니다

[1]의 결과로 보면 100%로 라는 말이네요

실예측정확도의 경우는 eval/Accuracy[0.3675] -> 36% 정도로가 평가가 나오네요

2) 이미 잘 만들어진 모델로부터 Flowers로 마지막 layer만 학습해 만든 모델

![](/assets/images/deep_learning_slim_라이브러리를_이용한_설치_학습_평가/img_8.png)

매칭 유사율 100%

실예측정확도 86%라고 평가가 나오네요

3) 2)으로 만들어진 모델에서 전체 layer를 학습해 만든 모델

![](/assets/images/deep_learning_slim_라이브러리를_이용한_설치_학습_평가/img_9.png)

매칭 유사율은 역시 100%

실예측정확도는 90%로 평가가 됩니다

결론은 기존에 잘 학습된 모델을 활용해서 그 위에 분류하고 싶은 추가적인 이미지를 학습하는 것이

실예측 정확도를 가장 효과적으로 올릴수 있다는 결론이 나온거 같네요

  

#평가 #Slim #학습 #라이브러리 #deep learning #tensorflow #실예측정확도 #유사율 #모델학습


</div>
<div class="lang-panel lang-en" lang="en">
(*No embedded English lines found. Add translations later.*)

</div>
