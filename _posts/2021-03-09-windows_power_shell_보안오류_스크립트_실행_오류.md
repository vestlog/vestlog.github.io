---
categories:
  - 'Blog'
tags:
  - '관리자'
  - 'unauthorizedAccess'
  - 'Power'
  - '보안'
  - 'PSSecurityException'
  - 'about_Execution_Policies'
last_modified_at: '2025-05-30T16:04:09+09:00'
title: '[2025-08-13] - Post'
excerpt: ''
layout: 'post'
lang: 'ko'
permalink: '/posts/2021-03-09-windows_power_shell_보안오류_스크립트_실행_오류/'
alt_en: '/en/posts/2021-03-09-windows_power_shell_보안오류_스크립트_실행_오류/'
---

## [Windows Power Shell] 보안오류(스크립트 실행 오류)

코딩정보/Windows

2021-03-09 07:58:14

* * *

안녕하세요.

코딩연습생입니다

요즘 회사 업무에 너무 시달리네요ㅎㅎ 회사 경기는 점점 안좋아진다고 하는데 왜 일은 계속 늘어날까요?ㅎㅎ

모든 직장인들의 고민이겠죠?ㅎ

이번 포스팅은 Windows Power Shell에서 ps1 확장자와 같은 파일을 실행시 듣보잡(?) 오류가 뜰때 해결 하는 방법

입니다

듣보잡(?) 오류는

\+ CategoryInfo : 보안 오류: (:) [], PSSecurityException  
\+ FullyQualifiedErrorId : UnauthorizedAccess

파일 실행시 이런 문구의 오류가 뜨는것이죠

이유는 대충 다들 이해 하실겁니다 접근 권한 문제겠죠...

근데 역시나 저는 컴퓨터가 아니라 금방 금방 까먹어서 블로그에 포스팅하여 후에 비슷한 문제가 발생하였을때

쉽게 해결하기 위해 남깁니다ㅎㅎ 물론 비슷한 문제에 봉착하신 분들이 이 글을 보고 쉽게 해결하면 더 좋구요~^^

■ 해결 방법

1\. Windows Power Shell을 관리자 권한으로 실행합니다

![](/assets/images/windows_power_shell_보안오류_스크립트_실행_오류/img.png)

2\. 실행 권한을 허용을 변경

\- 아래 스크립트를 캡쳐 화면과 같이 입력합니다

\- ExecutionPolicy

\- Set-ExecutionPolicy Unrestricted

![](/assets/images/windows_power_shell_보안오류_스크립트_실행_오류/img_1.png)

3\. 그리고 마지막 스크립트 파일 실행!!

\- 저는 파이썬 가상환경 실행 파일인 ps1 파일 실행시 접근 오류가 발생하였는데

이렇게 권한 해제를 하고 난뒤 아래 캡쳐와 같이 실행 되는것을 확인할 수 있습니다

![](/assets/images/windows_power_shell_보안오류_스크립트_실행_오류/img_2.png)

  

#관리자 권한 실행 #unauthorizedAccess #Power Shell 스크립트 실행 오류 #보안 오류
#PSSecurityException #about_Execution_Policies

