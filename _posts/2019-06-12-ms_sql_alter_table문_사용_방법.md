---
categories:
  - 'Blog'
tags:
  - 'MSSQL'
  - 'query'
  - 'table'
  - 'alter'
  - 'alter'
last_modified_at: '2025-05-30T16:03:54+09:00'
title: '[2025-08-13] - Post'
excerpt: ''
layout: 'post'
lang: 'ko'
permalink: '/posts/2019-06-12-ms_sql_alter_table문_사용_방법/'
alt_en: '/en/posts/2019-06-12-ms_sql_alter_table문_사용_방법/'
---

<div class="lang-panel lang-ko" lang="ko">
## [MS-SQL] ALTER TABLE문 사용 방법

코딩정보/MS-SQL

2019-06-12 08:08:09

* * *

**1)****alter table A alter column name char(10) not null **

**\-- char(10) 은 기존 컬럼의 크기 그대로 설정**

**2)****alter table A alter column price money not null**

**=====================**

** 보라색 부분들은 필수 구문이고요 **

** 초록색 부분은 해당 테이블, 컬럼 명 넣는 부분**

** 파랑색부분은 타입 및 , null 설정 부분입니다.**

**> >> ALTER 명령어 정리 <<<<<**

**alter table 테이블명 add 컬럼명 타입 null설정 **

**> > 해당 컬럼을 해당 타입과 해당 null 설정으로 추가**

**alter table 테이블명 drop column 컬럼명 **

**> > 해당 컬럼 삭제**

**alter table 테이블명 alter column 컬럼명 타입 null설정 **

**> > 해당 컬럼을 해당 타입과 NULL 설정으로 변화**

  

#MSSQL #query #table #alter #alter table


</div>
<div class="lang-panel lang-en" lang="en">
(*No embedded English lines found. Add translations later.*)

</div>
