---
categories:
  - 'Blog'
tags:
  - 'c#'
  - 'opencv'
  - '이미지효과'
  - '이미지필터'
  - 'opencvsharp'
  - '그레이효과'
last_modified_at: '2025-05-30T16:03:57+09:00'
title: '[2025-08-13] - Post'
excerpt: ''
layout: 'post'
lang: 'ko'
permalink: '/posts/2019-12-30-c_opencvsharp_그레이_효과_주기/'
alt_en: '/en/posts/2019-12-30-c_opencvsharp_그레이_효과_주기/'
---

## [C#] OpenCvSharp 그레이 효과 주기

코딩정보/OpenCv

2019-12-30 09:45:23

* * *

안녕하세요

요즘 C#으로 연습중인 OpenCv에서 불러온 이미지에 전체 그레이 효과를 주는 이벤트를

제작해 보겠습니다

C#을 통해 OpenCv 라이브러리 등록방법은 아래 링크를 확인해주세요

<https://codingman.tistory.com/49>

[ [C#]OpenCvSharp 라이브러리 사용하기 #1 안녕하세요 저번 포스팅에 C#으로 OpenCvSharp 라이브러리를 등록하여
구현하는 포스팅을 준비하던중에 OpenCv 3,4 버전에서 오류가 발생하는 문제가 있다는 얘길 듣고 부랴부랴 포스팅 내용을 검토해봤는데
역시.. codingman.tistory.com ](https://codingman.tistory.com/49)

그다음 C#을 통해 OpenCv 그림박스에 이미지 불러오기는 아래 링크를 확인해 주세요

<https://codingman.tistory.com/48>

[ [C#] OpenCvSharp 이미지 읽어 오기 안녕하세요 코딩하는남자 코딩연습생입니다 저번 블로그에서 C#에서 OpenCv라이브러리
등록을 통한 도구항목 추가에 대해서 공유했었는데요 혹시 처음 오신분은 아래 링크에서 확인하시기 바랍니다 https://coding..
codingman.tistory.com ](https://codingman.tistory.com/48)

이렇게 위의 과정을 모두 이해하셨다면 이제 이어서 불러온 이미지에 그레이 효과를 넣어보도록 하겠습니다

[디자인]

미리 만들어 놓은 MenuStepmenuStrip에 필터 -> 그레이라는 메뉴를 등록합니다

![](/assets/images/c_opencvsharp_그레이_효과_주기/img.jpg)

[Source Code]

-MenuStep에서 그레이 버튼을 클릭하였을때 실행될 클릭 이벤트를 생성합니다

![](/assets/images/c_opencvsharp_그레이_효과_주기/img_1.jpg)

\- 그다음 해당 클릭 이벤트에 다음과 같이 코딩 합니다

    
    
    private void 그레이ToolStripMenuItem_Click(object sender, EventArgs e)
            {
                using (gray gg = new gray())
                using (IplImage temp = gg.grayProcess(src))
                {
                    result = temp.Clone();
    
                }
                pictureBoxIpl2.ImageIpl = result;
    
            }

\- 그다음 이미지 필터 기능을 쉽게 구별할수 있도록 그레이 클레스를 생성합니다

![](/assets/images/c_opencvsharp_그레이_효과_주기/img_2.jpg)

\- 생성된 gray.cs 파일에 다음과 같이 코딩합니다

![](/assets/images/c_opencvsharp_그레이_효과_주기/img_3.jpg)

[Source Code]

    
    
    using System;
    using System.Collections.Generic;
    using System.Text;
    using OpenCvSharp;
    
    namespace OpenCV_V1
    {
        class gray : IDisposable
        {
            IplImage subgray;
    
            public IplImage grayProcess(IplImage src)
            {
                subgray = new IplImage(src.Size, BitDepth.U8, 1);
                Cv.CvtColor(src, subgray, ColorConversion.BgrToGray);
    
                return subgray;
            }
    
            public void Dispose()
            {
                if (subgray != null) Cv.ReleaseImage(subgray);
            }
    
            public IplImage ThresholdProcess(IplImage src)
            {
                subgray = new IplImage(src.Size, BitDepth.U8, 1);  //메모리 확보
                Cv.CvtColor(src, subgray, ColorConversion.BgrToGray); //그레이로 변환
                Cv.Smooth(subgray, subgray, SmoothType.Gaussian, 5);  //가우시안 스무스 주기
                Cv.Threshold(subgray, subgray, 120, 255, ThresholdType.Binary);  //120은 기준이 될 임계치
    
                return subgray;
            }
    
            public IplImage BuildCanny(IplImage src)
            {
                subgray = new IplImage(src.Size, BitDepth.U8, 1);  //메모리 확보
                Cv.CvtColor(src, subgray, ColorConversion.BgrToGray);   //그레이로 변환
    
                Cv.Canny(subgray, subgray, 80, 255);
    
                return subgray;
            }
    
            public IplImage BuildSobel(IplImage src)
            {
                subgray = new IplImage(src.Size, BitDepth.U8, 1);//메모리 확보
                Cv.CvtColor(src, subgray, ColorConversion.BgrToGray); //그레이로 변환
    
                Cv.Sobel(subgray, subgray, 1, 0, ApertureSize.Size3);
    
                return subgray;
            }
    
            public IplImage BuildLaplace(IplImage src)
            {
                subgray = new IplImage(src.Size, BitDepth.U8, 1);//메모리 확보
                using (IplImage temp = new IplImage(src.Size, BitDepth.S16, 1))
                using (IplImage graytemp = new IplImage(src.Size, BitDepth.U8, 1))
                {
                    Cv.CvtColor(src, graytemp, ColorConversion.BgrToGray); //그레이로 변환
    
                    Cv.Laplace(graytemp, temp);
                    Cv.ConvertScaleAbs(temp, subgray);
                    return subgray;
                }
            }
        }
    }
    

\- 이렇게 한뒤 실행하면 다음과 같은 효과를 나타낼수 있습니다

![](/assets/images/c_opencvsharp_그레이_효과_주기/img_4.jpg)

  

#c# #opencv #이미지효과 #이미지필터 #opencvsharp #그레이효과

