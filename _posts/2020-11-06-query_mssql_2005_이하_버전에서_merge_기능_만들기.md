---
categories:
  - 'Blog'
tags:
  - 'mssql'
  - 'MSSQL'
  - '2005'
last_modified_at: '2025-05-30T16:04:04+09:00'
title: '[2025-08-13] - Post'
excerpt: ''
layout: 'post'
lang: 'ko'
permalink: '/posts/2020-11-06-query_mssql_2005_이하_버전에서_merge_기능_만들기/'
alt_en: '/en/posts/2020-11-06-query_mssql_2005_이하_버전에서_merge_기능_만들기/'
---

## [Query]MSSQL 2005 이하 버전에서 Merge 기능 만들기.

코딩정보/MS-SQL

2020-11-06 07:35:06

* * *

안녕하세요.

코딩연습생입니다~

요즘 블로그 글쓰기에 많이 소홀해 진거 같습니다ㅠ

그래도 전에는 주에 하나는 꼭 쓴거 같은데...이제는 뭐..월에 하나 쓸까 말까 네요ㅠ

컨텐츠 선정의 어려움도 문제고... 회사에서 감당하기 어려울 정도의 업무량을 짧은 기간에 적용하길 원하고..

여기서 치이고 저기서 치이고ㅋㅋㅋ 넉두리 시간이였습니다ㅎ

이번 포스팅 글에서는 예전 MSSQL MERGE기능을 통해 한번에 INSERT와 UPDATE를 하는 구문 쿼리를

포스팅 했었는데요

<https://codingman.tistory.com/98?category=715730>

[ [MSSQL] MERGE를 이용한 INSERT와 UPDATE 한번에 하기 안녕하세요~ 코딩 연습생입니다 코로나 사태 여러분
괜찮으신가요?? 언제쯤 잠잠해질지 참...얼른 백신이나 대책이 나왔으면 좋겠는데 마스크 때문에 숨도 잘 안쉬어지네요~ 그래도 할건 해야겠
codingman.tistory.com ](https://codingman.tistory.com/98?category=715730)

그런데 이 MERGE라는 기능이 MSSQL 2005이상의 버전에서만 지원이 가능합니다

물론 요즘은 2005 이하 버전을 잘 사용하지는 않치만 옛날 시스템을 운영 중이거나 할 경우에는 난감하게 되죠

그래서 MERGE문과 동일한 기능을 할수 있는 구조의 쿼리를 알려 드리겠습니다

    
    
    UPDATE 테이블명
       SET 컬럼 = 값
     WHERE 조건컬럼= 조건값

업데이트의 기본 형식입니다

프로시져나 쿼리에서 다음과 같이 업데이트문을 작성하고 밑에

    
    
    IF @@ROWCOUNT = 0
    BEGIN
    	INSERT INTO 테이블명
        (테이블에 사용할 컬럼명)
        VALUES
        (컬럼에 삽입할려는 값)
    END

@@ROWCOUNT 구분을 붙여주고 업데이트의 결과 값이 0이면 INSERT문이 돌아가게 하면

프로시져 운영할떄 한번에 UPDATE와 INSERT를 동작 시킬수 있습니다

[전체 쿼리]

    
    
    UPDATE 테이블명
       SET 컬럼 = 값
     WHERE 조건컬럼= 조건값
     
     IF @@ROWCOUNT = 0
     BEGIN
     	INSERT INTO 테이블명
        (테이블 컬럼 정의)
        VALUES
        (컬럼별 등록 값)
     END

  

#mssql merge #MSSQL ROWCOUNT #2005 MERGE기능

