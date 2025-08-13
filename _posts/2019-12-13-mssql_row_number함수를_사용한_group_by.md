---
categories:
  - 'Blog'
tags:
  - 'MSSQL'
  - '쿼리'
  - 'ROW_NUMBER'
  - '중복제거'
  - 'GroupBy'
last_modified_at: '2025-05-30T16:03:56+09:00'
title: '[2025-08-13] - Post'
excerpt: ''
layout: 'post'
lang: 'ko'
permalink: '/posts/2019-12-13-mssql_row_number함수를_사용한_group_by/'
alt_en: '/en/posts/2019-12-13-mssql_row_number함수를_사용한_group_by/'
---

## [MSSQL] ROW_NUMBER함수를 사용한 GROUP BY

코딩정보/MS-SQL

2019-12-13 13:17:27

* * *

안녕하세요

코딩하는남자 코딩연습생입니다

MSSQL에서 ROW_NUMBER 함수를 이용해서 중복 데이터를 제외한 MAX의 데이만 추출 하는 방법을 설명

해볼려고 합니다

먼저 무정리된 ROW 데이터를 조회 해 볼꼐요

![](/assets/images/mssql_row_number함수를_사용한_group_by/img.jpg)

중요 정보는 흑백 처리 했습니다

이 조회된 데이터를 보시면 HOPPER_CART에 중복으로 많은 데이터가 있습니다

여기에 ROW_NUMBER 함수를 써서 HOPPER_CART의 데이터중에 HOPPRE_TIME의 값이 가장 높은것을이

나오도록 쿼리문 짜보겠습니다

    
    
    SELECT HOPPER_CODE, HOPPER_SEQ,
           HOPPER_CART, HOPPER_LOTNO,
           HOPPER_JAJIL, PCARD_NO, HOPPER_TIME
      FROM (
             SELECT HOPPER_CODE, HOPPER_SEQ,
           			HOPPER_CART, HOPPER_LOTNO,
           			HOPPER_JAJIL, PCARD_NO, HOPPER_TIME
               		ROW_NUMBER() OVER(PARTITION BY HOPPER_CODE ORDER BY HOPPER_SEQ DESC) AS ROWIDX
               FROM MIX_HOPPER_RFID_RESULT_TEMP WITH(NOLOCK)
           ) A
    WHERE ROWIDX = 1

자, 이렇게 쿼리문을 작성한뒤 조회를 하면

![](/assets/images/mssql_row_number함수를_사용한_group_by/img_1.jpg)

다음과 같은 결과 값이 나오네요

HOPPER_CART별 HOPPER_TIME가 가장 높은 값으로 조회가 됩니다

물론 GROUPBY를 서브쿼리로 짜서도 같은 결과값을 만들수 있지만 서브에 서브 쿼리를 많이 다는것보다

row_number() 함수를 활용해서 좀 간결한(?) 쿼리로 GROUP BY와 같은 효과를 나타낼수 있습니다

  

#MSSQL #쿼리 #ROW_NUMBER #중복제거 #GroupBy

