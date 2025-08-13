---
categories:
  - 'Blog'
tags:
  - '윈도우서버2003'
  - 'db접근통제'
  - '방화벽'
  - 'WindowsServer2003'
  - '서버접근차단'
  - 'MSSQL'
last_modified_at: '2025-05-30T16:04:26+09:00'
title: '[2025-08-13] - Post'
excerpt: ''
layout: 'post'
lang: 'ko'
permalink: '/posts/2021-09-03-windows_server_2003_방화벽_설정으로_특정_ip_차단_설정/'
alt_en: '/en/posts/2021-09-03-windows_server_2003_방화벽_설정으로_특정_ip_차단_설정/'
---

## [Windows Server 2003] 방화벽 설정으로 특정 IP 차단 설정

코딩정보/Windows

2021-09-03 14:10:05

* * *

안녕하세요~

저번 포스팅에 이어서 이번에는 Windows Server 2003에서도 방화벽 설정을 통해서 특정 IP 접근을 차단하는

방법을 포스팅 해보도록 할께요

Windows Server 2012 버전 이상은 아래 링크를 통해 확인하실 수 있습니다

<https://codingman.tistory.com/328>

[ [Windows Server 2012] 방화벽 설정으로 특정 IP 차단 설정 안녕하세요 코딩연습생입니다~ 매일 주식 딥러닝 봇 구동만하고
직접 포스팅을 쓰는건 정말 오랜만이네요ㅎㅎ 자주 해야지 하면서도 잘 안되는게 포스팅인듯 합니다ㅎㅎㅎ 이번 포스팅에서 설
codingman.tistory.com ](https://codingman.tistory.com/328)

윈도우 버전에 따라 방화벽 UI가 다르고 정책 설정 방식이 달라서

이렇게 두가지 버전으로 나누어 포스팅하게 되었습니다

윈도우서버 2003의 경우 제어판에 있는 방화벽 메뉴에서는 접속 허용 정책만 설정이 가능하기 때문에

차단의 경우 다른 보안 설정을 통해 정책을 설정 하였습니다

*Windows Server 2003의 방화벽 설정 화면

![](/assets/images/windows_server_2003_방화벽_설정으로_특정_ip_차단_설정/img.png)

위의 이미지에서 보시는거와 같이 차단을 없고 추가만 있습니다

그래서 서버 2003의 경우에는 제어판이 아닌 관리도구로 갑니다

시작 -> 관리도구 -> 로컬 보안 정책

![](/assets/images/windows_server_2003_방화벽_설정으로_특정_ip_차단_설정/img_1.png)

로컬보안설정에서 IP 보안 정책(위치: 로컬 컴퓨터)의 항목을 클릭 합니다

![](/assets/images/windows_server_2003_방화벽_설정으로_특정_ip_차단_설정/img_2.png)

저의 경우에는 이미 만들어놓은 보안 정책이 존재하지만 보통 처음 접근하신 분들은 오른쪽 정책 부분이 빈공간으로

나오실 겁니다

그부분에서 마우스 오른쪽 버튼을 누루셔서 IP 보안 정책 만들기를 눌러주시면 됩니다

![](/assets/images/windows_server_2003_방화벽_설정으로_특정_ip_차단_설정/img_3.png)

그러면 IP 보안 정책 마법사가 나타나게 되고

다음 다음 다음을 통해서 신규 정책을 생성합니다

![](/assets/images/windows_server_2003_방화벽_설정으로_특정_ip_차단_설정/img_4.png)

다음

![](/assets/images/windows_server_2003_방화벽_설정으로_특정_ip_차단_설정/img_5.png)

이름 지정 후 다음

![](/assets/images/windows_server_2003_방화벽_설정으로_특정_ip_차단_설정/img_6.png)

다음

![](/assets/images/windows_server_2003_방화벽_설정으로_특정_ip_차단_설정/img_7.png)

마침을 후에 신규로 생성된 정책의 속성 창이 열리게 됩니다

![](/assets/images/windows_server_2003_방화벽_설정으로_특정_ip_차단_설정/img_8.png)

추가 버튼을 클릭하여 보안 규칙 마법사를 소환 합니다;;ㅎㅎ

![](/assets/images/windows_server_2003_방화벽_설정으로_특정_ip_차단_설정/img_9.png)

다음

![](/assets/images/windows_server_2003_방화벽_설정으로_특정_ip_차단_설정/img_10.png)

다음

![](/assets/images/windows_server_2003_방화벽_설정으로_특정_ip_차단_설정/img_11.png)

다음

![](/assets/images/windows_server_2003_방화벽_설정으로_특정_ip_차단_설정/img_12.png)

IP 필터 규칙을 추가 버튼을 통해 생성합니다

![](/assets/images/windows_server_2003_방화벽_설정으로_특정_ip_차단_설정/img_13.png)

이름을 지정하고 추가 버튼을 눌러 줍니다

네 그렇습니다...IP 필터 마법사를 또 소환했습니다

![](/assets/images/windows_server_2003_방화벽_설정으로_특정_ip_차단_설정/img_14.png)

다음

![](/assets/images/windows_server_2003_방화벽_설정으로_특정_ip_차단_설정/img_15.png)

다음

![](/assets/images/windows_server_2003_방화벽_설정으로_특정_ip_차단_설정/img_16.png)

원본 주소에 내 IP 주소를 선택하고 다음

![](/assets/images/windows_server_2003_방화벽_설정으로_특정_ip_차단_설정/img_17.png)

대상주소는 특정 IP 주소 또는 서브네트를 선택 후 밑에 나오는 주소란에 차단하고자 하는 PC의 IP를 입력

그리고 다음을 눌러 줍니다

![](/assets/images/windows_server_2003_방화벽_설정으로_특정_ip_차단_설정/img_18.png)

프로토콜 종류 선택에서는 TCP를 선택하고 다음을 눌러 줍니다

![](/assets/images/windows_server_2003_방화벽_설정으로_특정_ip_차단_설정/img_19.png)

이 포트에서 부분에 MSSQL 기본 포트인 1433을 걸도록 할께요

그리고 다음을 눌러 줍니다

![](/assets/images/windows_server_2003_방화벽_설정으로_특정_ip_차단_설정/img_20.png)

이제 IP 필터 마법사 마침을 눌러 소환 해제 시켜 줍니다

그러면 이렇게 IP 필터 목록에 방금 소환했던 정보가 나타 납니다

![](/assets/images/windows_server_2003_방화벽_설정으로_특정_ip_차단_설정/img_21.png)

정보를 확인 후에 확인 버튼을 눌러줍니다

마법사가 하나씩 해제될때마다 하나씩 생겨 납니다ㅎㅎ

IP 필터 목록에도 방금 생성한 규칙이 보이 실 겁니다

![](/assets/images/windows_server_2003_방화벽_설정으로_특정_ip_차단_설정/img_22.png)

동그라미 부분을 클릭 후 다음을 눌러 줍니다

다음은 동작을 설정해야 합니다

보통 처음 오시는 분들은 필터 동작 부분에 공백으로 보이실 텐데 추가 버튼을 눌러 생성하면 됩니다

![](/assets/images/windows_server_2003_방화벽_설정으로_특정_ip_차단_설정/img_23.png)

![](/assets/images/windows_server_2003_방화벽_설정으로_특정_ip_차단_설정/img_24.png)

다음

![](/assets/images/windows_server_2003_방화벽_설정으로_특정_ip_차단_설정/img_25.png)

동작 이름 입력 후 다음 버튼 클릭

![](/assets/images/windows_server_2003_방화벽_설정으로_특정_ip_차단_설정/img_26.png)

동작 선택 후 다음 버튼 클릭

![](/assets/images/windows_server_2003_방화벽_설정으로_특정_ip_차단_설정/img_27.png)

마침을 누루면 생성한 동작이 화면에 보이게 됩니다

![](/assets/images/windows_server_2003_방화벽_설정으로_특정_ip_차단_설정/img_28.png)

저는 접근을 차단할것이기 때문에 거부 동작을 선택 후 다음을 누루겠습니다

![](/assets/images/windows_server_2003_방화벽_설정으로_특정_ip_차단_설정/img_29.png)

마침 버튼을 눌러 신규로 생성한 보안 정책에 IP 필터 목록 세부 정책이 설정된 화면을 보실수 있습니다

![](/assets/images/windows_server_2003_방화벽_설정으로_특정_ip_차단_설정/img_30.png)

로컬보안정책에 생성된 정책을 선택하고 마우스 오른쪽 버튼을 클릭하여 해당 정착을 할당 상태로 변경합니다

![](/assets/images/windows_server_2003_방화벽_설정으로_특정_ip_차단_설정/img_31.png)

이후 차단등록한 IP에서 MSSQL 접근을 시도하면 다음과 같이 차단이 되게 됩니다

![](/assets/images/windows_server_2003_방화벽_설정으로_특정_ip_차단_설정/img_32.png)

  

#윈도우서버2003 #db접근통제 #방화벽 설정 #WindowsServer2003 #서버접근차단 #MSSQL 접근 통제

