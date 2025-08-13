---
categories:
  - 'Blog'
tags:
  - 'python'
  - '파이썬'
  - 'python'
  - 'mssql'
  - '파이썬'
last_modified_at: '2025-05-30T16:04:03+09:00'
title: '[2025-08-13] - Post'
excerpt: ''
layout: 'post'
lang: 'ko'
permalink: '/posts/2020-08-13-파이썬_pymssql를_활용한_mssql_db_데이터_조회/'
alt_en: '/en/posts/2020-08-13-파이썬_pymssql를_활용한_mssql_db_데이터_조회/'
---

## [파이썬] pymssql를 활용한 MSSQL DB 데이터 조회

코딩정보/Python

2020-08-13 10:53:20

* * *

안녕하세요

코딩연습생입니다~ㅎ

이번 포스팅은 제목에서 언급한것 처럼 Python에서 pymssql을 사용한 mssql DB 데이터를 Select하는 방법을

포스팅해 보도록 하겠습니다

첫번째는 파이썬을 설치 해야 합니다

<https://www.python.org/downloads/>

[ Download Python The official home of the Python Programming Language
www.python.org ](https://www.python.org/downloads/)

해당 싸이트에 접속한 뒤에 아래 버튼을 통해 다운로드 받습니다

![](/assets/images/파이썬_pymssql를_활용한_mssql_db_데이터_조회/img.png)

구버전을 다운로드 하시고자 한다면 화면을 좀 더 아래로 내리면 버전별 다운로드가 가능합니다

![](/assets/images/파이썬_pymssql를_활용한_mssql_db_데이터_조회/img_1.png)

여기서 버전을 선택하여 Download를 눌러주시면 됩니다

다운 받은 설치 파일 실행하여 설치 합니다

![](/assets/images/파이썬_pymssql를_활용한_mssql_db_데이터_조회/img_2.png)

Install Now를 클릭하여 설치

정상 적으로 설치가 되셨으면 시작버튼을 누루면 다음과 같은 목록이 나옵니다

![](/assets/images/파이썬_pymssql를_활용한_mssql_db_데이터_조회/img_3.png)

다음 정상적인 설치가 되었는지 확인을 위해서 PowerSheel을 관리자 권한으로 실행 합니다

![](/assets/images/파이썬_pymssql를_활용한_mssql_db_데이터_조회/img_4.png)

파워쉘에서 다음 명령어를 실행합니다

(명령어 뒤에 V는 꼭 대문자로 해주셔야 합니다)

    
    
    python -V

이렇게 명령어를 치게 되면 현재 설치된 python의 버전 정보가 나타나야 합니다

![](/assets/images/파이썬_pymssql를_활용한_mssql_db_데이터_조회/img_5.png)

위와 같이 표기가 되어야 정상 구동이 되는 것입니다

그 다음 pymssql을 설치하기 위해 pip 명령어를 사용합니다

    
    
    pip install pymssql

위의 명령어를 치시면 설치가 진행 됩니다

![](/assets/images/파이썬_pymssql를_활용한_mssql_db_데이터_조회/img_6.png)

저는 이미 설치 해논 상태라 설치가 되어 있다고 나오네요

설치를 완료 하셨다면 정상적으로 설치가 되었는지 확인해야겠지요?

    
    
    python
    import pymssql

위의 명령어를 순서로 사용해 줍니다

![](/assets/images/파이썬_pymssql를_활용한_mssql_db_데이터_조회/img_7.png)

이렇게 pymssql에 패키를 불러와 다음 명령어를 대기하는 상태가 되어야 합니다

다음 파이썬 py 파일을 하나생성합니다

그리고 제일 상단에 pymssql 패키지를 불어와야 합니다

    
    
    import pymssql

간단하죠?

그다음 함수를 만들어서 MSSQL에 접속을 시도 할겁니다

    
    
    conn = pymssql.connect(server='localhost', database='SAC_VISION')

로컬의 SAC_VISION이라는 DB에 접속하겠다는 구문 입니다

여기서 혹 로컬이 아닌 네트워크 서버에 붙으신다면 server 뒤에 localhost가 아닌 IP 주소를 입력하시고

user='ID', password='패스워트'를 넣어주시면 됩니다

다음 커서를 생성하고

    
    
    cursor = conn.cursor()

쿼리를 돌릴 execute를 생성합니다

    
    
            cursor.execute("SELECT CONVERT(INT, MODEL_NO), CONVERT(INT, VARIABLE_1), VARIABLE_2, "
                          +"       CONVERT(INT, AREA_X)+CONVERT(INT, POINT_X), CONVERT(INT, AREA_Y)+CONVERT(INT, POINT_Y), "
                          +"       CONVERT(INT, AREA_X)+CONVERT(INT, AREA_WIDTH)+CONVERT(INT, POINT_X),"
                          +"       CONVERT(INT, AREA_Y)+CONVERT(INT, AREA_HEIGHT)+CONVERT(INT, POINT_Y)"
                          +"  FROM [VISION_MODEL]"
                          +" WHERE REPLACE(VISION_NO,' ', '') = '" + str(k_vision_no) + "'"
                          +"   AND REPLACE(MODEL_METHOD,' ', '') = 'CLASSIFICATION'")

쿼리 내용은 따라 하지 않으셔도 됩니다~

※ 본인이 조회 할려는 Query를 사용하세요

    
    
    row = cursor.fetchone()

그리고 한개씩의 값을 row라는 변수에 담아 줍니다

    
    
    while row:
                list_roi.append(row)
                row = cursor.fetchone()
            conn.close()

이렇게 해서 실행하시게 되면 해당 쿼리의 결과값을 받으실수 있는데요

제가 만든 전체 함수를 올려드리 활용하여 알맞게 수정하여 사용하시기 바랍니다

    
    
    def Read_CSV_ALL_Section(self, _cam_info = 1, _path = None):
            list_roi = []
            k_vision_no = _cam_info
    
            conn = pymssql.connect(server='localhost', database='SAC_VISION')
            cursor = conn.cursor()
            cursor.execute("SELECT CONVERT(INT, MODEL_NO), CONVERT(INT, VARIABLE_1), VARIABLE_2, "
                          +"       CONVERT(INT, AREA_X)+CONVERT(INT, POINT_X), CONVERT(INT, AREA_Y)+CONVERT(INT, POINT_Y), "
                          +"       CONVERT(INT, AREA_X)+CONVERT(INT, AREA_WIDTH)+CONVERT(INT, POINT_X),"
                          +"       CONVERT(INT, AREA_Y)+CONVERT(INT, AREA_HEIGHT)+CONVERT(INT, POINT_Y)"
                          +"  FROM [VISION_MODEL]"
                          +" WHERE REPLACE(VISION_NO,' ', '') = '" + str(k_vision_no) + "'"
                          +"   AND REPLACE(MODEL_METHOD,' ', '') = 'CLASSIFICATION'")
    
            row = cursor.fetchone()
            
            while row:
                list_roi.append(row)
                row = cursor.fetchone()
            conn.close()
            
            return list_roi

저는 저에게 맞는 방법으로 구현하것이라 소스코드를 그래도 사용하시면 오류가 나실겁니다~

꼭 수정하셔서 사용하세요~

  

#python #파이썬 #python mssql #mssql select #파이썬 DB접속

