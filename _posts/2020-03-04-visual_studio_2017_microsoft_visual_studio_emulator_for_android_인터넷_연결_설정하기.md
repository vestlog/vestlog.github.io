---
title:  "[2020-03-04] - [Visual Studio 2017] Microsoft Visual Studio Emulator for Android 인터넷 연결 설정하기"
categories:
  - Blog
tags:
  - "에뮬레이터"
  - "안드로이드"
  - "인터넷연결"
  - "인터넷연결안됨"
  - "Visual"
  - "ERR_SSL_PROTOCOL_ERROR"
  - "Webpage"
last_modified_at: 2025-05-30T16:04:00+09:00
---

## [Visual Studio 2017] Microsoft Visual Studio Emulator for Android 인터넷 연결
설정하기

코딩정보/Android

2020-03-04 09:30:34

* * *

안녕하세요 코딩 연습생입니다

블로그를 시작한지 3개월(?) 정도 되었는데 하루 한개의 포스팅이 이렇게 어려울수가 없습니다ㅠ

최대한 많이 올려볼려고 노력하는데 회사원으로써 기여도가 상당히 낮네요ㅎㅎ

주제선정 -> 내용 검색 -> 프로그램 구현 -> 화면 캡쳐 -> 내용 정리 -> 포스팅

이 순서로 블로그를 작성중인데 프로그램 구현에서 2~3일이 걸리네요ㅎㅎ

내가 지식과 능력이 부족한탓인듯 합니다ㅎ

자기 개발을 위해 쭉~~~ 운영 할 생각이니 이해해 주시길 바랍니다ㅎ

이번 포스팅은 저번 시간에 포스팅 했던 비쥬얼 스튜디오 2017에서 에뮬레이터를 설정하는 방법을

포스팅 했었는데요

<https://codingman.tistory.com/90>

[ [Visual Studio 2017] Microsoft Visual Studio Emulator for Android 설치 하기
안녕하세요 코딩 연습생입니다 이번 포스팅은 비쥬얼스튜디오2017을 이용하여 안드로이드 개발 환경을 구축하기 1단계 입니다 비쥬얼 스튜디오
2017에 에뮬레이터를 설치하여 안드로이드 개발환경을 만들어 보도록.. codingman.tistory.com
](https://codingman.tistory.com/90)

이번 시간에는 설정한 에뮬레이터에서 인터넷을 바로 사용할 수 있게 설정하는 방법을 포스팅 해볼려고 합니다

기본 에뮬레이터를 설정한 후 실행해서 인터넷 연결을 하시면 다음과 같은 화면이 나오실 꺼에요

![](/assets/images/visual_studio_2017_microsoft_visual_studio_emulator_for_android_인터넷_연결_설정하기/img.jpg)

인터넷 프로토콜이 없다는 말입니다

그러면 어떻게 해야 하는냐...그걸 이제 설명할려고 해요ㅎㅎ

차근 차근 해보시기 바랍니다

저는 윈도우10을 사용중이라서 캡쳐 내용이 윈도우10 위주로 설명되어 있으니 참고 하시기 바랍니다

1\. 제어판 열기

\- 윈도우10에서 검색을 통해 제어판을 열어 줍니다

![](/assets/images/visual_studio_2017_microsoft_visual_studio_emulator_for_android_인터넷_연결_설정하기/img_1.jpg)

2\. 제어판의 항목중 관리도구를 선택해 주세요

![](/assets/images/visual_studio_2017_microsoft_visual_studio_emulator_for_android_인터넷_연결_설정하기/img_2.jpg)

3\. 관리도구 항목 중 Hyper-V 관리자를 선택합니다

![](/assets/images/visual_studio_2017_microsoft_visual_studio_emulator_for_android_인터넷_연결_설정하기/img_3.jpg)

4\. Hyper-V 관리자에서 좌측 작업 항목중에서 가상 스위치 관리자를 클릭합니다

![](/assets/images/visual_studio_2017_microsoft_visual_studio_emulator_for_android_인터넷_연결_설정하기/img_4.jpg)

5\. 가상 스위치 관리자에서 스위치 유형을 외부로 선택한 후에 가상 스위치 만들기를 클릭 합니다

![](/assets/images/visual_studio_2017_microsoft_visual_studio_emulator_for_android_인터넷_연결_설정하기/img_5.jpg)

6\. 다시 Hyper-V 관리자에서 가상 컴퓨터에서 사용중인 에뮬레이터를 선택한 후 마우스 오른쪽 버튼을 클릭하면

세부 메뉴가 보입니다 그 리스트 중에서 설정을 클릭

![](/assets/images/visual_studio_2017_microsoft_visual_studio_emulator_for_android_인터넷_연결_설정하기/img_6.jpg)

7\. 설정 화면에서 하드웨어 추가 항목중 네트워크 어댑터를 클릭 후 추가 버튼을 눌러 어댑터를 추가 합니다

![](/assets/images/visual_studio_2017_microsoft_visual_studio_emulator_for_android_인터넷_연결_설정하기/img_7.jpg)

8\. 신규로 생성된 네트워크 어댑터를 클릭한 후에 가상 스위치를 5번에서 생성한 가상 스위츠를 선택한 뒤 적용 -> 확인

버튼을 클릭합니다

![](/assets/images/visual_studio_2017_microsoft_visual_studio_emulator_for_android_인터넷_연결_설정하기/img_8.jpg)

여기까지 설정하신뒤 다시 에뮬레이터를 실행한 뒤 인터넷을 확인해시면 다음과 같이 정상 연결이 됩니다

![](/assets/images/visual_studio_2017_microsoft_visual_studio_emulator_for_android_인터넷_연결_설정하기/img_9.jpg)

간단한 부분인데 모르면 어렵죠ㅎㅎ

감사합니다~

  

#에뮬레이터 #안드로이드 #인터넷연결 #인터넷연결안됨 #Visual Studio Emulator for Android
#ERR_SSL_PROTOCOL_ERROR #Webpage not available

