---
title:  "[2019-12-30] - [C#] OpenCvSharp 이미지처리(회전, 축소, 확대) 하기"
categories:
  - Blog
tags:
  - "c#"
  - "이미지회전"
  - "opencv"
  - "이미지확대"
  - "opencvsharp"
  - "이미지처리"
  - "이미지축소"
last_modified_at: 2025-05-30T16:03:57+09:00
---

## [C#] OpenCvSharp 이미지처리(회전, 축소, 확대) 하기

코딩정보/OpenCv

2019-12-30 15:09:11

* * *

안녕하세요

이번 시간에는 OpenCv를 통한 이미지 회전, 축소, 확대 기능을 만들어 볼려고 합니다

해당 기능을 구현하기 위해서 OpenCvSharp 라이브러리 등록부터 알아봐야 하는데

아래 링크를 통해 확인해 보시기 바랍니다

<https://codingman.tistory.com/49>

[ [C#]OpenCvSharp 라이브러리 사용하기 #1 안녕하세요 저번 포스팅에 C#으로 OpenCvSharp 라이브러리를 등록하여
구현하는 포스팅을 준비하던중에 OpenCv 3,4 버전에서 오류가 발생하는 문제가 있다는 얘길 듣고 부랴부랴 포스팅 내용을 검토해봤는데
역시.. codingman.tistory.com ](https://codingman.tistory.com/49)

그러면 해당 기능을 사용하기 위한 메뉴 등록부터 진행 하겠습니다

[디자인]

\- 다음과 같이 Menu에 이미지처리 -> 회전, 확대, 축소 버튼을 만들어 주세요

![](/assets/images/c_opencvsharp_이미지처리_회전_축소_확대_하기/img.jpg)

\- 각각의 버튼에 클릭이벤트를 생성해 주세요

(이벤트 생성 방법은 여러차례 포스팅하였으므로 생략하도록 할께요)

[Source Code]

-회전 클릭 이벤트
    
    
            private void 회전ToolStripMenuItem_Click(object sender, EventArgs e)
            {
                using (geometry Go = new geometry())
                using (IplImage temp = Go.Affine(src))
                {
                    result = temp.Clone();
    
                }
                pictureBoxIpl2.ImageIpl = result;
    
            }

\- 확대 클릭 이벤트

    
    
            private void 확대ToolStripMenuItem_Click(object sender, EventArgs e)
            {
                using (geometry Go = new geometry())
                using (IplImage temp = Go.MyPyrUp(src))
                {
                    result = temp.Clone();
    
                }
                pictureBoxIpl2.ImageIpl = result;
    
            }

\- 축소 클릭 이벤트

    
    
            private void 축소ToolStripMenuItem_Click(object sender, EventArgs e)
            {
                using (geometry Go = new geometry())
                using (IplImage temp = Go.MyPyrDown(src))
                {
                    result = temp.Clone();
    
                }
                pictureBoxIpl2.ImageIpl = result;
    
            }

[클래스 생성]

\- 이미지처리를 위한 전용 클래스 생성

![](/assets/images/c_opencvsharp_이미지처리_회전_축소_확대_하기/img_1.jpg)

\- 클래스명은 geometry.cs로 지정하였습니다

(클래스명은 굳이 똑같이 하지 않으셔도 됩니다)

![](/assets/images/c_opencvsharp_이미지처리_회전_축소_확대_하기/img.png)

[Source Code]

    
    
    using System;
    using System.Collections.Generic;
    using System.Text;
    using OpenCvSharp;
    
    namespace OpenCV_V1
    {
        class geometry : IDisposable
        {
            IplImage geo;
    
            #region Affine 변환
            //어파인 변환
            public IplImage Affine(IplImage src)
            {
                // cvGetAffineTransform + cvWarpAffine
                // 화상상의 3점에 대응하는 Affine 변환 행렬을 계산, 그 행렬을 이용하여 화상 전체의 Affine 변환을 실시한다.
    
                // (1) 화상을 읽어들이고, 출력용 화상의 메모리를 확보한다
                using (IplImage srcImg = src.Clone())
                using (IplImage dstImg = srcImg.Clone())
                {
                    // (2) 삼각형의 회전전과 회전 후의 대응하는 정점을 각각 세트 해  
                    //    cvGetAffineTransform를 이용해 Affine 행렬을 구한다  
                    CvPoint2D32f[] srcPnt = new CvPoint2D32f[3];
                    CvPoint2D32f[] dstPnt = new CvPoint2D32f[3];
                    srcPnt[0] = new CvPoint2D32f(200.0f, 200.0f);
                    srcPnt[1] = new CvPoint2D32f(250.0f, 200.0f);
                    srcPnt[2] = new CvPoint2D32f(200.0f, 100.0f);
                    dstPnt[0] = new CvPoint2D32f(300.0f, 100.0f);
                    dstPnt[1] = new CvPoint2D32f(300.0f, 50.0f);
                    dstPnt[2] = new CvPoint2D32f(200.0f, 100.0f);
                    using (CvMat mapMatrix = Cv.GetAffineTransform(srcPnt, dstPnt))
                    {
                        // (3) 지정된 어파인 행렬에 의해, cvWarpAffine를 사용해 화상을 회전시킨다
                        Cv.WarpAffine(srcImg, dstImg, mapMatrix, Interpolation.Linear | Interpolation.FillOutliers, CvScalar.ScalarAll(0));
    
                        geo = dstImg.Clone();
    
                    }
                }
                return geo;
            }
            #endregion
    
            #region PyrUpDown
    
    
    
            //이미지의 확대
            public IplImage MyPyrUp(IplImage src)
            {
                using (IplImage srcImg = src.Clone())
                using (IplImage dstImg = new IplImage(srcImg.Width * 2, srcImg.Height * 2, srcImg.Depth, srcImg.NChannels))
                {
                    // (1) 입력 화상에 대한 화상 피라미드를 구성
    
                    Cv.PyrUp(srcImg, dstImg, CvFilter.Gaussian5x5);
                    geo = dstImg.Clone();
    
                }
                return geo;
            }
    
    
    
            //이미지의 축소
    
            public IplImage MyPyrDown(IplImage src)
            {
                using (IplImage srcImg = src.Clone())
                using (IplImage dstImg = new IplImage(srcImg.Width / 2, srcImg.Height / 2, srcImg.Depth, srcImg.NChannels))
                {
                    // (1) 입력 화상에 대한 화상 피라미드를 구성
                    Cv.PyrDown(srcImg, dstImg, CvFilter.Gaussian5x5);
                    geo = dstImg.Clone();
    
                }
                return geo;
            }
    
            #endregion 
    
            public void Dispose()
            {
                if (geo != null) geo.Dispose();
            }
        }
    }
    

[결과 창]

\- 이미지 회전

![](/assets/images/c_opencvsharp_이미지처리_회전_축소_확대_하기/img_2.jpg)

\- 이미지 축소

![](/assets/images/c_opencvsharp_이미지처리_회전_축소_확대_하기/img_3.jpg)

-이미지 확대

![](/assets/images/c_opencvsharp_이미지처리_회전_축소_확대_하기/img_4.jpg)

  

#c# #이미지회전 #opencv #이미지확대 #opencvsharp #이미지처리 #이미지축소

