---
title:  "[2021-03-26] - [텐서플로워] Tensorflow 1.x버전 코드를 Tensorflow 2.x버전으로 사용"
categories:
  - Blog
tags:
  - "tensorflow"
  - "텐서플로우"
  - "Tensorflow"
  - "Tensorflow"
  - "텐서플로우"
  - "tf.contrib.layers.fully_connected"
  - "runtimeerror:"
  - "attributeerror:"
last_modified_at: 2025-05-30T16:04:10+09:00
---

## [텐서플로워] Tensorflow 1.x버전 코드를 Tensorflow 2.x버전으로 사용

코딩정보/TensorFlow

2021-03-26 07:38:24

* * *

안녕하세요

코딩연습생입니다~

정말 오랜만에 포스팅 하는거 같습니다..ㅠ

요즘 참 하는일 모두 하나하나 태글인거 같습니다..ㅎㅎ

정기적인 주식 관련 정보 포스팅을 하는 프로그램도 자주 뻑(?)이 나고.. 개선할려고 이것저것 수정 중인데..

쉽지가 않네요..

세금 관련 문제...하앜...ㅋㅋ

그래도 블로그 시작할때의 초기 마음가짐을 다시 바로 잡고...

포스팅을 올리도록 하겠습니다

이번 포스팅은 Tensorflow 1.x 버전의 소스코드를 사용하다가 GPU 카드를 변경하거나 또는 다른Tensorflow 2.x 버전의

소스 코드와 같이 사용해야 하는 상황이 발생하였을때 문제가 생깁니다

여기 Tensorflow 2.0이 Release 되면서 기존 문제 되는 사항을 잘 정리한 블로그가 있어서 첨부 한다

<http://solarisailab.com/archives/2640>

[ 33\. TensorFlow 2.0 Release 및 변경사항 정리 – tf.Session & tf.placeholder 삭제, @tf.function, tf_upgrade_v2 | 솔라 2019-09-30에 TensorFlow 2.0이 정식 Release 되었다. 그동안의 많은 개발사항을 반영한 메이저 업데이트가 이루어진만큼 API 구조가 대대적으로 변경되었다. 자세한 변경사항은 TensorFlow GitHub 저장소의 릴 solarisailab.com ](http://solarisailab.com/archives/2640)

특히 Release가 변하면서 가장 문제가 되는 부분이 몇가지 있다 개인적인으로 사용시 문제가된 항목들을

해결한 방법을 예제를 들어 설명 하겠다

1\. placeholder 사용 불가

해결 방법

(아래 예제 소스를 통해 같은 형태로 사용하면 된다)

    
    
    import tensorflow.compat.v1 as tf
    tf.disable_v2_behavior()
    
    #기존 코드
    X = tf.placeholder(tf.float32, [None, seq_length, input_data_column_cnt])
    #변경 코드
    X = tf.compat.v1.placeholder(tf.float32, [None, seq_length, input_data_column_cnt])

2\. rnn 사용 불가

해결 방법

(아래 예제 소스를 통해 같은 형태로 사용하면 된다)

    
    
    import tensorflow.compat.v1 as tf <--- 2.x 버전 텐서(2.x을 1.x 버전처럼 사용)
    
    tf.disable_v2_behavior()
    tf.compat.v1.set_random_seed(777)
    
    #기존 코드
    cell = tf.contrib.rnn.BasicLSTMCell(num_units=rnn_cell_hidden_dim,
                                         forget_bias=forget_bias, state_is_tuple=True, activation=tf.nn.softsign)
    
    #변경 코드
    cell = tf.compat.v1.nn.rnn_cell.BasicLSTMCell(num_units=rnn_cell_hidden_dim,
                                                     forget_bias=forget_bias, state_is_tuple=True,
                                                     activation=tf.nn.softsign)

3\. layerstf.contrib.layers.fully_connected 사용 불가

해결 방법

(아래 순서에 따라 설치하고 소스코드를 아래 형태로 변환해서 사용하면 된다)

1) pip install tf-slim <\-- 해당 명령올 패키지 설치

![](/assets/images/텐서플로워_tensorflow_1_x버전_코드를_tensorflow_2_x버전으로_사용/img.png)

2) 패키지 선언

    
    
    from tf_slim.layers import layers as _layers

3) 소스코드 변경

    
    
    # 기존 코드
    hypothesis = tf.contrib.layers.fully_connected(hypothesis[:, -1], output_data_column_cnt, activation_fn=tf.identity)
    
    #변경 코드
    hypothesis = _layers.fully_connected(hypothesis[:, -1], output_data_column_cnt, activation_fn=tf.identity)

이렇게 해당 부분들을 수정하고 나면

소스코드가 정상적으로 실행 되는 것을 확인 할 수가 있다

기존 Tensorflow 1.4 버전으로 구성된 코드를 Tensorflow 2.0 버전으로 변경 후 위에 관련된 부분을 수정한뒤에

실행하여 동작하는 모습이다

![](/assets/images/텐서플로워_tensorflow_1_x버전_코드를_tensorflow_2_x버전으로_사용/img_1.png)

  

#tensorflow #텐서플로우 #Tensorflow 1.x #Tensorflow 2.x #텐서플로우 버전 변경
#tf.contrib.layers.fully_connected #runtimeerror: tf.placeholder() is not
compatible with eager execution #attributeerror: module 'tensorflow' has no
attribute 'reset_default_graph'

