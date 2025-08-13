---
categories:
  - 'Blog'
tags:
  - '패킷분석'
  - '포티게이트(FortiGate)'
  - '포티가드(FortiGuard)'
  - '웹사이트차단'
  - 'URL확인'
last_modified_at: '2025-05-30T16:04:04+09:00'
title: '[2025-08-13] - Post'
excerpt: ''
layout: 'post'
lang: 'ko'
permalink: '/posts/2020-12-02-fortigate_fortiguard_예외_관리_방법/'
alt_en: '/en/posts/2020-12-02-fortigate_fortiguard_예외_관리_방법/'
---

<div class="lang-panel lang-ko" lang="ko">
## [FortiGate] FortiGuard 예외 관리 방법

코딩정보/IT 프로그램

2020-12-02 10:56:25

* * *

안녕하세요

코로나 확진자가 일일 400~500명이 나오고있네요ㅠ

잠잠해 지나 했는데 다시 시작인듯 합니다 정말 헉~! 이네요

![](/assets/images/fortigate_fortiguard_예외_관리_방법/img.png)

이번 포스팅은 포티케이트(FortiGate) 방화벽에서 웹필터(WebFilter) 기능 중에 하나인 포티가드(FortiGuard)의

카테고리(Category)에 의한 차단시 예외 처리 하는 방법에 대해 포스팅 하고자 합니다

아마 이미 많은 분들이 알고 계시는 정보라 생각하지만 저와 같은 분들이 분명 계실꺼라 생각되어

이렇게 포스팅 하는것이니 아시는 분들은 뒤로가기를 눌러오시면 됩니다^^

<https://codingman.tistory.com/129?category=762039>

[ [FortiGate] 방화벽에서 웹필터 정책 사용하기 안녕하세요~ 요즘 다시 잠잠해졌던 코로나가 붐이 되고 있는거 같네요ㅠ 이제 좀
지긋지긋한데 떨어져줬음 하네요ㅠ 이번 포스팅은 포티게이트(FortiGate) 방화벽 장비 기능 중 웹필터 정책을 사
codingman.tistory.com ](https://codingman.tistory.com/129?category=762039)

이전 포스팅에서 웹필터(WebFilter) 기능 사용 방법에 대해 작성했었는데 혹시 어떤 기능을 얘기하는 것인지?

이해가 잘 안되시는 분들은 위의 링크를 통해 한번 보시고 오시면 이해가 좀 쉽지 않을까 싶습니다

포트가드(FortiGuard)는 방대한 웹사이트를 일일이 필터 처리가 어려운것에 대한 포티게이트의 기능 중에 하나인데요

이미 수집된 웹사이트 URL에 대한 카테고리를 지정해 놓고 간단한 아이콘 선택으로 차단/허용/모니터링 관리를

가능하도록 만든 방화벽의 기능입니다

포티게이트(FortiGate)에서 포티가드(FortiGuard) 설정 위치는 아래 이미지와 같습니다

▶ Security Profiles -> Web Filter -> FortiGuard category based filter

![](/assets/images/fortigate_fortiguard_예외_관리_방법/img.jpg)

저는 예시로 쇼핑 카테고리를 사용해 볼려고 합니다

(포티가드에서 쇼핑 카테고리를 차단으로 설정한 뒤 네이버 사이트를 접속해보았습니다)

![](/assets/images/fortigate_fortiguard_예외_관리_방법/img_1.jpg)

이렇게 포티가드(FortiGuard)에서 쇼핑 카테고리를 차단으로 설정.

그뒤 네이버 쇼핑을 접속하면 아래와 같이 블럭 메세지가 나타납니다

![](/assets/images/fortigate_fortiguard_예외_관리_방법/img_2.jpg)

포티가드(FortiGuard)의 쇼핑 카테고리에 의해 차단된 정보를 확인 할 수 있습니다

이제 고정되어 있는 사용자 설정이 불가능한 포티가드(FortiGuard)에서 네이버 쇼핑을 예외 처리 해 보도록 할꼐요

(해당 예시는 Internet Explorer 11 버전을 사용하였습니다)

익스플로러에서 단축키 F12를 누루면 아래와 같은 화면이 나옵니다

여기서 네이버 쇼핑을 눌렀을때 어는 URL 또는 어는 단계에서 차단이 걸리는지 확인 할 수 있습니다

![](/assets/images/fortigate_fortiguard_예외_관리_방법/img_3.jpg)

네이버 쇼핑 버튼을 클릭했을때 쇼핑 URL이 403 에러가 발생하면서 차단이 되는 것을 확인 할 수 있습니다

![](/assets/images/fortigate_fortiguard_예외_관리_방법/img_4.jpg)

문제 위치에서 마우스 오른쪽 버튼을 클릭하여 URL 복사를 눌러 차단 되는 시점의 URL을 복사 합니다

![](/assets/images/fortigate_fortiguard_예외_관리_방법/img_5.jpg)

그 다음 포티가드(FortiGuard)의 쇼핑 카테고리 중 네이버 쇼핑을 예외 처리 하는 위치로 이동

▶ Security Prifiles -> Web 평가 관리자 수동 설정(Override) 메뉴로 이동

메뉴 이동한뒤 상단에 위치한 새로생성 버튼을 클릭 합니다

![](/assets/images/fortigate_fortiguard_예외_관리_방법/img_6.jpg)

아래와 같이 URL 위치에 복사한 URL을 입력하고 범주와 카테고리를 설정합니다

저는 custom1이라는 카테고리에 네이버 쇼핑을 예외로 입력하고 cutom1이라는 카테고리를 허용으로 정책 설정을

하였습니다

![](/assets/images/fortigate_fortiguard_예외_관리_방법/img_7.jpg)

이렇게 설정을 마친후 다시 익스플로러를 열어 네이버 쇼핑을 접속 시도 해보겠습니다

아래와 같이 기존 차단 되었던 403에러가 사라지면서 네이버 쇼핑이 접속되는 것을 확인 할 수 있는데요

웹 차단 정책을 시행할때 방대한 웹사이트를 모두 차단하기 어렵기 때문에 포티가드(FortiGuard) 기능을 사용해

카테고리별 관리 후 예외 사이트별 관리를 진행하면 좀 더 관리자가 수월할 거라고 생각됩니다

![](/assets/images/fortigate_fortiguard_예외_관리_방법/img_8.jpg)

  

#패킷분석 #포티게이트(FortiGate) #포티가드(FortiGuard) #웹사이트차단 #URL확인


</div>
<div class="lang-panel lang-en" lang="en">
(*No embedded English lines found. Add translations later.*)

</div>
