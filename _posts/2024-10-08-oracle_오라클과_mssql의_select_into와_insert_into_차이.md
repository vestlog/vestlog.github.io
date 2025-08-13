---
categories:
  - 'Blog'
tags:
  - 'mssql'
  - '오라클과'
  - '오라클'
  - '오라클'
  - 'mssql'
  - '오라클'
  - 'mssql'
last_modified_at: '2025-05-30T16:04:30+09:00'
title: '[2025-08-13] - Post'
excerpt: ''
layout: 'post'
lang: 'ko'
permalink: '/posts/2024-10-08-oracle_오라클과_mssql의_select_into와_insert_into_차이/'
alt_en: '/en/posts/2024-10-08-oracle_오라클과_mssql의_select_into와_insert_into_차이/'
---

## [ORACLE]오라클과 MSSQL의 SELECT INTO와 INSERT INTO 차이

코딩정보/Oracle

2024-10-08 09:00:58

* * *

안녕하세요.

정말 오랜만에 블로그를 작성하는것 같습니다

IT 종사자로써 가끔 혼동 되거나 기억을 까먹게 되는 부분이 오라클과 MSSQL의 쿼리 형태가 조금씩 다르다는 점이

어렵게 느껴질때가 있습니다

그 부분을 해결하기 위해 블로그에 요약하여 정리해 봅니다

*Chat GPT 피셜 

데이터베이스 관리 시스템(DBMS)인 오라클(Oracle)과 MSSQL(SQL Server)은 SQL 표준을 따르지만, 특정 구문이나 기능에

있어 약간의 차이가 있습니다. 그 중 SELECT INTO와 INSERT INTO 구문은 두 DBMS 간에 차이가 있는 대표적인 예입니다.

이 글에서는 오라클과 MSSQL에서 SELECT INTO와 INSERT INTO 구문이 어떻게 다른지, 각각의 사용 예제와 함께

설명하겠습니다.

### **1\. SELECT INTO 구문**

#### **1.1. MSSQL의 SELECT INTO**

MSSQL에서 SELECT INTO 구문은 **새로운 테이블을 생성** 하고, 다른 테이블이나 쿼리 결과의 데이터를 그 테이블에 삽입하는 데
사용됩니다. 즉, 기존 테이블이 아닌 **새로운 테이블을 만들면서 데이터를 복사** 하는 것입니다.

![](/assets/images/oracle_오라클과_mssql의_select_into와_insert_into_차이/img.png)
![](/assets/images/oracle_오라클과_mssql의_select_into와_insert_into_차이/img_1.png)

위 예제에서는 EmployeeTable에서 나이(age)가 30보다 큰 직원의 이름(name)과 나이(age)를 **새로운 테이블** 인
NewEmployeeTable에 저장합니다.

#### **1.2. 오라클의 SELECT INTO**

오라클에서는 SELECT INTO 구문이 MSSQL과는 **완전히 다른 목적** 으로 사용됩니다. 오라클에서 SELECT INTO는
**PL/SQL 블록 안에서 변수에 값을 할당** 할 때 사용됩니다. 오라클의 SELECT INTO는 **새로운 테이블을 생성** 하는 것이
아니라, **쿼리 결과를 변수에 저장** 하기 위한 구문입니다.

![](/assets/images/oracle_오라클과_mssql의_select_into와_insert_into_차이/img_2.png)

위 예제는 EmployeeTable에서 employee_id가 101인 직원의 이름(name)과 나이(age)를 PL/SQL 변수
v_name과 v_age에 저장하고 출력하는 예입니다.

### **2\. INSERT INTO 구문**

#### **2.1. MSSQL의 INSERT INTO**

MSSQL에서 INSERT INTO 구문은 **기존 테이블에 새로운 데이터를 삽입** 하는 데 사용됩니다. 이때 데이터는 **값을 직접
지정** 하거나 **다른 테이블에서 조회된 결과** 를 삽입할 수 있습니다.

![](/assets/images/oracle_오라클과_mssql의_select_into와_insert_into_차이/img_3.png)

#### **2.2. 오라클의 INSERT INTO**

오라클에서의 INSERT INTO 구문도 MSSQL과 비슷한 방식으로 동작합니다. 오라클 역시 **기존 테이블에 데이터를 삽입** 하는데
사용되며, 값을 직접 지정하거나 다른 테이블에서 데이터를 조회하여 삽입할 수 있습니다.

![](/assets/images/oracle_오라클과_mssql의_select_into와_insert_into_차이/img_4.png)

### **차이점 요약**

MSSQL오라클

**SELECT INTO** | 새로운 테이블을 생성하고 데이터를 삽입 | 쿼리 결과를 변수에 저장 (PL/SQL에서 사용)  
---|---|---  
**INSERT INTO** | 기존 테이블에 데이터를 삽입 (값 직접 지정 또는 SELECT 결과 삽입) | 기존 테이블에 데이터를 삽입 (값 직접 지정 또는 SELECT 결과 삽입)  
  
### **결론**

  * **MSSQL** 에서는 SELECT INTO를 사용하여 **새로운 테이블을 생성** 하고 데이터를 삽입할 수 있으며, 오라클에서의 INSERT INTO와 거의 동일한 구문을 가집니다.
  * 반면, **오라클** 에서는 SELECT INTO가 **변수에 값을 저장하는 기능** 으로 사용되며, 새로운 테이블을 생성하는 기능은 제공되지 않습니다. 대신 데이터를 삽입하는 작업은 **INSERT INTO** 구문을 사용하여 처리합니다.

따라서 MSSQL과 오라클에서 동일한 목적의 작업을 수행하려면 구문이 약간 다르기 때문에, 각 DBMS의 문법 차이를 이해하고 적절히
사용해야 합니다.

  

#mssql SELECT INTO #오라클과 mssql 차이점 #오라클 select into #오라클 insert into #mssql
insert into #오라클 예시 #mssql 예시

