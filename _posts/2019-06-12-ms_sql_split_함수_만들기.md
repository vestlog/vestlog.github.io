---
title:  "[2019-06-12] - [MS-SQL] Split 함수 만들기!!"
categories:
  - Blog
tags:
  - "함수"
  - "MSSQL"
  - "자르기"
  - "function"
  - "split"
last_modified_at: 2025-05-30T16:03:55+09:00
---

## [MS-SQL] Split 함수 만들기!!

코딩정보/MS-SQL

2019-06-12 08:23:20

* * *

안녕하세요

코딩하는 남자의 코딩연습생입니다

MSSQL에서 Split 제공 함수가 없습니다

그래서 사용자 Function으로 만들어 두시면 프로시져 내부에서 사용하시가 편합니다

    
    
    CREATE FUNCTION arr_split(
        @sText VARCHAR(500), -- 대상 문자열
        @str CHAR(1) = '|', -- 구분기호(Default '|')
        @idx INT -- 배열 인덱스
    
     )
    
    
    RETURNS VARCHAR(20)
    AS
    BEGIN
         DECLARE @word CHAR(20), -- 반환할 문자
         @sTextData VARCHAR(600), 
         @num SMALLINT;
    
          SET @num = 1;
          SET @str = LTRIM(RTRIM(@str));
          SET @sTextData = LTRIM(RTRIM(@sText)) + @str; 
    
          WHILE @idx >= @num
          BEGIN
    
                 IF CHARINDEX(@str, @sTextData) > 0
                 BEGIN
                       -- 문자열의 인덱스 위치의 요소를 반환
                       SET @word = SUBSTRING(@sTextData, 1, CHARINDEX(@str, @sTextData) - 1);
                       SET @word = LTRIM(RTRIM(@word));
    
                       -- 반환된 문자는 버린후 좌우공백 제거 
                       SET @sTextData = LTRIM(RTRIM(RIGHT(@sTextData, LEN(@sTextData) - (LEN(@word) + 1))))
                 END
    
                 ELSE
    
                 BEGIN
                       SET @word = NULL;
                 END
                 SET @num = @num + 1
          END
       RETURN(@word);
    END

  

#함수 #MSSQL #자르기 #function #split

