---
title:  "[2021-01-11] - [Python] 티스토리 API 사용을 위한 Access_token 구하기"
categories:
  - Blog
tags:
  - "파이썬"
  - "티스토리"
  - "티스토리"
  - "티스토리토큰"
last_modified_at: 2025-05-30T16:04:05+09:00
---

## [Python] 티스토리 API 사용을 위한 Access_token 구하기

코딩정보/Python

2021-01-11 15:05:23

* * *

안녕하세요

코딩연습생입니다~

이번 포스팅은 파이썬 언어를 통해 티스토리 API를 사용하여 자동 업로드를 구현해 볼려고 합니다

구현에 앞서 몇가지 준비사항들이 필요한데

_1\. Token 키를 알아야 합니다(이번 포스팅 내용)_

2\. 글을 올리려고 하시는 카테고리 ID를 알아야 합니다

3\. 파일 첨부시 이미지 파일만 가능합니다

그러면 시작해 보도록 할께요

1\. token 키를 확인하기

<https://www.tistory.com/guide/api/manage/register>

[ TISTORY 나를 표현하는 블로그를 만들어보세요. www.tistory.com
](https://www.tistory.com/guide/api/manage/register)

위의 사이트에 접속합니다

![](/assets/images/python_티스토리_api_사용을_위한_access_token_구하기/img.png)

빨간색으로 표기된 부분을 모두 작성합니다

서비스명 : 블로그명을 입력합니다

서비스URL : 블로그 전체 주소를 입력합니다

서비스형태 : 웹서비스

서비스권한 : 읽기.쓰기

CallBack : 서비스 URL와 동일하게 입력합니다

그 다음 등록을 눌러주세요

등록이 완료가 되면 앱 관리 메뉴로 들어가서 상세 내용을 확인 합니다

![](/assets/images/python_티스토리_api_사용을_위한_access_token_구하기/img_1.png)

앱 관리 -> 등록된 서비스명의 설정을 클릭

![](/assets/images/python_티스토리_api_사용을_위한_access_token_구하기/img_2.png)

설정 메뉴에서 다음 값을 확인 할 수 있습니다

1\. App ID, Secret Key

![](/assets/images/python_티스토리_api_사용을_위한_access_token_구하기/img_3.png)

AppID와 Secret Key를 알았다면 익스플로러를 실행해서 다음 주소를 입력 합니다

    
    
    https://www.tistory.com/oauth/authorize?client_id={AppID}&redirect_uri={서비스URL}&response_type=code&state=someValue

AppID와 서비스URL은 설정화면에 있는 정보를 넣어주시면 됩니다

위의 URL을 접속하시면 아래와 같은 화면이 나오게됩니다

![](/assets/images/python_티스토리_api_사용을_위한_access_token_구하기/img_4.png)

이런 창이 드시면 허가하기를 눌러줍니다

새로운 창이 뜨면서 위의 url 주소 중 아래 빨간색 영역으로 표기된 부분을 잘 복사해 줍니다

![](/assets/images/python_티스토리_api_사용을_위한_access_token_구하기/img_5.png)

code 값을 얻으셨다면 이제 마지막 단계만 하시면 Access Token을 얻으실수 있습니다

    
    
    https://www.tistory.com/oauth/access_token?client_id={AppID}&client_secret={SecretKey}&redirect_uri={서비스URL}&code=코드&grant_type=authorization_code

해당 주소를 익스플로러에 입력해주시고 디버깅 모드를 여시면 아래와 같이 Access_token을 얻으실수 있습니다

![](/assets/images/python_티스토리_api_사용을_위한_access_token_구하기/img_6.png)

다음번 포스팅에서는 이번에 얻은 Access_token을 사용하여 파이썬으로 카테고리 ID를 확인하는 방법을 포스팅

하도록 하겠습니다

  

#파이썬 #티스토리 자동글 올리기 #티스토리 Access_token #티스토리토큰

