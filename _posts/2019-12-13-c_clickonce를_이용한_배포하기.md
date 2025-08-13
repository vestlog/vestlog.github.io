---
categories:
  - 'Blog'
tags:
  - '보안'
  - '웹사이트'
  - '폴더'
  - 'FTP'
  - '배포'
  - 'c#'
  - 'ClickOnce'
  - 'IIS'
  - '게시'
  - '클릭온스'
last_modified_at: '2025-05-30T16:03:56+09:00'
title: '[2025-08-13] - Post'
excerpt: ''
layout: 'post'
lang: 'ko'
permalink: '/posts/2019-12-13-c_clickonce를_이용한_배포하기/'
alt_en: '/en/posts/2019-12-13-c_clickonce를_이용한_배포하기/'
---

## [C#] ClickOnce를 이용한 배포하기

코딩정보/C#

2019-12-13 10:35:35

* * *

안녕하세요

코딩하는남자 코딩연습생입니다

이번 블로그글은 C#이나 C++등 비쥬얼 스튜디오를 이용하여 프로젝트 개발을 진행하고

배포하는 방법 중 하나인 ClickOnce 사용 방법을 다루어 볼까 합니다

많은 분들이 사용하고 계시는 방법인데 프로젝트 Source 관리도 편하고 배포 버전도 자동 관리를 해주니

정말 단점이 별로 없을 정도로 유용한 기능 중 하나 입니다

ClickOnce를 사용하기 위해서는 서버 IIS 기능과 FTP 기능을 사용해야 합니다

IIS서버가 존재한다는 가정에 설명을 하도록 하겠습니다

IIS서버 구축 방법은 서버 버전에 따라 많이 다르고 IIS 버전에 따라서도 많이 다르기 때문에

이번 시간에 IIS 서버 구축 방법까지 설명하기가 힘들거 같습니다

차후에 IIS 서버를 구축하게 될 일이 생기면 그때 자료를 모아서 포스팅 하도록 하겠습니다

[서버 설정]

1\. IIS 서버에 배포를 위한 웹사이트 등록하기

\- 사이트 항목에서 마우스 오른쪽 버튼을 클릭하여 웹 사이트 추가를 클릭

![](/assets/images/c_clickonce를_이용한_배포하기/img.jpg)

2\. 웹사이트 추가 정보 입력

\- 사이트 이름, 실제 경로 입력하고 확인

![](/assets/images/c_clickonce를_이용한_배포하기/img_1.jpg)

3\. IIS 웹서버 상세 설정 진행

\- IIS 웹서버 상세 설정에서 "디렉터리 검색" 부분을 사용안함에서 적용으로 상태 변경

![](/assets/images/c_clickonce를_이용한_배포하기/img_2.jpg)
![](/assets/images/c_clickonce를_이용한_배포하기/img_3.jpg)

4\. IIS서버 접속시 운영될 기본 문서 설정

\- IIS서버 상세 속성 설정에서 기본문서부분에 publish.htm 항목 추가

![](/assets/images/c_clickonce를_이용한_배포하기/img_4.jpg)

5\. IIS서버 접속 인증

\- 익명 인증 사용

![](/assets/images/c_clickonce를_이용한_배포하기/img_5.jpg)

6\. 생성한 IIS서버에 FTP게시 추가

\- 생성한 웹사이트 항목에서 마우스 오른쪽 버튼을 클릭하여 FTP 게시 추가 클릭

![](/assets/images/c_clickonce를_이용한_배포하기/img_6.jpg)

7\. FTP 서버 상세 설정에서 FTP 권한 부여 규칙 설정

\- 모든 사용자 읽기,쓰기 권한 부여

![](/assets/images/c_clickonce를_이용한_배포하기/img_7.jpg)

8\. FTP 서버 상세 설정에서 FTP 인증 규칙 설정

\- 기본인증 및 익명 인증 허용

![](/assets/images/c_clickonce를_이용한_배포하기/img_8.jpg)

9\. 서버 내 게시될 위치의 폴더 권한 수정

\- 웹사이트 등록시 실제 경로의 위치의 폴더에서 마우스 오른쪽 버튼 클릭하여 속성 클릭

![](/assets/images/c_clickonce를_이용한_배포하기/img_9.jpg)

