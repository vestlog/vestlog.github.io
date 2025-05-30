---
title:  "[2020-01-23] - [Deep Learning] Anaconda3 + Tensorflow 사용하기"
categories:
  - Blog
tags:
  - "아나콘다"
  - "python"
  - "파이썬"
  - "deep"
  - "딥러닝"
  - "tensorflow"
  - "텐서플로우"
  - "anaconda3"
last_modified_at: 2025-05-30T16:03:59+09:00
---

## [Deep Learning] Anaconda3 + Tensorflow 사용하기

코딩정보/Deep Learning

2020-01-23 12:21:47

* * *

안녕하세요

코딩연습생 입니다ㅠ 개발 블로그를 운영하면서 이것저것 많이 정보를 올리고 있는데

해보고자 하는 연습물이 잘 안풀려서 요즘 1일 1포스팅이 잘 안 이루어지고 있습니다ㅠ

대충 포스팅 글 올리기에 집중하기 보단 좀 더 정확한 정보를 업로드 하고자 늦어지는것입니다

이번 포스팅은 Deep Learning을 구현해 볼려고 하는데요

Deep Learning란?

\- 기계 학습 알고리즘의 집합(?)

이런식으로 표현을 하는거 같습니다 딥러닝이라는것은 컴퓨터 비전, 머신런닝, 음성인식, 신호처리등

모든 분야에서 기계 학습을 통한 훈련 기법 이다 라고 저는 생각합니다

딥러닝 기법을 사용하고자 할때 제일 많이 듣는 말이 텐서플로우(Tensorflow)인데요

그럼 텐서플로우는 또 뭐냐?

텐서플로우란?

\- 구글이 2011년에 개발을 시작하여 2015년에 오픈소스로 공개한 기계학습 라이브러리

2016년 알파고와 함께 관심이 높아진 컨퍼런스임

Python 언어로 되어 있는 텐서플로우는 다른 프로그래밍 언어들 연계하여

다양한 분야에 적용할 수 있음

뭐 인터넷에 이정도 포스팅 되어 있네요ㅎ

참 어렵습니다ㅎ

근데 이것을 왜 제가 하고 있는냐 단순합니다 기존 OpenCv를 통해 이미지 처리법을 공부하고

그 처리된 이미지를 통해 판독 시스템을 만들어볼 예정이거든요

근데 단순 판독이 아니라 시스템 자체 학습을 통해 신규 사물을 재정의하고 학습하면서

시스템에 보이는 이미지를 어떤 이미지라고 인식하는 프로그램을 만들려고 하다보니

이 영역까지 오게 되었습니다ㅎㅎ

그래서 어쨋든 핵심인 딥러닝을 구현하기 위해서는 텐서플로우가 필요하고 그 텐서플로우를 알려면

Python을 알아야한다는게 결론입니다

이래서 사설이 엄청 길어졌는데 이번 포스팅에서 윈도우에서 Python과 텐서플로우를 셋팅하는 방법을

포스팅 해볼려고 합니다

일단 윈도우에서 Python을 사용하기 위해 Anaconda라는 프로그램을 설치 할것입니다

1.Anaconda3 설치하기

\- 링크 주소를 통해 사이트에서 다운로드 받기

<https://www.anaconda.com/distribution/>

