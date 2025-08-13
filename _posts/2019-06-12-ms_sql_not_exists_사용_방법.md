---
categories:
  - 'Blog'
tags:
  - 'MSSQL'
  - 'query'
  - '쿼리'
  - 'Exists'
  - 'NOT'
  - '조회조건'
last_modified_at: '2025-05-30T16:03:54+09:00'
title: '[2025-08-13] - Post'
excerpt: ''
layout: 'post'
lang: 'ko'
permalink: '/posts/2019-06-12-ms_sql_not_exists_사용_방법/'
alt_en: '/en/posts/2019-06-12-ms_sql_not_exists_사용_방법/'
---

<div class="lang-panel lang-ko" lang="ko">
## [MS-SQL] NOT EXISTS 사용 방법

코딩정보/MS-SQL

2019-06-12 08:04:51

* * *

테이블의 동일하지 않은 값만 조회하기 위한 조건문.

    
    
    SELECT * FROM AAAAAA
    
    WHERE NOT EXISTS(SELECT * FROM BBB WHERE AAA=BBB AND AAA=BBB)

  

#MSSQL #query #쿼리 #Exists #NOT EXISTS #조회조건


</div>
<div class="lang-panel lang-en" lang="en">
(*No embedded English lines found. Add translations later.*)

</div>
