---
categories:
  - 'Blog'
tags:
  - '부트캠프'
  - '윈도우10'
  - '윈도우10'
  - '외장하드윈도우설치'
  - '외장하드디스크부팅'
last_modified_at: '2025-05-30T16:04:00+09:00'
title: '[2025-08-13] - Post'
excerpt: ''
layout: 'post'
lang: 'ko'
permalink: '/posts/2020-02-14-bootcamp_외장하드_usb_에_윈도우10_설치하기/'
alt_en: '/en/posts/2020-02-14-bootcamp_외장하드_usb_에_윈도우10_설치하기/'
---

## [BootCamp] 외장하드(USB)에 윈도우10 설치하기

코딩정보/BootCamp

2020-02-14 09:11:48

* * *

안녕하세요

IT 관련 정보와 C# 개발 관련 포스팅을 하고 있는 코딩연습생입니다

제가 포스팅용 및 개발 업무용으로 사용하고 있는 맥북에어(2015)가 하드디시크(SSD512)를 장착 중인데

개발 관련 프로그램 및 이것저것(?) 사용하면 용량이 많은거 같으면서도 항상 부족하더라구요

하나의 하드디스크에 두개의 OS를 넣어 사용할려니 문제가 있는것 같고

예전에 페럴러즈 설치 하는 방법을 포스팅한 적이 있는데요

<https://codingman.tistory.com/31>

[ [패럴러즈] 맥북으로 윈도우 사용하기 #1 안녕하세요. 코딩하는남자의 주인장 코딩연습생입니다~ 참 이쁘고 좋은 맥북... 근데 한국에서는
참 사용하기 불편하죠.. 저도 맥북에어를 가지고 있는데요 사실 맥북에어로 뭘 할려고 해도 윈도우가 필요하더라구..
codingman.tistory.com ](https://codingman.tistory.com/31)

장단점 분석해서 포스팅을 했었는데 퍼포먼스쪽 부분에서 어려움이 있더라구요

특히 개발할때 외부기기 연결을 할때 제한을 많이 받습니다 페럴러즈는...

그래서 이곳저곳 검색을 통해서 알게된 별도의 외장하드디스크에 윈도우10을 설치하고 부트캠프를 통해

맥북에서 돌아갈수 있게 만드는 과정을 포스팅할려고 합니다

환경 구성을 하기 위해서는 몇가지 준비물이 필요합니다

첫번째는 당연히 윈도우10 ISO 파일입니다

마이크로소프트 공식홈에서 받으셔도 되지만 저는 안정성이 확인된 빌드버전을 사용할려고 이전 릴리즈 싸이트

에서 다운로드 받겠습니다

<https://tb.rg-adguard.net/public.php>

[ TechBench by WZT (v4.1.1) This website was created with simplicity in mind.
Here you can easily download products directly from Microsoft. This website
neither its author are not affiliated with Microsoft Corporation. tb.rg-
adguard.net ](https://tb.rg-adguard.net/public.php)

해당 링크 싸이트로 이동하시면 다음과 같은 화면이 나오게 됩니다

![](/assets/images/bootcamp_외장하드_usb_에_윈도우10_설치하기/img.png)

유형, 버전, 에디션, 언어, 아키텍처를 선택해야 하는데요

*저는 1803 - Redstone 4를 사용했습니다

아래와 같이 선택하시면 우측에 다운로드 버튼이 나오게 되면 눌러주시면 다운로드 됩니다

![](/assets/images/bootcamp_외장하드_usb_에_윈도우10_설치하기/img_1.png)

이렇게 윈도우10 ISO 파일을 다운로드 합니다

두번째는 FUFUS가 필요합니다 외장하드를 하드디스크 처럼 사용할 수 있게 타입을 변경해주는 소프트웨어 입니다

아래 링크로 이동합니다

<https://rufus.ie/>

[ Rufus rufus.ie ](https://rufus.ie/)

싸이트에 접속해서 다음 링크를 클릭하여 다운로드 받아 줍니다

![](/assets/images/bootcamp_외장하드_usb_에_윈도우10_설치하기/img_2.png)

이렇게 RUFUS까지 다운로드를 받으면 준비물은 끝입니다

![](/assets/images/bootcamp_외장하드_usb_에_윈도우10_설치하기/img_3.png)

그럼 이제 본격적으로 제작을 한번 해보도록 하겠습니다

1\. rufus를 실행합니다

\- 고급 드라이브 속성 숨기기를 활성화한 뒤 USB 하드 드라이브 목록을 체그 해 줍니다

![](/assets/images/bootcamp_외장하드_usb_에_윈도우10_설치하기/img_4.png)

2\. 선택 버튼을 클릭하여 윈도우10 ISO 파일을 선택

![](/assets/images/bootcamp_외장하드_usb_에_윈도우10_설치하기/img_5.png)

3\. 이미지 옵션과 볼륨 레이블 명칭 변경

![](/assets/images/bootcamp_외장하드_usb_에_윈도우10_설치하기/img_6.png)

4\. 시작 버튼을 클릭하여 윈도우 버전 선택

![](/assets/images/bootcamp_외장하드_usb_에_윈도우10_설치하기/img_7.png)

5\. 외장 하드 드라이브 포맷 진행

\- * 모든 파일이 삭제 되니 주의 하시기 바랍니다

![](/assets/images/bootcamp_외장하드_usb_에_윈도우10_설치하기/img_8.png)

* 제가 사용하는 하드디스크는 이미 한번 rufus를 사용한 하드 디스크라 다음과 같은 화면이 하나 더 나오는데

그냥 확인을 눌러 줍니다

![](/assets/images/bootcamp_외장하드_usb_에_윈도우10_설치하기/img_9.png)

6\. 외장 하드 디스크에 설치 진행

![](/assets/images/bootcamp_외장하드_usb_에_윈도우10_설치하기/img_10.png)

7\. 외장하드를 USB에 꽃고 부팅시켜 줍니다

\- 맥북 부팅 화면을 캡쳐 할 수 없어서 글로 설명 드립니다

\- USB를 꽃고 전원키를 누루고 맥북의 Option키를 꾹~~~ 누구고 계시면 아래와 같은 화면이 나옵니다

![](/assets/images/bootcamp_외장하드_usb_에_윈도우10_설치하기/img_11.png)

\- 이상태에서 EFI Boot를 마우스로 선택후 control 버턴을 눌러주면 위쪽의 화살표가 회전하는 화살표로 변경됩니다

\- 그다음 enter를 누루시면 부팅이 되면서 윈도우 설치 화면이 뜹니다

8\. 윈도우 설치 진행은 생략하겠습니다

\- 요즘은 누구나 다 설치 할수 있다고 생각하고....

9\. 부팅이 완료되어 지면 부트캠프에서 다운로드 받은 파일을 C 드라이브에 Copy 한뒤 실행 합니다

![](/assets/images/bootcamp_외장하드_usb_에_윈도우10_설치하기/img_12.png)

10\. 드라이브를 모두 설치하게 되면 외장하드로 윈도우10를 사용하실수 있습니다~

  

#부트캠프 #윈도우10 #윈도우10 설치 #외장하드윈도우설치 #외장하드디스크부팅

