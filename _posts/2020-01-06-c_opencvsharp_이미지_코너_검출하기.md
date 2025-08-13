---
categories:
  - 'Blog'
tags:
  - '이미지편집'
  - 'c#'
  - 'opencv'
  - 'opencvsharp'
  - '이미지처리'
  - '이미지코너검출'
  - '코너검출'
last_modified_at: '2025-05-30T16:03:57+09:00'
title: '[2025-08-13] - Post'
excerpt: ''
layout: 'post'
lang: 'ko'
permalink: '/posts/2020-01-06-c_opencvsharp_이미지_코너_검출하기/'
alt_en: '/en/posts/2020-01-06-c_opencvsharp_이미지_코너_검출하기/'
---

## [C#] OpenCvSharp 이미지 코너 검출하기

코딩정보/OpenCv

2020-01-06 15:41:50

* * *

안녕하세요

이번 포스팅은 불러온 이미지에서 CornerMinEigenVal을 이용한 코너 검출 그리고 CornerHarris를 이용한 코너 검출을

포스팅 해볼려고 합니다

일단 포스팅을 읽기에 앞서 OpenCvSharp에 대해서 공부하면서 연결해서 포스팅 중인데

이미지를 불러오는 방법이나 이미지 처리에 관련된 기본 포스팅은 아래 링크를 통해 확인하시기 바랍니다

연제성 포스팅이기 때문에 해당 본문 내용이 다소 생략될수 잇으니 양해 바랍니다

<https://codingman.tistory.com/49>

