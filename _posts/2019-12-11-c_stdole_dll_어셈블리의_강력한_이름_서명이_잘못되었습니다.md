---
categories:
  - 'Blog'
tags:
  - '오류'
  - '배포'
  - 'ClickOnce'
  - '코딩'
  - '생활코딩'
  - '코딩교육'
  - '코딩배우기'
  - '코딩프로그램'
  - 'stdole.dll'
last_modified_at: '2025-05-30T16:03:55+09:00'
title: '[2025-08-13] - Post'
excerpt: ''
layout: 'post'
lang: 'ko'
permalink: '/posts/2019-12-11-c_stdole_dll_어셈블리의_강력한_이름_서명이_잘못되었습니다/'
alt_en: '/en/posts/2019-12-11-c_stdole_dll_어셈블리의_강력한_이름_서명이_잘못되었습니다/'
---

<div class="lang-panel lang-ko" lang="ko">
## [C#] stdole.dll 어셈블리의 강력한 이름 서명이 잘못되었습니다.

코딩정보/C#

2019-12-11 13:51:54

* * *

안녕하세요.

코딩하는남자의 코딩연습생입니다

C#을 통해서 PPT 자동 슬라이드 프로그램을 구현하고 ClickOnce를 사용하여 배포 할려고 하는데

응용 프로그램을 시작할 수 없습니다??

![](/assets/images/c_stdole_dll_어셈블리의_강력한_이름_서명이_잘못되었습니다/img.jpg)

읭?? 뭐가 잘못됏지??

처음에는 프로그램상 오류가 있어서 그런건가 의심해서 코드 부분을 열심히 살펴 보았는데

아무 문제가 없고 로컬에서 실행을 하니 아주 잘 되더라구요

그래서 자세히(D)...를 눌러서 오류 내용을 확인 해봤어요

![](/assets/images/c_stdole_dll_어셈블리의_강력한_이름_서명이_잘못되었습니다/img_1.jpg)

"[stdole.dll](stdole.dll) 어셈블리의 강력한 이름 서명이 잘못되었습니다."

이런 오류의 종류로 에러가 난것을 확인한 뒤 바로 모든걸 알고 있을거 같은 구글님에게 폭풍 검색 시작...

![](/assets/images/c_stdole_dll_어셈블리의_강력한_이름_서명이_잘못되었습니다/img_2.jpg)

와~ 저와 비슷한 분들이 상당히 많은거 같더라구요 검색량이 엄청 났습니다

그중에 제일 위의 검색 내용을 확인해 보니

<https://underbar332.tistory.com/m/13>

[ Visual Studio 2013 설치후 stdole.dll 서명에러 VS2010으로 작업했던 작업의 업데이트를 위해서 배포를 했더니
(ClickOnce) 다운로드 완료후 실행시 자꾸 " stdole.dll 어셈블리의 강력한 이름 서명이 잘못되었습니다." 라는 메세지로
업데이트가 안되는 현상이.. underbar332.tistory.com ](https://underbar332.tistory.com/13)

이런 글이 있더라구요

결국 결론은 stdole.dll을 교채 했다는 내용은데...

제가 만든 프로그램을 배포 댓수가 20대 가량 되는데 그곳의 모든 PC의 stdole.dll을 교체하는건

참 귀찮고 하기 싫은 일이라서 저는 생각을 좀 바꾸엇습니다

제 프로젝트의 참고 내용중 stdole.dll을 삭제 한 후에 배포 해보자!

근데 생각의외로 좋은 결과가 나왔습니다

![](/assets/images/c_stdole_dll_어셈블리의_강력한_이름_서명이_잘못되었습니다/img_3.jpg)

이렇게 참조 내용중 stdole.dll을 삭제시킨 후 재 게시 진행

![](/assets/images/c_stdole_dll_어셈블리의_강력한_이름_서명이_잘못되었습니다/img_4.jpg)

재 설치 이후 정상 설치가 되면서 아주 잘 실행이 되엇습니다

저와 같이 ClickOnce 배포후에 "[stdole.dll](stdole.dll) 어셈블리의 강력한 이름 서명이 잘못되었습니다." 같은
에러로

당황하신분들은 링크 페이지의 내용처럼 시도 해보시거나 혹은 저처럼 참조 배포를 변경한뒤 재배포 시도를

해보시기 바랍니다~

감사합니다^^

  

#오류 #배포 #ClickOnce #코딩 #생활코딩 #코딩교육 #코딩배우기 #코딩프로그램 #stdole.dll


</div>
<div class="lang-panel lang-en" lang="en">
(*No embedded English lines found. Add translations later.*)

</div>
