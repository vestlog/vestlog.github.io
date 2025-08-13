---
categories:
  - 'Blog'
tags:
  - '클라이언트'
  - 'VPN'
  - '방화벽'
  - 'SSL'
  - 'fortigate'
  - 'FortiClient'
  - 'VPN'
last_modified_at: '2025-05-30T16:03:57+09:00'
title: '[2025-08-13] - Post'
excerpt: ''
layout: 'post'
lang: 'ko'
permalink: '/posts/2020-01-02-네트워크_forticlient_설치_하기/'
alt_en: '/en/posts/2020-01-02-네트워크_forticlient_설치_하기/'
---

## [네트워크] FortiClient 설치 하기

코딩정보/IT 프로그램

2020-01-02 22:31:13

* * *

[ FortiClientVPNOnlineInstaller_6.2.zip 0.34MB
](./file/FortiClientVPNOnlineInstaller_6.2.zip)

안녕하세요

코딩연습생입니다

이번 포스팅은 FortiGate의 VPN, SSL 접속을 위한 FortiClient 설치 방법을 포스팅 해보겠습니다

다운로드 받아 그냥 설치만 하면 되는거긴 한데 FortiGate가 외국회사라 그런지 주소가 간혹 기억이 안나는 경우가

있어서 포스팅 하게 되었습니다

일단 FortiClient 다운로드 주소는

<https://www.forticlient.com/downloads>

[ Forticlient - Next Generation Endpoint Protection Get FortiClient 6.0 for
Linux Ubuntu 16.04 or higher Red Hat, CentOS 7.4 or higher Info
www.forticlient.com ](https://www.forticlient.com/downloads)

혹시 싸이트 접속이 안되시는 분들은 6.2 버전을 업로드 했으니 다운로드 받으시면 될거 같습니다

[ FortiClientVPNOnlineInstaller_6.2.zip 0.34MB
](./file/FortiClientVPNOnlineInstaller_6_1.2)

[설치 방법]

1.위의 싸이트 or 업로드 파일을 다운로드 받는다

\- 싸이트를 통해 다운로드 할 경우 싸이트 접속 후 해당 링크 클릭

![](/assets/images/네트워크_forticlient_설치_하기/img.jpg)

2\. FortiClientVPNOnlineInstaller_6.2 파일 실행 하기

![](/assets/images/네트워크_forticlient_설치_하기/img_1.jpg)
![](/assets/images/네트워크_forticlient_설치_하기/img_2.jpg)

3\. 다음을 통한 설치 이어하기

\- Yes, I have read and accept the 체크 한 후 다음

![](/assets/images/네트워크_forticlient_설치_하기/img_3.jpg)

4\. 다음...다음...

![](/assets/images/네트워크_forticlient_설치_하기/img_4.jpg)

5\. 설치...설치...

![](/assets/images/네트워크_forticlient_설치_하기/img_5.jpg)

6\. 설치...설치...

![](/assets/images/네트워크_forticlient_설치_하기/img_6.jpg)

7\. 완료 후 바탕화면 아이콘 실행

![](/assets/images/네트워크_forticlient_설치_하기/img_7.jpg)

8\. FortiClient 초기 설정 화면

\- 연결이름 : 명칭

\- 설명 : 명칭에 대한 설명

\- 원격 게이트웨이 : FortiGate 접속 IP 번호

(기본 포트번호가 아닐 경우 사용자 정의 포트번호 체크박스 클릭 후 변경)

\- 모두 작성 한 후 저장

![](/assets/images/네트워크_forticlient_설치_하기/img_8.jpg)

9\. 정상 로그인 창

\- VPN이름 : 초기 설정창에서 지정한 명칭

\- 사용자 아이디, 비밀번호 입력후 "연결" 클릭시 VPN 연결

![](/assets/images/네트워크_forticlient_설치_하기/img_9.jpg)

  

#클라이언트 #VPN #방화벽 #SSL #fortigate #FortiClient VPN #VPN 클라이언트

