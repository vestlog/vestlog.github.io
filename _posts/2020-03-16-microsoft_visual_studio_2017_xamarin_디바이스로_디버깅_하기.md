---
categories:
  - 'Blog'
tags:
  - '안드로이드'
  - '디버깅'
  - '비쥬얼스튜디오'
  - '앱개발'
  - '개발자옵션'
  - '디바이스디버깅'
  - '휴대폰빌드'
  - '내휴대폰으로앱실행하기'
last_modified_at: '2025-05-30T16:04:01+09:00'
title: '[2025-08-13] - Post'
excerpt: ''
layout: 'post'
lang: 'ko'
permalink: '/posts/2020-03-16-microsoft_visual_studio_2017_xamarin_디바이스로_디버깅_하기/'
alt_en: '/en/posts/2020-03-16-microsoft_visual_studio_2017_xamarin_디바이스로_디버깅_하기/'
---

<div class="lang-panel lang-ko" lang="ko">
## [Microsoft Visual Studio 2017] Xamarin 디바이스로 디버깅 하기

코딩정보/Android

2020-03-16 15:07:54

* * *

안녕하세요

코딩연습생입니다

요즘 코로나 때문에 난리도 아니죠?ㅠ 제 주변에도 온통 관심사가 코로나에 가있습니다

이런 시국에 회사에서는 왜이렇게 일을 많이 주는걸까요....참 이해하기 힘든...ㅋㅋ

이번 포스팅은 요즘 안드로이드 공부 중에 에뮬레이터를 사용하다보니 속도도 느리고 버그(?)도 많이 생기느듯해서

폭풍 검색을 해서 찾아낸 방법인데요

바로 USB를 꽃아서 직접 내 안드로이드 폰에서 직접 디버깅을 하는 방법입니다

에뮬레이터랑 비교해 봤을때 속도면에서 빠르고 배포 테스트도 한번에 되는거 같아서 정말 편한거 같습니다

해당 방법을 적용하기 위해서는 내가 사용할려는 핸드폰 기종에 따라 조금 다릅니다

저의 경우 삼성 폰을 사용중이기 때문에 삼성폰을 위주로 설명을 할테니 다른 기종을 사용하시는분들은

참고해서 비슷하게 적용하시면 될거 같습니다

1\. 핸드폰 USB 드라이브 설치

\- 통합 USB 드라이브 설치하기 삼성 통합 툴입니다

<http://local.sec.samsung.com/comLocal/support/down/kies_main.do?kind=usb >

[ http://local.sec.samsung.com/comLocal/support/down/kies_main.do?kind=usb%20
local.sec.samsung.com
](http://local.sec.samsung.com/comLocal/support/down/kies_main.do?kind=usb%20)

2\. 핸드폰 설정 변경

\- 설정 메뉴로 들어가 줍니다

\- 테마 종류에 따라 아이콘을 다르겠지만 보통 메뉴에 설정이 있습니다

![](/assets/images/microsoft_visual_studio_2017_xamarin_디바이스로_디버깅_하기/img.jpg)

\- 설정 메뉴에 들어가면 맨 아래쪽에 휴대전화 정보라는것이 있습니다

![](/assets/images/microsoft_visual_studio_2017_xamarin_디바이스로_디버깅_하기/img_1.jpg)

\- 휴대전화 정보안에 보시면 소프트웨어 정보라는것이 또 있습니다 클릭해 주세요

![](/assets/images/microsoft_visual_studio_2017_xamarin_디바이스로_디버깅_하기/img_2.jpg)

\- 소프트웨어 정보 중 빌드번호 부분을 연속으로 클릭해 주시면 아래 작은 글씨로 문구가 뜨면서

개발자 모드가 활성화 됩니다

![](/assets/images/microsoft_visual_studio_2017_xamarin_디바이스로_디버깅_하기/img_3.jpg)

\- 다시 설정 화면으로 들어가시면 맨 아래쪽에 아래와 같이 개발자 옵션이라는 메뉴가 생기셧을 겁니다

클릭해서 들어가 주세요

![](/assets/images/microsoft_visual_studio_2017_xamarin_디바이스로_디버깅_하기/img_4.jpg)

\- 개발자 옵션에 들어가시면 쭉~ 밑으로 내리시면 USB디버깅 체크박스를 활성화 상태로 만들어 주시면

핸드폰 설정이 완료됩니다

![](/assets/images/microsoft_visual_studio_2017_xamarin_디바이스로_디버깅_하기/img_5.jpg)

3\. 비쥬얼스튜디오 실행

\- 위의 휴대폰 설정이 완료되셨다면 USB 연결을 한뒤에 비쥬얼스튜디오를 실행하시면

해당 프로젝트의 실행 아이콘이 아래와 같이 핸드폰 기종 명칭으로 변경 될것입니다

이 상태에서 클릭하시면 자동으로 USB에 연결된 휴대폰으로 배포되어지고 비쥬얼스튜디오와 연결된 상태에서

앱이 실행되어 디버깅이 가능합니다

![](/assets/images/microsoft_visual_studio_2017_xamarin_디바이스로_디버깅_하기/img_6.jpg)

저사양 PC로 앱을 개발하고 계신분이시라면 바로 실행 해 보세요ㅎㅎ

  

#안드로이드 #디버깅 #비쥬얼스튜디오 #앱개발 #개발자옵션 #디바이스디버깅 #휴대폰빌드 #내휴대폰으로앱실행하기


</div>
<div class="lang-panel lang-en" lang="en">
(*No embedded English lines found. Add translations later.*)

</div>
