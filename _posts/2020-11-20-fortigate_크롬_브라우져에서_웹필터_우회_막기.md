---
categories:
  - 'Blog'
tags:
  - '웹필터'
  - '크롬'
  - '프록시'
  - '포티케이트(FortiGate)'
  - 'fortigate'
  - '크롬'
  - '웹필터'
last_modified_at: '2025-05-30T16:04:04+09:00'
title: '[2025-08-13] - Post'
excerpt: ''
layout: 'post'
lang: 'ko'
permalink: '/posts/2020-11-20-fortigate_크롬_브라우져에서_웹필터_우회_막기/'
alt_en: '/en/posts/2020-11-20-fortigate_크롬_브라우져에서_웹필터_우회_막기/'
---

<div class="lang-panel lang-ko" lang="ko">
## [FortiGate] 크롬 브라우져에서 웹필터 우회 막기

코딩정보/IT 프로그램

2020-11-20 10:56:39

* * *

안녕하세요~

코딩연습생입니다ㅎㅎㅎ

오늘은 역시 방화벽 장비인 포티게이트(FortiGate) 웹필터 정책에 관련된 포스팅 글 입니다

저번에 포티게이트(FortiGate) 웹필터 기능에 대해서 소개를 한 적이 있는데

<https://codingman.tistory.com/129>

[ [FortiGate] 방화벽에서 웹필터 정책 사용하기 안녕하세요~ 요즘 다시 잠잠해졌던 코로나가 붐이 되고 있는거 같네요ㅠ 이제 좀
지긋지긋한데 떨어져줬음 하네요ㅠ 이번 포스팅은 포티게이트(FortiGate) 방화벽 장비 기능 중 웹필터 정책을 사
codingman.tistory.com ](https://codingman.tistory.com/129)

운영을 하면서 버그(?) 같은것이 생겨서 기록 차원에서 포스팅을 하게 되었어요

웹필터 적용 이후에 익스플로러(IE) 브라우져에서 정상 작동하는것이 크롬 브라우져에서 우회가 되는 현상이

발견 되었어요

방화벽 업체에도 문의를 해보고 구글 검색도 해보았는데 딱히 정보가 안나와서 헤매던중에 혹시 프로시 타입의 문제

일수도 있겠다는 생각에 이것 저것 만져보다 해결 하게 되었는데

일단 증상부터 말씀드리면

포티게이트(FortiGate) 웹필터에 네이버 웹툰에 대한 URL을 등록했습니다

![](/assets/images/fortigate_크롬_브라우져에서_웹필터_우회_막기/img.png)

Simple 타입으로 하나 등록하였구요

![](/assets/images/fortigate_크롬_브라우져에서_웹필터_우회_막기/img_1.png)

와일드 카드 타입으로도 하나 등록하였습니다

이 상태에서 익스플로러(IE)에서 네이버 웹툰을 접속 시도 하면

![](/assets/images/fortigate_크롬_브라우져에서_웹필터_우회_막기/img_2.png)

이렇게 정상적으로 차단이 걸리고 있습니다

하지만 크롭에서 웹툰을 접속하면

![](/assets/images/fortigate_크롬_브라우져에서_웹필터_우회_막기/img_3.png)

당황스럽게도 접속이 되고 있습니다

방화벽 업체에 문의 해본 결과로는 프록시 타입의 도메인을 크롬에서는 별도 보호가 적용되어 방화벽에서 캣치를

잘 못하고 있는거 같다고 하는데요

![](/assets/images/fortigate_크롬_브라우져에서_웹필터_우회_막기/img.jpg)

로그를 보면 정상적으로 Blocked가 처리되고 있습니다

업체에서 말한 부분이 딱 이해가 되지는 않았지만 그럴수도 있기에 방화벽에서 프록시를 처리하도록 설정을 해보았습니다

![](/assets/images/fortigate_크롬_브라우져에서_웹필터_우회_막기/img_1.jpg)

시스템 -> 설정 -> System Operation Settings에서 검사 모드를 프록시로 변경해 주었습니다

결과적으로는 크롬에서 차단이 되었네요?

![](/assets/images/fortigate_크롬_브라우져에서_웹필터_우회_막기/img_4.png)

정말 업체의 말이 정답이었는지는 잘 모르겠습니다

하지만 이상 문제가 해결을 되어 보이는데 몇일간 모니터링을 해봐야 알 수 있을거 같아요

향후에 동일한 문제가 발생하였을때를 위해 기록 차원에서 이렇게 포스팅을 하게 되었는데

혹시 저와 같은 방화벽 장비를 사용하시는 분중에 같은 문제를 고민중이신 분이 있다면 해당 글을 보시고

해결 하셨으면 좋겠네요~

  

#웹필터 #크롬 브라우져 #프록시 설정 #포티케이트(FortiGate) #fortigate 501E 장비 #크롬 우회 방지 #웹필터 우회
방지


</div>
<div class="lang-panel lang-en" lang="en">
(*No embedded English lines found. Add translations later.*)

</div>
