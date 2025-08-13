---
categories:
  - 'Blog'
tags:
  - 'MSSQL'
  - '윈도우서버'
  - 'WindowsServer2012'
  - '특정프로그램차단'
last_modified_at: '2025-05-30T16:04:25+09:00'
title: '[2025-08-13] - Post'
excerpt: ''
layout: 'post'
lang: 'ko'
permalink: '/posts/2021-09-03-windows_server_2012_방화벽_설정으로_특정_ip_차단_설정/'
alt_en: '/en/posts/2021-09-03-windows_server_2012_방화벽_설정으로_특정_ip_차단_설정/'
---

## [Windows Server 2012] 방화벽 설정으로 특정 IP 차단 설정

코딩정보/Windows

2021-09-03 13:31:53

* * *

안녕하세요

코딩연습생입니다~

매일 주식 딥러닝 봇 구동만하고 직접 포스팅을 쓰는건 정말 오랜만이네요ㅎㅎ

자주 해야지 하면서도 잘 안되는게 포스팅인듯 합니다ㅎㅎㅎ

이번 포스팅에서 설명드릴것은 Windows Server에서 특정 IP를 차단하거나

특정 프로그램의 접근을 차단하고자 할때 정책 설정하는 방법인데요

간단한거 같으면서도 모르면 매우 어려운 그런거(?) 입니다ㅎㅎ

저의 경우 제 서버에 특정 IP에서 MSSQL 접근을 막고자 해서 알아본 내용을 포스팅 합니다

비슷한 정책을 설정하시고자 하실때 참고하셔서 응용하시면 좀 더 쉽게 적용 하실 수 있을거라 생각됩니다

그럼 첫번째로 Windows Server 서버의 방화벽 설정으로 갑니다

방화벽 설정 화면으로 들어가는 방법은

제어판에서 Windows 방화벽 아이콘을 클릭하면 됩니다

![](/assets/images/windows_server_2012_방화벽_설정으로_특정_ip_차단_설정/img.png)

두번째는 방화벽 정책을 활성화해야 합니다

![](/assets/images/windows_server_2012_방화벽_설정으로_특정_ip_차단_설정/img_1.png)
![](/assets/images/windows_server_2012_방화벽_설정으로_특정_ip_차단_설정/img_2.png)

이렇게 방화벽 정책을 활성화 해주고 이제 세부정책을 설정하러 가겠습니다

세번째는 고급설정입니다

![](/assets/images/windows_server_2012_방화벽_설정으로_특정_ip_차단_설정/img_3.png)

고급설정으로 들어가게 되면 이렇게 세부 정책을 설정할수 있게 되어 있는데

간단히 설명을 하면

인바운드 규칙 : 외부에서 안으로 들어오는 정책입니다

아웃바운드규칙 : 인바운드규칙과 반대로 안에서 밖으로 나가는 정책입니다

![](/assets/images/windows_server_2012_방화벽_설정으로_특정_ip_차단_설정/img_4.png)

제가 하고자 하는 것은 외부의 특정 PC에서 MSSQL 서버에 접근을 하지 못하도록 하고자 하는것이기에

저는 인바운드 규칙에 새로운 정책을 넣겠습니다

![](/assets/images/windows_server_2012_방화벽_설정으로_특정_ip_차단_설정/img_5.png)

인바운드 규칙에서 새규칙을 클릭 합니다

이름을 적어주고 작업에서 저는 차단을 선택하였습니다

![](/assets/images/windows_server_2012_방화벽_설정으로_특정_ip_차단_설정/img_6.png)

그리고 내 서버안에서 구동중인 MSSQL의 접속 포트는 기본 포트인 1433을 지정하겠습니다

![](/assets/images/windows_server_2012_방화벽_설정으로_특정_ip_차단_설정/img_7.png)

그다음 특정 IP의 접근만 차단하도록 설정해야겠죠

![](/assets/images/windows_server_2012_방화벽_설정으로_특정_ip_차단_설정/img_8.png)

영역 탭에서 원격 IP주소 부분에서 추가 버튼을 눌러 줍니다

![](/assets/images/windows_server_2012_방화벽_설정으로_특정_ip_차단_설정/img_9.png)

빨간색 테두리안에 차단하고자 하는 접근 PC의 IP 주소를 입력합니다

![](/assets/images/windows_server_2012_방화벽_설정으로_특정_ip_차단_설정/img_10.png)

최종적으로 이렇게 인바운드규칙에 새로운 규칙이 생성되었습니다

테스트를 진행해 보면 다음과 같이 MSSQL 접근이 차단이 됩니다

![](/assets/images/windows_server_2012_방화벽_설정으로_특정_ip_차단_설정/img_11.png)

  

#MSSQL 접근 차단 #윈도우서버 접근 차단 #WindowsServer2012 #특정프로그램차단

