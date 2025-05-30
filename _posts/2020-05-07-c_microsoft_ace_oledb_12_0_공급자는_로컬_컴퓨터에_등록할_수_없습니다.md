---
title:  "[2020-05-07] - [C#] 'Microsoft.ACE.OLEDB.12.0' 공급자는 로컬 컴퓨터에 등록할 수 없습니다"
categories:
  - Blog
tags:
  - "Microsoft.ACE.OLEDB.12.0"
  - "OLEDB"
  - "엑셀"
last_modified_at: 2025-05-30T16:04:02+09:00
---

## [C#] 'Microsoft.ACE.OLEDB.12.0' 공급자는 로컬 컴퓨터에 등록할 수 없습니다

코딩정보/C#

2020-05-07 14:43:57

* * *

안녕하세요

코딩연습생입니다

C# Winform에서 oledb를 사용하여 엑셀 연동을 구현하실때 다음과 같은 오류가 간혹 나타납니다

이럴 경우 조치 할 수 있는 방법에 대해 포스팅 해보도록 하겠습니다

해결 방법은 Access 패키지 설치 입니다

1\. AccessRuntime 설치

\- <https://www.microsoft.com/en-us/download/details.aspx?id=39358>

[ Microsoft Access 2013 Runtime The Microsoft Access 2013 Runtime enables you
to distribute Access 2013 applications to users who do not have the full
version of Access 2013 installed on their computers. www.microsoft.com
](https://www.microsoft.com/en-us/download/details.aspx?id=39358)

해당 링크에서 다운로 받아 설치 합니다

2\. Microsoft Access Database Engine 2016 Redistributable 설치

\- <https://www.microsoft.com/en-us/download/details.aspx?id=54920>

[ Microsoft Access Database Engine 2016 Redistributable This download will
install a set of components that can be used to facilitate transfer of data
between Microsoft Office System files and non-Microsoft Office applications.
www.microsoft.com ](https://www.microsoft.com/en-
us/download/details.aspx?id=54920)

설치에는 별다른게 없이 다음 버튼만 누루면 설치가 완료 됩니다

설치 이후 컴퓨터 재부팅 후에 재실행 하시면 해당 오류가 해결 된 걸 보실 수 있습니다

![](/assets/images/c_microsoft_ace_oledb_12_0_공급자는_로컬_컴퓨터에_등록할_수_없습니다/img.png)

  

#Microsoft.ACE.OLEDB.12.0 #OLEDB 공급자 오류 #엑셀 연동 오류

