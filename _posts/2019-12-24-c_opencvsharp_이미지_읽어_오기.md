---
categories:
  - 'Blog'
tags:
  - 'c#'
  - '불러오기'
  - '파일불러오기'
  - 'opencv'
  - 'opencvsharp'
  - 'PictureBoxIpI'
  - '그림파일넣기'
last_modified_at: '2025-05-30T16:03:57+09:00'
title: '[2025-08-13] - Post'
excerpt: ''
layout: 'post'
lang: 'ko'
permalink: '/posts/2019-12-24-c_opencvsharp_이미지_읽어_오기/'
alt_en: '/en/posts/2019-12-24-c_opencvsharp_이미지_읽어_오기/'
---

## [C#] OpenCvSharp 이미지 읽어 오기

코딩정보/C#

2019-12-24 12:38:04

* * *

안녕하세요

코딩하는남자 코딩연습생입니다

저번 블로그에서 C#에서 OpenCv라이브러리 등록을 통한 도구항목 추가에 대해서 공유했었는데요

혹시 처음 오신분은 아래 링크에서 확인하시기 바랍니다

<https://codingman.tistory.com/47>

[ [C#] OpenCv 라이브러리 사용하기 안녕하세요 코딩하는남자 코딩연습생입니다 저번 블로그에서 OpenCV에 대한 소개글을 한번
올렸엇는데요 https://codingman.tistory.com/46 [OpenCV] OpenCVSharp 분석하기 안녕하세요 코딩하는남자
코딩연습생입.. codingman.tistory.com ](https://codingman.tistory.com/47)

이번에는 추가한 픽쳐박스 구성하는 방법, 이미지 불러오는 방법, 이미지 확대 방법에 대해서 포스팅 해보도록 하겠습니다

1\. 픽쳐박스 구성 방법

\- OpenCvSharp PictureBoxIpI 콘트롤 사용 방법

![](/assets/images/c_opencvsharp_이미지_읽어_오기/img.jpg)

\- 비쥬얼스튜디오의 도구상자에서 PictureBoxIpI 컨트로를 드래그앤드롭하여 디자인폼으로 이동 시킵니다

![](/assets/images/c_opencvsharp_이미지_읽어_오기/img_1.jpg)

저는 이렇게 디자인 했습니다

연습하는냐고 이것저것 해보는냐고 MenuStrip과 파일 읽어올때 사용할 OpenFileDialog도 추가해줬구요

드래그 앤 드롭 시킨 PictureBoxIpI 의 속성을 설정해 볼께요

![](/assets/images/c_opencvsharp_이미지_읽어_오기/img_2.jpg)

고정 크기를 사용하기 위해 사이즈를 320x207로 고정 시킵니다

![](/assets/images/c_opencvsharp_이미지_읽어_오기/img_3.jpg)

사이즈 모드에서 불러온 이미지가 사이즈 크기에 맞게 자동 조절되어 그려지도록 사이즈 모드를 StretchImage로 변경

위와 같이 설정을 하게되면 일단 PictureBoxIpI에 대한 사용할 수 있는 상태가 되었구요

[Source Code]

    
    
    using OpenCvSharp;

소스 코드 작성을 위해 Form 소스에 다음과 같이 정의해줍니다

2\. PictureBoxIpI 클릭으로 이미지 확대하기

\- PictureBoxIpI의 클릭 이벤트를 설정해 주세요

![](/assets/images/c_opencvsharp_이미지_읽어_오기/img_4.jpg)

\- [Source Code]

    
    
            private void pictureBoxIpl1_Click(object sender, EventArgs e)
            {
                if (pictureBoxIpl1.ImageIpl == null) return;
    
                using (CvWindow wind = new CvWindow("원본그림"))
                {
                    wind.Image = src;
                    Cv.WaitKey(0);
                }
            }

이렇게 하게 되면 PictureBoxIpI 클릭하면 해당 불러온 이미지를 확대하여 볼수 있습니다

3\. 그림 파일 읽어와서 PictureBoxIpI에 보여주기

\- 디자인에서 도구 상자 항목 중 openFileDialog를 드래그 앤 그롭하여 디자인 폼에 생성 시킵니다

\- 추가로 똑같이 도구 상자 항목 중 menuStrip을 드래그 앤 그롭하여 디자인 폼에 생성 시킵니다

\- 아래 그림과 같이 menuStrip에서 파일 -> 그림읽기를 만들어 주세요

![](/assets/images/c_opencvsharp_이미지_읽어_오기/img_5.jpg)

\- 그 다음 그림읽기 메뉴에 클릭 이벤트 추가

![](/assets/images/c_opencvsharp_이미지_읽어_오기/img_6.jpg)

\- [Source Code]

    
    
            private void 그림읽기ToolStripMenuItem_Click(object sender, EventArgs e)
            {
                if (openFileDialog1.ShowDialog() == DialogResult.OK)  //파일 읽어 오기 추가
                {
                    loadImage(openFileDialog1.FileName);
                }
                else
                {
                    return;
                }
    
            }
    
    
            private void loadImage(String filename)
            {
                src = new IplImage(filename, LoadMode.AnyColor); //Opencv형태로 그림 파일을 읽어다 src에 저장
                pictureBoxIpl1.ImageIpl = src;
            }

\- 위의 소스코드를 사용하시면 PictureBoxIpI에 넣을 그림 파일을 선택할 Dialog창이 뜨고 파일을 선택하면

해당 파일이 PictureBoxIpI에 보여지게 됩니다

[2019.12.30]

OpenCvSharp Dll 오류 해결하기 위한 신규 라이브러리 추가 방법

*해당 포스팅을 따라하시다가 오류 나시는 분들은 다음 링크를 통해 OpenCvSharp DLL을 변경하시기 바랍니다

<https://codingman.tistory.com/49>

[ [C#]OpenCvSharp 라이브러리 사용하기 #1 안녕하세요 저번 포스팅에 C#으로 OpenCvSharp 라이브러리를 등록하여
구현하는 포스팅을 준비하던중에 OpenCv 3,4 버전에서 오류가 발생하는 문제가 있다는 얘길 듣고 부랴부랴 포스팅 내용을 검토해봤는데
역시.. codingman.tistory.com ](https://codingman.tistory.com/49)

  

#c# #불러오기 #파일불러오기 #opencv #opencvsharp #PictureBoxIpI #그림파일넣기