[ [C#]OpenCvSharp 라이브러리 사용하기 #1 안녕하세요 저번 포스팅에 C#으로 OpenCvSharp 라이브러리를 등록하여
구현하는 포스팅을 준비하던중에 OpenCv 3,4 버전에서 오류가 발생하는 문제가 있다는 얘길 듣고 부랴부랴 포스팅 내용을 검토해봤는데
역시.. codingman.tistory.com ](https://codingman.tistory.com/49)

포스팅에 앞서 공부한 내용을 설명하고 프로그램에 대한 부분도 설명 드리겠습니다

이미지 처리 기법중 여러 방식의 코너 검출이 있습니다

그중 OpenCv는 4가지 커널을 사용하여 코너를 검출 합니다

\- 사각형

\- 다이아몬드

\- X

\- 십자

이 형태의 커널들을 이용하여 팽창, 침식 시킨 후 차영상을 통해 코너를 검출한다고 합니다

이러한 형태를 사용하여 쉽게 코너를 검출할 수 있는 함수가 OpenCv에 존재하는데요

바로 goodFeaturesToTrack라는 함수 입니다

해당 함수의 형태는

C#: void GoodFeaturesToTrack(CvArr image, CvArr eigImage, CvArr tempImage, out
CvPoint2D32f[] corners, ref int cornerCount, double qualityLevel, double
minDistance, CvArr mask);

• image – 8비트, 32비트 부동소수점 단일 이미지

• eigImage – 이미지와 동일한 크기의 임시 부동 소수점 32 비트 이미지

• tempImage – eigImage 와 크기 및 형식이 다른 임시 이미지

• corners – 검출된 코너를 담을 벡터

• cornerCount– 반환될 코너의 최대 개수, 만약 찾아낸 코너의 수가 더 많을 경우, 강력한 코너가 반환된다.

• qualityLevel – 코너라고 판단하기 위한 기준이 되는 최소의 값, 이 값은 최고의 minimal eigenvalue를 가지는
코너의 quality에 곱해지며, 그 값보다 작은 quality를 갖는 코너는 코너라고 판단하지 않는다. 예를 들어,

최고의 minimal eigenvalue=1500 이고, qualityLevel= 0.01 이면, quality가 15보다 작은 코너는

무시된다.

• minDistance – 반환되는 코너 사이의 최소 유클리디안 거리

• mask – 코너를 찾을 관심영역, input과 크기가 동일해야한다..

이렇게 사용되어 집니다

그러면 우선 메인폼의 디자인부터 설정하겠습니다

[디자인]

\- 메인폼의 Menu트립에서 다음과 같이 디자인 합니다

\- 최상단에 알고리즘 -> 코너검출 -> EigenVal / Harris

![](/assets/images/c_opencvsharp_이미지_코너_검출하기/img.jpg)

\- Menu 트립에 클릭 이벤트를 생성합니다

![](/assets/images/c_opencvsharp_이미지_코너_검출하기/img_1.jpg)
![](/assets/images/c_opencvsharp_이미지_코너_검출하기/img_2.jpg)

[Source Code]

\- EigenVal / Harris의 각각의 클릭 이벤트에 다음과 같은 코딩을 해줍니다

    
    
            private void eigenValToolStripMenuItem_Click(object sender, EventArgs e)
            {
                using (corner Cn = new corner())
                using (IplImage temp = Cn.EigenValCornerDetect(src))
                {
                    result = temp.Clone();
    
                }
                pictureBoxIpl2.ImageIpl = result;
    
            }
    
    
            private void harrisToolStripMenuItem_Click(object sender, EventArgs e)
            {
                using (corner Cn = new corner())
                using (IplImage temp = Cn.HarrisCornerDetect(src))
                {
                    result = temp.Clone();
    
                }
                pictureBoxIpl2.ImageIpl = result;
    
            }

\- 코너 검출을 위한 Class 생성

(클래스명징은 corner로 사용하였습니다)

[Class Sorce Code]

\- Class 생성 방법은 이전 포스팅에서 설명했기 때문에 생략하도록 하겠습니다

![](/assets/images/c_opencvsharp_이미지_코너_검출하기/img_3.jpg)

    
    
    using System;
    using System.Collections.Generic;
    using System.Text;
    using OpenCvSharp;
    
    namespace OpenCV_V1
    {
        class corner : IDisposable
        {
            IplImage cor;
    
    
            public IplImage EigenValCornerDetect(IplImage src)
            {
                // cvGoodFeaturesToTrack, cvFindCornerSubPix
                // 화상의 코너 검출
    
                int cornerCount = 150;
    
                using (IplImage dstImg = src.Clone())
                using (IplImage srcImgGray = new IplImage(src.Size, BitDepth.U8, 1))
                using (IplImage eigImg = new IplImage(srcImgGray.GetSize(), BitDepth.F32, 1))
                using (IplImage tempImg = new IplImage(srcImgGray.GetSize(), BitDepth.F32, 1))
                {
                    Cv.CvtColor(dstImg, srcImgGray, ColorConversion.BgrToGray);
    
                    CvPoint2D32f[] corners;
                    // (1) CornerMinEigenVal를 이용한 코너 검출
                    Cv.GoodFeaturesToTrack(srcImgGray, eigImg, tempImg, out corners, ref cornerCount, 0.1, 15);
                    Cv.FindCornerSubPix(srcImgGray, corners, cornerCount, new CvSize(3, 3), new CvSize(-1, -1), new CvTermCriteria(20, 0.03));
                    // (2) 코너 그리기
                    for (int i = 0; i < cornerCount; i++)
                        Cv.Circle(dstImg, corners[i], 3, new CvColor(255, 0, 0), 2);
    
                    cor = dstImg.Clone();
    
                }
    
                return cor;
            }
    
            public IplImage HarrisCornerDetect(IplImage src)
            {
                // cvGoodFeaturesToTrack, cvFindCornerSubPix
                // 화상의 코너 검출
    
                int cornerCount = 150;
    
                using (IplImage dstImg = src.Clone())
                using (IplImage srcImgGray = new IplImage(src.Size, BitDepth.U8, 1))
                using (IplImage eigImg = new IplImage(srcImgGray.GetSize(), BitDepth.F32, 1))
                using (IplImage tempImg = new IplImage(srcImgGray.GetSize(), BitDepth.F32, 1))
                {
                    Cv.CvtColor(dstImg, srcImgGray, ColorConversion.BgrToGray);
    
                    CvPoint2D32f[] corners;
    
    
    
                    // (1) CornerHarris를 이용한 코너 검출
                    cornerCount = 150;
                    Cv.GoodFeaturesToTrack(srcImgGray, eigImg, tempImg, out corners, ref cornerCount, 0.1, 15, null, 3, true, 0.01);
                    Cv.FindCornerSubPix(srcImgGray, corners, cornerCount, new CvSize(3, 3), new CvSize(-1, -1), new CvTermCriteria(20, 0.03));
                    // (2) 코너 그리기
                    for (int i = 0; i < cornerCount; i++)
                        Cv.Circle(dstImg, corners[i], 3, new CvColor(0, 0, 255), 2);
    
                    cor = dstImg.Clone();
    
                }
    
                return cor;
            }
    
            public void Dispose()
            {
                if (cor != null) Cv.ReleaseImage(cor);
            }
        }
    }
    

이렇게 Class까지 생성한 다음 빌드 하여 실행 시키면 다음과 같은 결과 값을 얻을수 잇습니다

[결과창]

*EigenVal

![](/assets/images/c_opencvsharp_이미지_코너_검출하기/img_4.jpg)

*Harris

![](/assets/images/c_opencvsharp_이미지_코너_검출하기/img_5.jpg)

  

#이미지편집 #c# #opencv #opencvsharp #이미지처리 #이미지코너검출 #코너검출

