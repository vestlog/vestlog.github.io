---
categories:
  - 'Blog'
tags:
  - '팁'
  - 'SQL'
  - '차이점'
  - 'MSSQL'
  - 'query'
  - 'VARCHAR'
  - 'nvarchar'
  - '소소한팁'
  - 'varchar와nvarchar의차이'
  - '초보sql'
last_modified_at: '2025-05-30T16:03:55+09:00'
title: '[2025-08-13] - Post'
excerpt: ''
layout: 'post'
lang: 'ko'
permalink: '/posts/2019-12-05-ms_sql_varchar과_nvarchar의_차이/'
alt_en: '/en/posts/2019-12-05-ms_sql_varchar과_nvarchar의_차이/'
---

## [MS-SQL] VARCHAR과 NVARCHAR의 차이??

코딩정보/MS-SQL

2019-12-05 07:42:33

* * *

안녕하세요

코딩하는 남자의 코딩연습생입니다

이번 중국 프로젝트를 진행하면서 알게된 내용입니다만 혹시 모르시는 분들이 계실까봐

한번 올려 봅니다ㅎㅎ

일반적으로 varcahr은 가변 문자열이라고 하고 nvarchar은 가변 유니코드 문자열이라고 하네요

그래서 프로그램 개발시에 다국어를 염두하고 있다면 MSSQL 연동시에 필드를 nvarchar를 사용해야 한다고 합니다

보통 영문이나 숫자는 1바이트이고 한글이나 중국 간체 등은 2바트로 구성되어지는데

varchar과 nvarchar의 차이가 바로 이 문자 저장 바이트 크기 차이 라고 합니다

소소하지만 저는 모르고 있었던 내용입니다ㅎ

아마 저와 같이 별거 아니지만 모르고 계셨던 분들은 이 블로그를 읽으시고 적용하시면

도움이 되지 않을까 싶습니다~

[테스트 Query 결과]

![](/assets/images/ms_sql_varchar과_nvarchar의_차이/img.jpg)

varchar(3)에 테스트라는 문자열을 넣었는데 길이가 1바이트 밖에 되지 않아 한자리만 출력되고 있습니다

그에 반면 nvarchar(3)은 3자리가 모두 출력되는 결과가 나오네요

무조껀 SQL 작성할때 저는 nvarchar을 사용하려고 합니다

  

#팁 #SQL #차이점 #MSSQL #query #VARCHAR #nvarchar #소소한팁 #varchar와nvarchar의차이
#초보sql

