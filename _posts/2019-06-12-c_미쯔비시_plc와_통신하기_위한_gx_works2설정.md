---
categories:
  - 'Blog'
tags:
  - '시뮬레이션'
  - 'c#'
  - 'PLC'
  - '미쯔비시'
  - 'GX'
last_modified_at: '2025-05-30T16:03:55+09:00'
title: '[2025-08-13] - Post'
excerpt: ''
layout: 'post'
lang: 'ko'
permalink: '/posts/2019-06-12-c_미쯔비시_plc와_통신하기_위한_gx_works2설정/'
alt_en: '/en/posts/2019-06-12-c_미쯔비시_plc와_통신하기_위한_gx_works2설정/'
---

<div class="lang-panel lang-ko" lang="ko">
## [C#] 미쯔비시 PLC와 통신하기 위한 GX Works2설정

코딩정보/C#

2019-06-12 08:56:40

* * *

안녕하세요

코딩하는남자의 코딩 연습생입니다

미쯔비시 PLC와 통신하기 위한 MX Componnent v4 설정방법에 대한 글을 게시햇었는데

GX Works2 시뮬레이션 환경 설정 방법에 대한 글이 없어 작성하게 되엇습니다

해당 글은 실제 미쯔비시 PLC가 없더라도 GX Works2의 시뮬레이션 환경을 통해

PLC의 환경을 구성해 줍니다

설정 방법은 아래를 참고해 주세요~

1\. GX WORKS2를 설치 한다

다운 받아서 다음 버튼을 통해 설치하면 되므로 설명은 생략

2\. GX WORKS2를 실행하고 New Project를 실행해서 기본 정보를 입력해서 OK 버튼을 누른다

![](/assets/images/c_미쯔비시_plc와_통신하기_위한_gx_works2설정/img.jpg)

간단한 Ladder 코드를 자것ㅇ하고 M0가 접점이 이고, D0가 랜덤하고 값을 입력하는 코드

![](/assets/images/c_미쯔비시_plc와_통신하기_위한_gx_works2설정/img_1.jpg)

3\. Ladder를 작성 한뒤 Debus > Start/Stop Simulation 클릭

![](/assets/images/c_미쯔비시_plc와_통신하기_위한_gx_works2설정/img_2.jpg)

4\. 시뮬레이션 가동 상태

처음 실행시 ERR 발생시 RESET 후 RUN 해야 함

![](/assets/images/c_미쯔비시_plc와_통신하기_위한_gx_works2설정/img_3.jpg)

5\. 시뮬레이션 정상 가동인 상태

![](/assets/images/c_미쯔비시_plc와_통신하기_위한_gx_works2설정/img_4.jpg)

  

#시뮬레이션 #c# #PLC #미쯔비시 #GX Works2


</div>
<div class="lang-panel lang-en" lang="en">
(*No embedded English lines found. Add translations later.*)

</div>
