---
categories:
  - 'Blog'
tags:
  - '웹필터'
  - '보안정책'
  - '포티게이트(FortiGate)'
  - '포티가드(FortiGuard)'
  - '501E'
last_modified_at: '2025-05-30T16:04:04+09:00'
title: '[2025-08-13] - Post'
excerpt: ''
layout: 'post'
lang: 'ko'
permalink: '/posts/2020-11-19-fortigate_방화벽에서_웹필터_정책_사용하기/'
alt_en: '/en/posts/2020-11-19-fortigate_방화벽에서_웹필터_정책_사용하기/'
---

<div class="lang-panel lang-ko" lang="ko">
## [FortiGate] 방화벽에서 웹필터 정책 사용하기

코딩정보/IT 프로그램

2020-11-19 08:52:34

* * *

안녕하세요~ 요즘 다시 잠잠해졌던 코로나가 붐이 되고 있는거 같네요ㅠ

이제 좀 지긋지긋한데 떨어져줬음 하네요ㅠ

![](/assets/images/fortigate_방화벽에서_웹필터_정책_사용하기/img.png)

이번 포스팅은 포티게이트(FortiGate) 방화벽 장비 기능 중 웹필터 정책을 사용해서

유해 싸이트 차단 정책을 운영하는 기능 사용방법에 대해 포스팅 할려고 합니다

물론 사용제품이라 메뉴얼에 다 나와 있는거지만.. 저 처럼 기억력이 안좋은 사람은 기록하는 습관을 가져야 하기에

정보 공유 + 기록?? 차원에서 포스틍 합니다ㅎㅎㅎ

현재 제가 사용중인 포티게이트(FortiGate) 장비는 501E라는 장비 입니다

장비의 종류도 약간 차이가 있지만 관리자 콘솔의 펌웨어 버전에 따라 화면이 상이 할 수 있으니 참고하셔서

봐주셔야 할거 같습니다

현재 제가 사용하는 펌웨어의 버전은 v6.0.8입니다

대쉬보드 메인 화면은 이렇게 생겼죠

![](/assets/images/fortigate_방화벽에서_웹필터_정책_사용하기/img_1.png)

**※ 개인정보 영역은 일부러 가진것이니 특별한 정보는 없습니다**

이제 우리가 확인하고자 하는 메뉴를 선택해야겠죠?

![](/assets/images/fortigate_방화벽에서_웹필터_정책_사용하기/img_2.png)

Security Profiles -> Web Filter 메뉴로 들어가게 되면 위와 같은 화면이 나오게 됩니다

(여기서 펌웨어 버전에 따라 화면이 조금 다를수 있습니다)

웹필더(Web Filter)로 들어가게 되면 크게 두가지로 눈에 띄게 되는데

FortiGuard category based filter라는것이 있습니다

이건 포티게이트(FortiGate)에서 Keyword를 통해 패키지(?) 처럼 카테고리 형태로 정책을 운영할수 있게 만든

기능인데요

FortiGuard는 사용하고자 할 경우 라이센스가 필요합니다 즉, 상용이라는 말이죠

제가 운영하는 회사에서는 다행이 FortiGuard가 있는 라이센스를 보유 중이라 저렇게 활성화가 되어 있는데

만약에 FortiGuard 활성화가 없거나 안되신다면 라이센스를 확인해 보시기 바랍니다

이제 두번째로 확인할 것은 정척 URL 필터 입니다

저희가 유심히 지속적으로 쭉~~~ 관리해주어야 할 기능인거죠

차단하고자 하는 URL를 허용/Block/모니터링 기능을 주어서 개별 관리 할 수 있는 기능입니다

사용 방법은 간단합니다

![](/assets/images/fortigate_방화벽에서_웹필터_정책_사용하기/img_3.png)

생성 버튼을 눌러 줍니다

그러면 아래와 같은 팝업 창이 하나 띄게 되는데요

![](/assets/images/fortigate_방화벽에서_웹필터_정책_사용하기/img_4.png)

URL 부분에 도메인 주소를 입력합니다

그런데 타입별로 작성하는 방법이 조금 다릅니다

※ 네이버를 예를 들어서 설명 드리겠습니다

https://www.naver.com이라는 는 도메일이 있을 경우

Simple : naver.com만 기입

정규식표현 : <https://www.naver.com으로> 로 모두 기입

와일드카드 : *.naver.* 네이버라는 키워드(Keyword)가 들어가는 모든 관련 도메인을 관리

이렇게 사용하게 됩니다

두번째 동작은 별도로 설명하지 않을께요

이렇게 작성하신뒤 확은 버튼을 눌러줍니다

그럼 목록에 추가하신 도메인이 생성이 됩니다

![](/assets/images/fortigate_방화벽에서_웹필터_정책_사용하기/img_5.png)

저는 네이버 웹툰을 차단하였습니다

그다음 꼭!! 필수로 하단에 있는 적용 버튼을 눌러 주셔야 합니다

![](/assets/images/fortigate_방화벽에서_웹필터_정책_사용하기/img_6.png)

이 적용 버튼을 누루지 않고 화면을 이동하시게 되면 저장이 안되니 꼭 유의하시기 바랍니다

이상으로 포티게이트(FortiGate)에서 유해 사이트 차단 정책을 위한 웹필터 정책 사용법에 대한 포스팅을 마치도록

하겠습니다

  

#웹필터 #보안정책 #포티게이트(FortiGate) #포티가드(FortiGuard) #501E


</div>
<div class="lang-panel lang-en" lang="en">
(*No embedded English lines found. Add translations later.*)

</div>