[ Anaconda Python/R Distribution - Free Download Anaconda Distribution is the
world's most popular Python data science platform. Download the free version
to access over 1500 data science packages and manage libraries and
dependencies with Conda. www.anaconda.com
](https://www.anaconda.com/distribution/)

\- 링크를 접속하신뒤에 Download 버튼 눌러 줍니다

![](/assets/images/deep_learning_anaconda3_tensorflow_사용하기/img.png)

\- 적용하실려는 PC의 OS타입 그리고 OS비트에 맞는 링크를 눌러 다운로드를 실행합니다

![](/assets/images/deep_learning_anaconda3_tensorflow_사용하기/img_1.png)

\- 다운 받은 실행 파일을 실행하여 설치를 진행해 주세요

![](/assets/images/deep_learning_anaconda3_tensorflow_사용하기/img_2.png)

\- 경로 지정이 나올때까지 다음(Next) 버튼을 눌러주세요

![](/assets/images/deep_learning_anaconda3_tensorflow_사용하기/img_3.png)
![](/assets/images/deep_learning_anaconda3_tensorflow_사용하기/img_4.png)
![](/assets/images/deep_learning_anaconda3_tensorflow_사용하기/img_5.png)

\- 경로 지정 부분이 나타나면 Default로 설치하셔도 되긴 합니다만

기본 경로에 있는 ProgramData 폴더는 숨김 폴더라 삭제할때 조금 귀찮아 질 수 있어서

저는 D:\에 Anaconda3라는 폴더로 지정하여 설치 하였습니다

![](/assets/images/deep_learning_anaconda3_tensorflow_사용하기/img_6.png)

![](/assets/images/deep_learning_anaconda3_tensorflow_사용하기/img_7.png)
![](/assets/images/deep_learning_anaconda3_tensorflow_사용하기/img_8.png)

\- 이렇게 설치가 완료 되어지면 시작 메뉴에서 다음 메뉴를 "관리자 권한으로 실행해 주세요"

![](/assets/images/deep_learning_anaconda3_tensorflow_사용하기/img_9.png)

\- 그러면 콘솔창이 하나 뜹니다 거기에 다음과 같으 명령어를 쳐주세요

    
    
    conda upgrade pip

\- 그 다음 pip 패키지 업데이트를 실행 합니다

    
    
    pip install upgrade

※다음과 같은 오류가 날수가 있는데 저의 경우 패스 했습니다

\- 다음은 텐서플로우 설치를 위한 가상환경을 만들어 줍니다

    
    
    conda create -n 임의이름지정 python=3.6

![](/assets/images/deep_learning_anaconda3_tensorflow_사용하기/img_10.png)

\- Proceed([y]/n)?이라고 물어보면 y를 눌러주고 엔터를 칩니다

![](/assets/images/deep_learning_anaconda3_tensorflow_사용하기/img_11.png)

\- 생성된 가상환경을 활성화 시켜 줍니다

    
    
    activate 지정된 임의 가상환경 이름

![](/assets/images/deep_learning_anaconda3_tensorflow_사용하기/img_12.png)

\- 이렇게 하면 다음과 같이 (base)가 가상환경 이름으로 변경이 됩니다

![](/assets/images/deep_learning_anaconda3_tensorflow_사용하기/img_13.png)

\- 그다음 텐서플로우를 설치 합니다

    
    
    pip install tensorflow

![](/assets/images/deep_learning_anaconda3_tensorflow_사용하기/img_14.png)

\- 설치가 모두 끝나고 나면 python을 실행 시켜줍니다

    
    
    python

![](/assets/images/deep_learning_anaconda3_tensorflow_사용하기/img_15.png)

\- 파이썬이 제대로 실행되는지 명령어를 칩니다

    
    
    import tensorflow as tf
    hello = tf.constant("hello, TensorFlow!")
    sess = tf.Session()
    print(sess.run(hello))

\- 그런데 다음과 같은 오류가 뜨실수 있습니다

(DLL load failed: 지정된 모듈을 찾을 수 없습니다)

![](/assets/images/deep_learning_anaconda3_tensorflow_사용하기/img_16.png)

\- AVX(Advanced Vector Extensions)를 지원하지 않는 CPU를 사용할 경우 다음과 같은 오류가 납니다

\- 이경우 텐서플로우를 다운그래이드 해줘야 합니다

    
    
    pip install tensorflow==1.5

![](/assets/images/deep_learning_anaconda3_tensorflow_사용하기/img_17.png)

\- 이렇게 다운그래이드를 실행한 다음에 다시 파이썬을 실행한뒤 명령어를 실행합니다

![](/assets/images/deep_learning_anaconda3_tensorflow_사용하기/img_18.png)

\- 이렇게 출력이 되면 정상적으로 텐서플로우를 파이썬에서 호출해서 사용된것입니다

  

#아나콘다 #python #파이썬 #deep learning #딥러닝 #tensorflow #텐서플로우 #anaconda3

