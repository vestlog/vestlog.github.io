---
categories:
  - 'Blog'
tags:
  - 'Mitsubishi'
  - '시뮬레이션'
  - 'c#'
  - 'PLC'
  - '미쯔비시'
  - 'MXComponent'
  - 'GX'
last_modified_at: '2025-05-30T16:03:54+09:00'
title: '[2025-08-13] - Post'
excerpt: ''
layout: 'post'
lang: 'ko'
permalink: '/posts/2019-06-12-c_mx_component_v4_설정_방법/'
alt_en: '/en/posts/2019-06-12-c_mx_component_v4_설정_방법/'
---

## [C#]MX Component V4 설정 방법

코딩정보/IT 프로그램

2019-06-12 07:55:04

* * *

안녕하세요.

코딩하는남자 입니다

이번에 게시하게 된 정보는 제조업에서 많이 사용하고 있는 미쯔비시 PLC에 대해

C#이라는 개발 프로그램으로 통신하는 방법을 작성해 보겠습니다

C#으로 PLC와 통신하는 방법은 여러가지가 있습니다

소켓 통신이라든지 시리얼 통신이라던지..

근데 왜 글자는 MX Component를 사용하는냐 이렇개 생각하실텐데요

간단합니다 소켓/시리얼 통신은 모든 PLC와 연결이 가능하고 앞서 말씀드린것과 같이 미쯔비시 PLC를 사용할 경우에

정말 간편하게 통신이 가능하기 때문인데요

내용을 확인하시고 편리하다 나랑 환경이 비슷하다라고 생각되시면 한번 시도해 보시기 바랍니다

1\. MX Component v4 64bit용 설치 파일을 설치 합니다

![](/assets/images/c_mx_component_v4_설정_방법/img.jpg)

2\. Communication Setup Utility 실행

![](/assets/images/c_mx_component_v4_설정_방법/img_1.jpg)

3\. Communication Setup Utility 실행 후 아래 그림과 같이 설정 후 Wizard 클릭

![](/assets/images/c_mx_component_v4_설정_방법/img_2.jpg)

4\. Wizard 버튼을 누룬후 Logical Station number를 다음과 같이 넣고 Next 버튼을 누름

![](/assets/images/c_mx_component_v4_설정_방법/img_3.jpg)

5\. PC Side 설정

![](/assets/images/c_mx_component_v4_설정_방법/img_4.jpg)

6\. Comment 입력 후 Finish 버튼

![](/assets/images/c_mx_component_v4_설정_방법/img_5.jpg)

7\. Step 4에서 입력한 Logical Station Number는 지금까지 설정한 PLC 연결 정보를

Mx Component에 PLC Port 번호로 지정한 것이다

이 PLC Port번호는 PC와 PLC를 연결하는 Port번호로 사용 된다.

확인 했으면 Exit를 눌러서 해당 프로그램을 종료한다

참고로 아래 그림에서 PC 모양을 클릭하면 설정한 내용을 다시 입력할 수 있다

![](/assets/images/c_mx_component_v4_설정_방법/img_6.jpg)

8\. PLC Monitor Utility 실행

![](/assets/images/c_mx_component_v4_설정_방법/img_7.jpg)

9\. 아까 Setp4에서 입력한 Logical Station Number이 보인다 그걸 선택한 후 OK를 누룬다

![](/assets/images/c_mx_component_v4_설정_방법/img_8.jpg)

10\. Gx Simulatior2를 실행한 뒤 OK를 누룬다

![](/assets/images/c_mx_component_v4_설정_방법/img_9.jpg)

11\. Set8를 실행하면 다음과 같은 그림이 나오면 성공이다

![](/assets/images/c_mx_component_v4_설정_방법/img_10.jpg)

이상 GX Works2의 시뮬레이션과 연동하기 위한 MX Component 설정 방법 입니다

  

#Mitsubishi #시뮬레이션 #c# #PLC #미쯔비시 #MXComponent #GX Works2

