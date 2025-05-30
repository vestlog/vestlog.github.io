---
title:  "[2019-12-30] - [C#]OpenCvSharp 라이브러리 사용하기 #1"
categories:
  - Blog
tags:
  - "xml"
  - "c#"
  - "opencv"
  - "dll등록"
  - "opencvsharp"
  - "라이브러리등록"
  - "c#"
last_modified_at: 2025-05-30T16:03:57+09:00
---

## [C#]OpenCvSharp 라이브러리 사용하기 #1

코딩정보/C#

2019-12-30 08:22:53

* * *

안녕하세요

저번 포스팅에 C#으로 OpenCvSharp 라이브러리를 등록하여 구현하는 포스팅을 준비하던중에

OpenCv 3,4 버전에서 오류가 발생하는 문제가 있다는 얘길 듣고 부랴부랴 포스팅 내용을 검토해봤는데

역시나...제가 포스팅한 글에서도 역시 오류가 발생하더라구요

그래서 해당 부분을 오류 해결하고 OpenCvSharp 오류 없는 버젼을 추가할수 있는 방법을 재 포스팅 햇습니다

아마 순서로는 해당 글이 1번글이고 이 이후에 과정은 동일합니다

해당글을 먼저 읽고 라이브러리를 등록한 뒤에 빌드한뒤 나온 DLL를 사용하여 다름 아래 링크 과정을 따라 하시면

오류 없이 OpenCv를 사용할 수 있습니다

[과정]

1\. 프로젝트 생성 #1

\- 비쥬얼 스튜디오 2017을 이용하여 신규 프로젝트를 생성합니다

![](/assets/images/c_opencvsharp_라이브러리_사용하기_1/img.jpg)

2\. 프로젝트 생성 #2

\- Windows Forms 앱 형식의 프로젝트를 생성하고 아래 속성 값을 지정해 줍니다

(이름, 위치만 설정하시면 솔루션, 솔루션이름은 자동으로 동기화 됩니다)

![](/assets/images/c_opencvsharp_라이브러리_사용하기_1/img_1.jpg)

3\. NuGet을 통한 OpenCvSharp 설치 하기

\- 비쥬얼스튜디오의 솔루션탐색기에서 참조 위치에서 마우스 오른쪽 버튼을 클릭한뒤 NuGet 패키지 관리를 클릭

![](/assets/images/c_opencvsharp_라이브러리_사용하기_1/img_2.jpg)

4\. NuGet 패키지 찾기 #1

\- NuGet 패키지 관리창에서 찾아보기를 클릭한뒤 검색창에 OpenCvSharp를 검색

![](/assets/images/c_opencvsharp_라이브러리_사용하기_1/img_3.jpg)

5\. NuGet 패키지 찾기 #2

\- OpecCv 2.x wrapper 버전을 클릭

![](/assets/images/c_opencvsharp_라이브러리_사용하기_1/img_4.jpg)

6\. NuGet 패키지 설치

\- OpenCvSharp-AnyCPU 버전를 확인 한뒤 설치 버튼을 통해 설치

![](/assets/images/c_opencvsharp_라이브러리_사용하기_1/img_5.jpg)

7\. 정상 설비 여부 확인

\- 나의 프로젝트 참조 부분에 다음과 같은 참조가 추가되었으면 성공

![](/assets/images/c_opencvsharp_라이브러리_사용하기_1/img_6.jpg)

8\. 프로젝트 빌드

\- 7번까지 성공 되셨으면 해당 프로젝트를 빌드하여 Debug폴더에 해당 버전의 OpenCv Dll 파일을 생성

![](/assets/images/c_opencvsharp_라이브러리_사용하기_1/img_7.jpg)

8번까지 성공하셨나요?? 그러면 오류 없는 OpenCv 버전이 정상적으로 등록되신겁니다

이후 과정은 기존 포스팅 내용을 따라 하시면 오류 없이 예제가 실행될 겁니다

다음 과정 포스팅 링크는 아래를 클릭해 주세요 ↓↓↓↓↓↓↓↓↓

<https://codingman.tistory.com/47>

[ [C#] OpenCv 라이브러리 사용하기 안녕하세요 코딩하는남자 코딩연습생입니다 저번 블로그에서 OpenCV에 대한 소개글을 한번
올렸엇는데요 https://codingman.tistory.com/46 [OpenCV] OpenCVSharp 분석하기 안녕하세요 코딩하는남자
코딩연습생입.. codingman.tistory.com ](https://codingman.tistory.com/47)

문제에 대해서는 뎃글 달라주시면 같이 해결해보도록 하겟습니다

감사합니다

  

#xml #c# #opencv #dll등록 #opencvsharp #라이브러리등록 #c# opencv버전

