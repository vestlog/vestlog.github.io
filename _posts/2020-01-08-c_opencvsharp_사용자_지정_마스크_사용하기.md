---
categories:
  - 'Blog'
tags:
  - 'c#'
  - 'opencv'
  - 'threshold'
  - 'opencvsharp'
  - '사용자지정마스크'
  - '유저마스크'
  - 'Fiter2D'
last_modified_at: '2025-05-30T16:03:58+09:00'
title: '[2025-08-13] - Post'
excerpt: ''
layout: 'post'
lang: 'ko'
permalink: '/posts/2020-01-08-c_opencvsharp_사용자_지정_마스크_사용하기/'
alt_en: '/en/posts/2020-01-08-c_opencvsharp_사용자_지정_마스크_사용하기/'
---

<div class="lang-panel lang-ko" lang="ko">
## [C#] OpenCvSharp 사용자 지정 마스크 사용하기

코딩정보/OpenCv

2020-01-08 13:39:22

* * *

안녕하세요

벌써 OpenCvSharp를 공부한지 1달정도 되어 가는거 같네요

너무 범위가 넓어서 하나씩 하나씩 하자는 마음으로 시작했는데 끝이 안보이니깐 의욕이 점점 떨어지네요ㅎ

저번시간에 모폴로지에 대해 포스팅 했는데 이번시간에는

OpenCv의 Filter2D() 함수를 사용해서 사용자 지정 마스크 기능들을 구현해 볼려고 합니다

사용자 지정 마스크는 Filter2D의 함수를 어떻게 사용하는냐에 따라 지정될수 있습니다

[주요 함수 설명]

C# : Filter2DCv.Filter2D(s1, temp, b, new CvPoint(-1, -1));

  * s1 : 이미지
  * temp : 대상이미지
  * b : 커널 행렬
  * new CvPoint(-1, -1) : 커널 앵커

C# : ThresholdCv.Threshold(temp, temp, 80, 255, ThresholdType.BinaryInv);

  * temp : 이미지
  * trmp : 대상이미지
  * 80 : 임계치
  * 255 : 기준값을 넘었을 때 적용할 최대값
  * ThresholdType.BinaryInv : 임계치의 유형  
  

연속 포스팅이라서 처음 디자인을 구성하시는경우에는 처음 라이브러리 등록 포스팅 부터 보시기 바랍니다

<https://codingman.tistory.com/49>

