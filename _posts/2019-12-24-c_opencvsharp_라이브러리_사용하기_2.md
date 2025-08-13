---
categories:
  - 'Blog'
tags:
  - 'xml'
  - 'c#'
  - '라이브러리'
  - 'opencv'
  - 'dll등록'
  - 'opencvsharp'
last_modified_at: '2025-05-30T16:03:56+09:00'
title: '[2025-08-13] - Post'
excerpt: ''
layout: 'post'
lang: 'ko'
permalink: '/posts/2019-12-24-c_opencvsharp_라이브러리_사용하기_2/'
alt_en: '/en/posts/2019-12-24-c_opencvsharp_라이브러리_사용하기_2/'
---

## [C#] OpenCvSharp 라이브러리 사용하기 #2

코딩정보/C#

2019-12-24 08:59:56

* * *

안녕하세요

코딩하는남자 코딩연습생입니다

저번 블로그에서 OpenCV에 대한 소개글을 한번 올렸엇는데요

<https://codingman.tistory.com/46>

[ [OpenCV] OpenCVSharp 분석하기 안녕하세요 코딩하는남자 코딩연습생입니다 요즘 개발 업무를 진행하면서 자주 듣는 말이
있습니다 비전, OCR, 템플릿 매칭, 등.. 어는샌가 개발자가 단순 처리 프로그램밍이 아닌 지능적 프로그래밍으로 변화 하..
codingman.tistory.com ](https://codingman.tistory.com/46)

관련 정보를 한번 보시고 난뒤에 C#에서 OpenCV를 사용하기 위한 첫단계를 진행해보곘습니다

저는 OpenCvSharp 네이버 카페에 올려져 있는 최신버전의 라이브러리를 사용했구요

비쥬얼 스튜디오 버전은 2017입니다

첫번째로 OpenCV에서 영상이나 이미지 처리를 위한 IplImage 전용 픽쳐박스를 사용해야 하는데요

IplImage용 픽쳐박스를 사용하는 방법을 소개 해보겟습니다

해당 자료는 <https://cafe.naver.com>/opencvsharp의 카페에서 강좌를 보고 실제 연습을 한 정보로

작성햇습니다

1\. IplImage용 픽쳐박스 사용을 위한 도구모음 등록

\- 도구상자에서 빈공간에서 마우스 오른쪽 버튼을 클릭하여 "항목선택"을 클릭

![](/assets/images/c_opencvsharp_라이브러리_사용하기_2/img.jpg)

\- 도구상자 항목 선택 창에서 찾아보기 버튼을 클릭

![](/assets/images/c_opencvsharp_라이브러리_사용하기_2/img_1.jpg)

\- 준비한 OpenCV 라이브러리 파일중 "OpenCvSharp.UserInterface.dll"파일을 선택

![](/assets/images/c_opencvsharp_라이브러리_사용하기_2/img_2.jpg)

\- 열기버튼을 누루면 도구모음항목선택창에서 다음과 같은 도구가 추가 된것을 확인할 수 있습니다

![](/assets/images/c_opencvsharp_라이브러리_사용하기_2/img_3.jpg)

![](/assets/images/c_opencvsharp_라이브러리_사용하기_2/img_4.jpg)

2. 프로젝트에서 OpenCV를 사용하기 위한 Dll 등록 하기

\- 비쥬얼스튜디오에서 솔루션탐색기 목록 중 참조 위치에서 마우스 오른쪽 버튼 클릭

![](/assets/images/c_opencvsharp_라이브러리_사용하기_2/img_5.jpg)

\- 마우스 오른족에서 나타난 리스트 중에 참조 추가 버튼 클릭

![](/assets/images/c_opencvsharp_라이브러리_사용하기_2/img_6.jpg)

\- 참조관리자 화면에서 찾아보기 버튼 클릭

![](/assets/images/c_opencvsharp_라이브러리_사용하기_2/img_7.jpg)

\- 준비한 OpenCv라이브러리 파일중 다음 Dll 파일을 선택

(OpenCvSharp.dll, OpenCvSharp.MachineLearning.dll)

![](/assets/images/c_opencvsharp_라이브러리_사용하기_2/img_8.jpg)

\- 참조 추가가 정상적으로 되었을 경우 솔루션탐색기에 다음과 같은 항목이 보이셔야 합니다

![](/assets/images/c_opencvsharp_라이브러리_사용하기_2/img_9.jpg)

\- Debug 폴더에 해당 참조가 생성될수 있도록 프로젝트 빌드를 수행 합니다

![](/assets/images/c_opencvsharp_라이브러리_사용하기_2/img_10.jpg)

\- 정상 빌드 수행 후 해당 프로젝트의 Debug 폴더를 보시면 다음과 같은 Dll파일과 XML문서가 생성되시면

정상적인 OpenCvSharp가 등록된 것입니다

![](/assets/images/c_opencvsharp_라이브러리_사용하기_2/img_11.jpg)

다음과 같은 과정이 모두 정상적으로 되셧다면 이제 OpenCvSharp를 사용할 준비가 완료된 것이며

현재 만드신 프로젝트를 가지고 OpenCvSharp에 대한 기능를 하나씩 연습해 보도록 하겠습니다

  

#xml #c# #라이브러리 #opencv #dll등록 #opencvsharp

