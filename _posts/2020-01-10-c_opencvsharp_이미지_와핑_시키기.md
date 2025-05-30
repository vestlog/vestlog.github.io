---
title:  "[2020-01-10] - [C#] OpenCvSharp 이미지 와핑 시키기"
categories:
  - Blog
tags:
  - "이미지편집"
  - "c#"
  - "opencv"
  - "와핑"
  - "Warping"
  - "WarpPerspective"
  - "opencvsharp"
  - "이미지왜곡"
  - "이미지변조"
last_modified_at: 2025-05-30T16:03:58+09:00
---

## [C#] OpenCvSharp 이미지 와핑 시키기

코딩정보/OpenCv

2020-01-10 13:30:27

* * *

안녕하세요

요즘 하루에 2개 이상씩 포스팅하고 있네요ㅎㅎ

얼른 목표로 하고 있는 이미지 기법등을 공부해서 C#으로 이미지 판독 프로그램이나

OCR 같은 지능형 프로그램을 만들어보는게 목표인데

아직 OpenCvSharp만 디딥다 파고 있습니다ㅎㅎ

기본 정보를 모으고 그걸 구현해보고 오류 수정하고 매일 이걸 반복하고 있으니 이젠 제가

블로거인지...프로그래머인지...사진편집가인지 헷갈리네요ㅎㅎㅎ

아무튼 OpenCv 포스팅을 이어서 하겠습니다

이번 포스팅은 이미지 와핑이라는 것인데요

와핑이라는게 이미지를 왜곡시키는 기능인데요

이미지를 찌그러 트리거나 회전시키거나 뭐 이런 기능을 다 와핑이라고 표현하는거 같습니다

그 와핑이라는것을 C# OpenCvSharp를 이용해서 구현해 보도록 할께요

처음 오시느 분들은 앞 포스팅에서 라이브러리 등록부터 보시고 오시면 좋을거 같습니다

<https://codingman.tistory.com/49>

[ [C#]OpenCvSharp 라이브러리 사용하기 #1 안녕하세요 저번 포스팅에 C#으로 OpenCvSharp 라이브러리를 등록하여
구현하는 포스팅을 준비하던중에 OpenCv 3,4 버전에서 오류가 발생하는 문제가 있다는 얘길 듣고 부랴부랴 포스팅 내용을 검토해봤는데
역시.. codingman.tistory.com ](https://codingman.tistory.com/49)

[디자인]

\- 메뉴에 와핑 버튼을 생성해줍니다

![](/assets/images/c_opencvsharp_이미지_와핑_시키기/img.jpg)

\- 와핑 버튼에 아래 같이 클릭 이벤트를 생성해 주구요

![](/assets/images/c_opencvsharp_이미지_와핑_시키기/img_1.jpg)

\- 늘 반복적으로 하는 행위라서 간단하게 넘어가겠습니다

\- 클릭 이벤트 지점에 다음과 같이 코딩 합니다

    
    
            private void 와핑ToolStripMenuItem_Click(object sender, EventArgs e)
            {
                if (src == null) return;
                using (perspect Pp = new perspect())
                using (IplImage temp = Pp.Perspective(src))
                {
                    result = temp.Clone();
    
                }
                pictureBoxIpl2.ImageIpl = result;
            }

\- 그 다음 이미지를 와핑 시키기 위해서 사용할 클래스를 생성해줍니다

![](/assets/images/c_opencvsharp_이미지_와핑_시키기/img_2.jpg)

\- 그리고 생성된 클래스 파일에 아래와 같이 코딩해 줍니다

    
    
    using System;
    using System.Collections.Generic;
    using System.Text;
    using OpenCvSharp;
    
    namespace OpenCV_V1
    {
        class perspect : IDisposable
        {
            IplImage Pp;
            public IplImage Perspective(IplImage srcImg)
            {
                // cvGetPerspectiveTransform + cvWarpPerspective
                // 화상상의 4점에 대응하는 투시 투영 변환 행렬을 계산해, 그 행렬을 이용해 화상 전체의 투시 투영 변환을 실시한다.
    
                // (1) 화상을 읽어들여, 출력용 화상 영역의 확보를 행한다
                using (IplImage dstImg = srcImg.Clone())
                {
                    // (2) 사각형의 변환전과 변환 후의 대응하는 정점을 각각 세트 해
                    //    cvWarpPerspective를 이용해 투시 투영 변환 행렬을 요구한다
                    CvPoint2D32f[] srcPnt = new CvPoint2D32f[4];
                    CvPoint2D32f[] dstPnt = new CvPoint2D32f[4];
                    srcPnt[0] = new CvPoint2D32f(150.0f, 150.0f);
                    srcPnt[1] = new CvPoint2D32f(150.0f, 300.0f);
                    srcPnt[2] = new CvPoint2D32f(350.0f, 300.0f);
                    srcPnt[3] = new CvPoint2D32f(350.0f, 150.0f);
                    dstPnt[0] = new CvPoint2D32f(200.0f, 200.0f);
                    dstPnt[1] = new CvPoint2D32f(150.0f, 300.0f);
                    dstPnt[2] = new CvPoint2D32f(350.0f, 300.0f);
                    dstPnt[3] = new CvPoint2D32f(300.0f, 200.0f);
                    using (CvMat mapMatrix = Cv.GetPerspectiveTransform(srcPnt, dstPnt))
                    {
                        // (3) 지정된 아핀 행렬에 의해, cvWarpAffine를 이용해 화상을 회전시킨다
                        Cv.WarpPerspective(srcImg, dstImg, mapMatrix, Interpolation.Linear | Interpolation.FillOutliers, CvScalar.ScalarAll(100));
                        Pp = dstImg.Clone();
                        return Pp;
    
                    }
                }
            }
            public void Dispose()
            {
                if (Pp != null) Cv.ReleaseImage(Pp);
            }
        }
    }
    

\- 그런 다음 이미지를 불러오고 와핑 시키면 다음과 같은 결과가 나타나게 됩니다

[결과 창]

![](/assets/images/c_opencvsharp_이미지_와핑_시키기/img_3.jpg)

  

#이미지편집 #c# #opencv #와핑 #Warping #WarpPerspective #opencvsharp #이미지왜곡 #이미지변조

