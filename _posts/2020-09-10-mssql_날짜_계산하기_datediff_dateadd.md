---
categories:
  - 'Blog'
tags:
  - '날짜계산'
  - 'DATEDIFF'
  - 'dateadd'
  - '일자계산'
  - 'mssql'
  - '일수'
last_modified_at: '2025-05-30T16:04:03+09:00'
title: '[2025-08-13] - Post'
excerpt: ''
layout: 'post'
lang: 'ko'
permalink: '/posts/2020-09-10-mssql_날짜_계산하기_datediff_dateadd/'
alt_en: '/en/posts/2020-09-10-mssql_날짜_계산하기_datediff_dateadd/'
---

<div class="lang-panel lang-ko" lang="ko">
## [MSSQL] 날짜 계산하기(datediff, dateadd)

코딩정보/MS-SQL

2020-09-10 07:39:06

* * *

안녕하세요~

코딩연습생입니다

MSSQL로 쿼리(Query)를 작성하실때 조회조건으로 가장 많이 사용되는것이 바로 날짜죠..

기간별 조회, 기간이후 조회, 등

그래서 이번 포스팅은 MSSQL에서 대표적인 날짜 계산 함수에 대해 간략히 소개해 드릴려고 합니다

![](/assets/images/mssql_날짜_계산하기_datediff_dateadd/img.png)

_**1\. Dateadd**_

\- dateadd 함수는 날짜를 더하거나 빼기를 할 수 있는 함수 입니다

예) 월의 마지막 날 구하기

→ **select dateadd(month, 1, getdate())-day(getdate())**

![](/assets/images/mssql_날짜_계산하기_datediff_dateadd/img_1.png)

1일 더하기

→ **select dateadd(day, 1, getdate())**

![](/assets/images/mssql_날짜_계산하기_datediff_dateadd/img_2.png)

1월 더하기

→ **select dateadd(month, 1, getdate())**

![](/assets/images/mssql_날짜_계산하기_datediff_dateadd/img_3.png)

1년 더하기

→ **select dateadd(year, 1, getdate())**

![](/assets/images/mssql_날짜_계산하기_datediff_dateadd/img_4.png)

_**2\. datediff**_

\- datediff 함수는 날짜와 날짜의 차이를 구하는 함수 입니다

예) 1일 차이(분) 구하기

→ **select datediff(mi, gatdate(), getdate()+1)**

: 1440분

![](/assets/images/mssql_날짜_계산하기_datediff_dateadd/img_5.png)

1일 차이(초) 구하기

→ **select datediff(s, getdate(), getdate()+1)**

: 86400초

![](/assets/images/mssql_날짜_계산하기_datediff_dateadd/img_6.png)

1일 차이(시간) 구하기

→ **select datediff(hour, getdate(), getdate()+1)**

: 24시간

![](/assets/images/mssql_날짜_계산하기_datediff_dateadd/img_7.png)

1일 차이(일자) 구하기

→ **select datediff(day, getdate(), getdate()+1)**

: 1일

![](/assets/images/mssql_날짜_계산하기_datediff_dateadd/img_8.png)

차이(월) 구하기

→ **select datediff(month, getdate(), getdate()+31)**

: 1 개월

![](/assets/images/mssql_날짜_계산하기_datediff_dateadd/img_9.png)

차이(년) 구하기

→ **select datediff(year, getdate(), getdate()+730)**

: 2년(730일)

![](/assets/images/mssql_날짜_계산하기_datediff_dateadd/img_10.png)

  

#날짜계산 #DATEDIFF #dateadd #일자계산 #mssql 날짜 조회 #일수 구하기


</div>
<div class="lang-panel lang-en" lang="en">
(*No embedded English lines found. Add translations later.*)

</div>