10\. 폴더 속성에서 보안탭 클릭

![](/assets/images/c_clickonce를_이용한_배포하기/img_10.jpg)

11\. 폴더 속성의 보안탭에서 편집 클릭

![](/assets/images/c_clickonce를_이용한_배포하기/img_11.jpg)

12\. 폴더 사용권한에서 추가 버튼 클릭

![](/assets/images/c_clickonce를_이용한_배포하기/img_12.jpg)

13\. 사용자 또는 그룹 선택 화면에서 고급 항목 클릭

![](/assets/images/c_clickonce를_이용한_배포하기/img_13.jpg)

14\. 사용자 또는 그룹선택 고급 화면에서 지금찾기 버튼 클릭

![](/assets/images/c_clickonce를_이용한_배포하기/img_14.jpg)

15\. 검색된 사용자중에 다음 사용자를 추가

\- IIS_IUSRS, Users

![](/assets/images/c_clickonce를_이용한_배포하기/img_15.jpg)
![](/assets/images/c_clickonce를_이용한_배포하기/img_16.jpg)

16\. 비쥬얼스튜디오로 돌아와서 해당 프로젝트의 속성 보기

\- 솔루션 탐색기에서 프로젝트 항목에서 마우스 오른쪽 버튼을 클릭하여 속성 클릭

![](/assets/images/c_clickonce를_이용한_배포하기/img_17.jpg)

17\. 프로젝트 속성에서 서명 탭을 클릭하여 ClickOnce 매니페스트 서명 체크

![](/assets/images/c_clickonce를_이용한_배포하기/img_18.jpg)

18\. 프로젝트 속성에서 보안탭에서 ClickOnce 보안 설정 사용 체크 설정

![](/assets/images/c_clickonce를_이용한_배포하기/img_19.jpg)

19\. 프로젝트 속성 탭에서 게시 탭을 선택

\- 게시 위치 상단에 IIS서버에서 구축한 FTP 주소 입력

\- 게시 위치 하단에 IIS서버 주소 입력

\- 설치 모드 및 설정 상세 속성 설정

![](/assets/images/c_clickonce를_이용한_배포하기/img_20.jpg)

20\. 응용 프로그램 파일

\- 기본 빌드 구성의 배포 파일을 생성시켜 주므로 별도 설정은 하지 않음

21\. 필수 구성 요소

\- 개발 환경에서 닷넷 환경에 필요한 필수 S/W를 배포시 같이 배포 되도록 설정 할 수 있음

(저는 배포 환경에 맞지 않아 추가 구성 요소를 설정하지 않았습니다)

![](/assets/images/c_clickonce를_이용한_배포하기/img_21.jpg)

22\. 옵션 설정

\- 게시 옵션 화면에서 프로젝트 설명

(해당 부분의 정보는 배포시 웹사이트나 응용 프로그램 항목 명칭이 자동 생성되어 집니다

![](/assets/images/c_clickonce를_이용한_배포하기/img_22.jpg)

\- 게시 옵션의 배포 탭 설정

![](/assets/images/c_clickonce를_이용한_배포하기/img_23.jpg)

\- 게시 옵션 항목중 매니페스트 설정

(바탕화면 아이콘을 자동으로 설정할 수 있음)

![](/assets/images/c_clickonce를_이용한_배포하기/img_24.jpg)

23\. 마무리 단계 최종 배포 완료 이후 이렇게 웹사이트 화면으로 배포가 가능 합니다

![](/assets/images/c_clickonce를_이용한_배포하기/img_25.jpg)

다음과 같은 화면이 보이신다면 ClickOnce를 사용하여 배포에 성공하신 겁니다~

웹사이트에 보이는 설치 버튼 클릭 한번으로 제가 만든 응용프로그램이 자동 배포 됩니다ㅎㅎ

여기까지 보시는라 고생하셨습니다

앞으로 비쥬얼스튜디오를 사용하여 개발하였을 경우 Debug 폴더 뒤져서 배포 하지 마시고 ClickOnce를 사용해 보세요~

감사합니다

  

#보안 #웹사이트 #폴더 #FTP #배포 #c# #ClickOnce #IIS #게시 #클릭온스

