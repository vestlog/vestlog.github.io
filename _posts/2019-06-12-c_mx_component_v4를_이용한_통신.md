---
categories:
  - 'Blog'
tags:
  - '통신'
  - 'c#'
  - 'PLC'
  - '미쯔비시'
  - '비쥬얼스튜디오'
  - '2017'
last_modified_at: '2025-05-30T16:03:55+09:00'
title: '[2025-08-13] - Post'
excerpt: ''
layout: 'post'
lang: 'ko'
permalink: '/posts/2019-06-12-c_mx_component_v4를_이용한_통신/'
alt_en: '/en/posts/2019-06-12-c_mx_component_v4를_이용한_통신/'
---

## [C#]MX Component V4를 이용한 통신

코딩정보/C#

2019-06-12 09:06:21

* * *

안녕하세요

코딩하는남자의 코딩연습생입니다

이번 블러그에서는 C#에서 MX Component V4의 API를 이용하여 PLC와 통신할 수 있는

설정 방법을 다뤄보겠습니다

1\. MX Conmpnent의 Communication Setup Utility를 이용해서 기본 셋팅 한다

필자가 작성한 게시글중 MX Componnent v4 설정 방법의 게시글을 참고

2\. GX Works2를 실행 및 새 프로젝트 생성해서 간단한 Ladder 코드를 작성하고 GX Simulator를 실행한다

Ladder코드는 검색을 통해 작성하시기 바란다.

3\. 비쥬얼스튜디오 2017를 실행해서 프조게트를 생성한다

C#이든 WPF든 생성한다

![](/assets/images/c_mx_component_v4를_이용한_통신/img.jpg)

4, 비쥬얼 스튜디오에 MX Component의 설치 경로에 있는 DLL 파일을 참조 추가 한다

[ActEther.dll](ActEther.dll) 은 이더넷 카드를 통해서 LAN선으로 연결하고자 할 사용 가능하다. 다만 설정할 것들이
좀 있다

[ActPcUsb.dll은](ActPcUsb.dll은) CPU의 USB Port를 통해서 PLC에 접근하고자 할 때 사용할 수 있다

[ActUtlType.dll은](ActUtlType.dll은) Step1에서 설정한 내용을 기준으로 PLC에 접근이 가능하도록 해준다

![](/assets/images/c_mx_component_v4를_이용한_통신/img_1.jpg)
![](/assets/images/c_mx_component_v4를_이용한_통신/img_2.jpg)

5\. 비쥬얼 스튜디오 디자인을 다음과 같이 간단하게 한다

![](/assets/images/c_mx_component_v4를_이용한_통신/img_3.jpg)

6\. 비쥬얼 스튜디오에서 소스를 입력한다

![](/assets/images/c_mx_component_v4를_이용한_통신/img_4.jpg)
![](/assets/images/c_mx_component_v4를_이용한_통신/img_5.jpg)
![](/assets/images/c_mx_component_v4를_이용한_통신/img_6.jpg)
![](/assets/images/c_mx_component_v4를_이용한_통신/img_7.jpg)

소스코드까지 입력하고 난뒤에 프로젝트를 실행한뒤 Logical station number 부분에 MX Component V4에서 설정한

station number를 입력한뒤 connect 버튼을 클릭하게 되면 우측 상단의 Connected : 부분에 현재의 PLC의 상태 값이

표시된다

정상적으로 표시가 된다면 연결에 성공하신것이다

  

#통신 #c# #PLC #미쯔비시 #비쥬얼스튜디오 #2017

