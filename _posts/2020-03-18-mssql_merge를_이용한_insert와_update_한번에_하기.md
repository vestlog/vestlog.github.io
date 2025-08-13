---
categories:
  - 'Blog'
tags:
  - 'Update'
  - 'MSSQL'
  - 'query'
  - 'insert'
  - 'merge'
  - 'INSERT와UPDATE를'
  - 'INSERT와'
last_modified_at: '2025-05-30T16:04:01+09:00'
title: '[2025-08-13] - Post'
excerpt: ''
layout: 'post'
lang: 'ko'
permalink: '/posts/2020-03-18-mssql_merge를_이용한_insert와_update_한번에_하기/'
alt_en: '/en/posts/2020-03-18-mssql_merge를_이용한_insert와_update_한번에_하기/'
---

## [MSSQL] MERGE를 이용한 INSERT와 UPDATE 한번에 하기

코딩정보/MS-SQL

2020-03-18 13:21:32

* * *

안녕하세요~ 코딩 연습생입니다

코로나 사태 여러분 괜찮으신가요??

언제쯤 잠잠해질지 참...얼른 백신이나 대책이 나왔으면 좋겠는데 마스크 때문에 숨도 잘 안쉬어지네요~

그래도 할건 해야겠죠?ㅎㅎ

그래서 저는 매일 출근합니다;;;ㅋ

오늘 포스팅 주제는 MSSQL 쿼리인데요

MSSQL을 접해보신 분들한데는 참 쉬운 정보일수 있지만 혹시 모르시는 분들을 위해서 포스팅 합니다

프로그램을 작성하다가 DB와 Data를 주고 받을때 이미 있는 데이터를 처리하기 위해서 SELECT를 한번 더 해야 하고

중복인지 아닌지를 체크해서 중복이면 UPDATE를 신규이면 INSERT 뭐 이런식으로 프로그램을 많이 했습니다

그런데 이 MERGE라는 함수를 알게 되고 부턴 한번의 쿼리로 INSERT / UPDATE가 조건에 의해 한번에 처리가 되니

참 편하더라구요

그래서 이 MERGE함수 사용하는 방법을 포스팅 하겠습니다

일단 쿼리 작성을 위해서 MSSQL을 접속합니다

접속을 하신뒤 새쿼리를 눌러 쿼리를 작성합니다

저의 경우 USER_MAST라는 테이블을 생성하였습니다

*USER_MAST 테이블

\- 컬럼정보 : USER_ID, USER_NAME, USER_PSWD

이렇게 3개의 컬럼이 존재합니다

그럼 조회를 한번 해보겠습니다

![](/assets/images/mssql_merge를_이용한_insert와_update_한번에_하기/img.jpg)

보시는거와 같이 USER_MAST라는 테이블에는 TEST라는 정보가 이미 존재하고 있습니다

그럼 MERGE 쿼리를 작성해 볼께요

*Query
    
    
    MERGE USER_MAST
          USING (SELECT 'x' AS DUAL) AS B
             ON [USER_ID] = 'TEST'
           WHEN MATCHED THEN
                UPDATE SET [USER_NAME] = 'TEST111111'
           WHEN NOT MATCHED THEN
                INSERT([USER_ID], [USER_NAME], USER_PSWD) VALUES('TEST', 'TEST', '');

쿼리의 내용을 말로 설명하자면 이렇게 됩니다

USER_MAST라는 테이블에 [USER_ID]가 'TEST'인 테이터가 존재하면

UPDATE문으로 [USER_NAME] 컬럼에 'TEST111111'을 UPDATE하고

존재하지 않으면 INSERT문으로 [USER_ID]가 'TEST'이고 [USER_NAME]가 'TEST'인 DATA를 생성해라

이렇게 됩니다 어렵지 않죠?

그럼 MERGE 쿼리를 실행해 보겠습니다

※ 아래 이미지는 USER_PSWD가 빠져있는데 쿼리 자체게 문제는 없습니다 참고하세요

![](/assets/images/mssql_merge를_이용한_insert와_update_한번에_하기/img_1.jpg)

실행했으면 USER_MAST 테이블을 다시 조해해보겠습니다

위에서 보았듯이 이미 USER_MAST 테이블에는 TEST라는 데이터가 존재했습니다

그래서 USER_NAME 컬럼에 TEST111111을 UPDATE한 결과를 확인 할 수 있습니다

![](/assets/images/mssql_merge를_이용한_insert와_update_한번에_하기/img_2.jpg)

그럼 다음 조건을 테스트하기 위해서 USER_MAST 테이블의 값을 지워 볼께요

![](/assets/images/mssql_merge를_이용한_insert와_update_한번에_하기/img_3.jpg)

DELETE문을 실행했습니다

![](/assets/images/mssql_merge를_이용한_insert와_update_한번에_하기/img_4.jpg)

이제 USER_MAST 테이블에는 'TEST'라는 데이터는 존재하지 않습니다

다시 MERGE문을 실행해 보겠습니다

![](/assets/images/mssql_merge를_이용한_insert와_update_한번에_하기/img_5.jpg)

그럼 저희는 예측할수가 있죠

USER_MAST 테이블에 USER_ID컬럼이 'TEST'이고 USER_NAME컬럼이 'TEST'인 데이터가 생성되어야 합니다

조회 해보겠습니다

![](/assets/images/mssql_merge를_이용한_insert와_update_한번에_하기/img_6.jpg)

예상했던 결과값이 보여지네요

이렇게 INSERT와 UPDATE를 하나의 쿼리에서 동작할 수 있는 방법을 알아봤습니다

  

#Update #MSSQL #query #insert #merge #INSERT와UPDATE를 한번에 #INSERT와 UPDATE 동시

