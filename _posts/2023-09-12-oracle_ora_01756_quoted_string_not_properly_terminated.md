---
title:  "[2023-09-12] - [Oracle] ORA-01756 : quoted string not properly terminated"
categories:
  - Blog
tags:
  - "oracle"
  - "오라클"
  - "오류"
  - "작은"
  - "오라클오류"
  - "ORA-01756"
  - "단일인용부"
  - "인용부"
last_modified_at: 2025-05-30T16:04:30+09:00
---

## [Oracle] ORA-01756 : quoted string not properly terminated

코딩정보/Oracle

2023-09-12 11:02:55

* * *

안녕하세요

코딩하는남자 코남입니다

정말 정말 오랜만에 글을 쓰는듯해요..

개인적으로 이사도 하고..이직도하고..요 근래 참 많은 일들이 일어나고 있습니다ㅎㅎ

이번 포스팅은 프로그램단에서 오라클 쿼리를 날리실때 종종 만날수 있는 ORA 에러 코드 입니다

ORA-01756 : quoted string not properly terminated

ORA-01756 : 단일 인용부를 지정해 주십시오

![](/assets/images/oracle_ora_01756_quoted_string_not_properly_terminated/img.png)

오류 메세지의 형태는 오류 발생 위치에 따라 조금씩 다르게 보일 수 있습니다

저의 경우에는 C# 프로그램 내에서 쿼리에서 발생한 오류라 위와 같은 형태로 에러 메세지가 발생하였습니다

![](/assets/images/oracle_ora_01756_quoted_string_not_properly_terminated/img_1.png)

단일 인용부...이게 뭔말인지...

일단 모르면 구글링이 정답이죠??

![](/assets/images/oracle_ora_01756_quoted_string_not_properly_terminated/img_2.png)

역시 구글은 모르는게 없는듯 합니다..

제가 작성한 프로그램 내에 있는 쿼리문 중에 작은 따옴표가 누락이나 중복이 있다라는 얘기인데...

![](/assets/images/oracle_ora_01756_quoted_string_not_properly_terminated/img_3.png)

시작점의 작은따옴표가 누락되었네요..

참 알고 나면 별거 아닌데...찾는데 시간이 많이 걸렸습니다

저와 같이 ORA-01756 오류를 만나신 분들..프로그램안에서 작은 따옴표를 찾아보세요

그럼 이만~

  

#oracle #오라클 #오류 #작은 따옴표 #오라클오류 #ORA-01756 #단일인용부 #인용부