[ [C#]OpenCvSharp 라이브러리 사용하기 #1 안녕하세요 저번 포스팅에 C#으로 OpenCvSharp 라이브러리를 등록하여
구현하는 포스팅을 준비하던중에 OpenCv 3,4 버전에서 오류가 발생하는 문제가 있다는 얘길 듣고 부랴부랴 포스팅 내용을 검토해봤는데
역시.. codingman.tistory.com ](https://codingman.tistory.com/49)

[디자인]

\- Menu에 필터 -> 유저마스크 -> 선명화1, 선명화2, 선명화3, 수평엣지, 수직엣지를 등록해 주세요

![](/assets/images/c_opencvsharp_사용자_지정_마스크_사용하기/img.jpg)

\- 각 메뉴에 클릭 이벤트 설정

(클릭 이벤트 설정하는 방법은 생략하겟습니다)

(그리고 이벤트 순서는 바뀌어도 문제되지 않습니다)

![](/assets/images/c_opencvsharp_사용자_지정_마스크_사용하기/img_1.jpg)
![](/assets/images/c_opencvsharp_사용자_지정_마스크_사용하기/img_2.jpg)
![](/assets/images/c_opencvsharp_사용자_지정_마스크_사용하기/img_3.jpg)
![](/assets/images/c_opencvsharp_사용자_지정_마스크_사용하기/img_4.jpg)
![](/assets/images/c_opencvsharp_사용자_지정_마스크_사용하기/img_5.jpg)

\- 클릭이벤트별 다음과 같이 코딩 합니다

[Source Code]

    
    
            private void 선명화1ToolStripMenuItem_Click(object sender, EventArgs e)
            {
                using (Mask Mk = new Mask())
                using (IplImage temp = Mk.SunMyung1(src))
                {
                    result = temp.Clone();
    
                }
                pictureBoxIpl2.ImageIpl = result;
            }
    
            private void 선명화2ToolStripMenuItem_Click(object sender, EventArgs e)
            {
                using (Mask Mk = new Mask())
                using (IplImage temp = Mk.SunMyung2(src))
                {
                    result = temp.Clone();
    
                }
                pictureBoxIpl2.ImageIpl = result;
            }
    
            private void 선명화3ToolStripMenuItem_Click(object sender, EventArgs e)
            {
                using (Mask Mk = new Mask())
                using (IplImage temp = Mk.SunMyung3(src))
                {
                    result = temp.Clone();
    
                }
                pictureBoxIpl2.ImageIpl = result;
            }
    
            private void 수평엣지ToolStripMenuItem_Click(object sender, EventArgs e)
            {
                using (Mask Mk = new Mask())
                using (IplImage temp = Mk.H_Edge(src))
                {
                    result = temp.Clone();
    
                }
                pictureBoxIpl2.ImageIpl = result;
            }
    
            private void 수직엣ToolStripMenuItem_Click(object sender, EventArgs e)
            {
                using (Mask Mk = new Mask())
                using (IplImage temp = Mk.V_Edge(src))
                {
                    result = temp.Clone();
    
                }
                pictureBoxIpl2.ImageIpl = result;
            }

\- 사용자 지정 마스크 기능을 구현할 Class 파일을 하나 생성 합니다

(클래스 생성 방법은 여러번 포스팅 하였기 때문에 생략 하도록 하겠습니다)

(이전 포스팅 자료를 참고 하시기 바랍니다)

![](/assets/images/c_opencvsharp_사용자_지정_마스크_사용하기/img_6.jpg)

\- 신규로 생성한 클래스 파일에 다음과 같이 코딩 합니다

[Source Code]

    
    
    using System;
    using System.Collections.Generic;
    using System.Text;
    using OpenCvSharp;
    
    namespace OpenCV_V1
    {
        class Mask : IDisposable
        {
            IplImage maskimg;
    
            //세가지 필터로 선명화 시키기
            public IplImage SunMyung1(IplImage src)
            {
                double[,] _b = new double[,]{ {0.0f/5.0f, -1.0f/5.0f, 0.0f/5.0f},
                                              {-1.0f/5.0f, 9.0f/5.0f, -1.0f/5.0f},
                                              {0.0f/5.0f, -1.0f/5.0f, 0.0f/5.0f} };
    
                using (CvMat b = CvMat.FromArray(_b))
                using (IplImage temp = new IplImage(src.Size, BitDepth.U8, 1))
                using (IplImage s1 = new IplImage(src.Size, BitDepth.U8, 1))
                {
                    Cv.CvtColor(src, s1, ColorConversion.BgrToGray);
                    Cv.Filter2D(s1, temp, b, new CvPoint(-1, -1));
                    maskimg = temp.Clone();
                }
                return maskimg;
            }
    
            public IplImage SunMyung2(IplImage src)
            {
                double[,] _b = new double[,]{ {0, -1, 0},
                                              {-1, 5, -1},
                                              {0, -1, 0} };
    
                using (CvMat b = CvMat.FromArray(_b))
                using (IplImage temp = new IplImage(src.Size, BitDepth.U8, 1))
                using (IplImage s1 = new IplImage(src.Size, BitDepth.U8, 1))
                {
                    Cv.CvtColor(src, s1, ColorConversion.BgrToGray);
                    Cv.Filter2D(s1, temp, b, new CvPoint(-1, -1));
                    maskimg = temp.Clone();
    
                }
                return maskimg;
    
            }
    
            public IplImage SunMyung3(IplImage src)
            {
                double[,] _b = new double[,]{ {-1, -1, -1},
                                              {-1, 9, -1},
                                              {-1, -1, -1} };
    
                using (CvMat b = CvMat.FromArray(_b))
                using (IplImage temp = new IplImage(src.Size, BitDepth.U8, 1))
                using (IplImage s1 = new IplImage(src.Size, BitDepth.U8, 1))
                {
                    Cv.CvtColor(src, s1, ColorConversion.BgrToGray);
                    Cv.Filter2D(s1, temp, b, new CvPoint(-1, -1));
                    maskimg = temp.Clone();
    
    
                }
                return maskimg;
    
            }
    
            //수직 엣지 찾기
            public IplImage V_Edge(IplImage src) //그레이 변환된 이미지
            {
                double[,] _b = new double[,]{ {-1, 0, 1},
                                              {-1, 0, 1},
                                              {-1, 0, 1} };
    
    
                using (CvMat b = CvMat.FromArray(_b))
                using (IplImage temp = new IplImage(src.Size, BitDepth.U8, 1))
                using (IplImage s1 = new IplImage(src.Size, BitDepth.U8, 1))
                {
                    Cv.CvtColor(src, s1, ColorConversion.BgrToGray);
                    Cv.Filter2D(s1, temp, b, new CvPoint(-1, -1));
                    Cv.Threshold(temp, temp, 80, 255, ThresholdType.BinaryInv); //이진화
    
                    maskimg = temp.Clone();
    
    
                }
                return maskimg;
            }
    
    
    
            //수평 엣지 찾기
            public IplImage H_Edge(IplImage src)
            {
                double[,] _b = new double[,]{ {1, 1, 1},
                                              {0, 0, 0},
                                              {-1, -1, -1} };
    
    
                using (CvMat b = CvMat.FromArray(_b))
                using (IplImage temp = new IplImage(src.Size, BitDepth.U8, 1))
                using (IplImage s1 = new IplImage(src.Size, BitDepth.U8, 1))
                {
                    Cv.CvtColor(src, s1, ColorConversion.BgrToGray);
                    Cv.Filter2D(s1, temp, b, new CvPoint(-1, -1));
                    Cv.Threshold(temp, temp, 80, 255, ThresholdType.BinaryInv);
    
                    maskimg = temp.Clone();
    
    
                }
                return maskimg;
            }
    
    
    
            public void Dispose()
            {
                if (maskimg != null) Cv.ReleaseImage(maskimg);
            }
        }
    }
    

\- 빌드 후 실행하신뒤 각 기능별 결과를 확인 합니다

[결과 창]  
*선명화1

![](/assets/images/c_opencvsharp_사용자_지정_마스크_사용하기/img_7.jpg)

*선명화2

![](/assets/images/c_opencvsharp_사용자_지정_마스크_사용하기/img_8.jpg)

*선명화3

![](/assets/images/c_opencvsharp_사용자_지정_마스크_사용하기/img_9.jpg)

*수직 엣지

![](/assets/images/c_opencvsharp_사용자_지정_마스크_사용하기/img_10.jpg)

*수평엣지

![](/assets/images/c_opencvsharp_사용자_지정_마스크_사용하기/img_11.jpg)

결과를 보면 약간씩 차이점이 보이실 겁니다

감사합니다

  

#c# #opencv #threshold #opencvsharp #사용자지정마스크 #유저마스크 #Fiter2D


</div>
<div class="lang-panel lang-en" lang="en">
(*No embedded English lines found. Add translations later.*)

</div>
