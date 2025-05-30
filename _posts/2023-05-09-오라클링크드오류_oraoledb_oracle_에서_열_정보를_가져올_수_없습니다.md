---
title:  '[2023-05-09] - [오라클링크드오류]"OraOLEDB.Oracle"에서 열 정보를 가져올 수 없습니다.'
categories:
  - Blog
tags:
  - "오라클"
  - "MSSQL"
  - "링크드서버오류"
  - "OraOLEDB.Oracle"
  - '"OraOLEDB.Oracle"에'
  - '"OraOLEDB.Oracle"에서'
  - '"OraOLEDB.Oracle"에서'
last_modified_at: 2025-05-30T16:04:30+09:00
---

## [오라클링크드오류]"OraOLEDB.Oracle"에서 열 정보를 가져올 수 없습니다.

코딩정보/Oracle

2023-05-09 09:58:20

* * *

MSSQL에서 오라클 DB를 링크드 설정하여 OPENQUERY를 실행하였을 경우 다음과 같은 오류가 발생합니다

이때 해결 하기 위한 방법 입니다

오류는 아래와 같이 나타 날 수 있습니다

![](/assets/images/오라클링크드오류_oraoledb_oracle_에서_열_정보를_가져올_수_없습니다/img.png)

이런 오류가 발생하였을때 SQL Server 서버시의 시작 계정에 필요한 권한을 부여하여 해결 할 수 있습니다

![](/assets/images/오라클링크드오류_oraoledb_oracle_에서_열_정보를_가져올_수_없습니다/img_1.png)

위의 해결 방안을 설정한 뒤 오라클의 dllhost에 정상적으로 오라클이 올라 왔는지 확인 한다

확인 방법은 아래 명령 프롬프트를 사용함

![](/assets/images/오라클링크드오류_oraoledb_oracle_에서_열_정보를_가져올_수_없습니다/img_2.png)

위의 이미지 처럼 명령 프롬프트에 오라클 DLL이 정상적으로 나타난다면 SSMS에 접속하여 다시 OPENQUERY를

실행하면 해결된 모습을 볼 수 있습니다

감사합니다

  

#오라클 #MSSQL 링크드 #링크드서버오류 #OraOLEDB.Oracle #"OraOLEDB.Oracle"에 오류가 발생했습니다. 액세스가
거부되었습니다. #"OraOLEDB.Oracle"에서 필수 인터페이스("IID_IDBCreateCommand")를 가져올 수 없습니다.
#"OraOLEDB.Oracle"에서 열 정보를 가져올 수 없습니다.

