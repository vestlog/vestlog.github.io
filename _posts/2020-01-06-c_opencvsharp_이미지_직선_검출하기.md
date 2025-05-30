---
title:  "[2020-01-06] - [C#] OpenCvSharp 이미지 직선 검출하기"
categories:
  - Blog
tags:
  - "c#"
  - "opencv"
  - "opencvsharp"
  - "이미지처리"
  - "직선검출"
  - "HoughLines2"
  - "허프변환"
last_modified_at: 2025-05-30T16:03:58+09:00
---

## [C#] OpenCvSharp 이미지 직선 검출하기

코딩정보/OpenCv

2020-01-06 16:52:12

* * *

안녕하세요

이번 포스팅은 저번 포스팅(코너검출)에 이어 직선을 검출하는 기능을 구현해 보도록 하겠습니다

저번 포스팅에 대한 정보를 확인하고자 한다면 아래의 링크를 확인하시기 바랍니다

<https://codingman.tistory.com/60>

[ [C#] OpenCvSharp 이미지 코너 검출하기 안녕하세요 이번 포스팅은 불러온 이미지에서 CornerMinEigenVal을 이용한
코너 검출 그리고 CornerHarris를 이용한 코너 검출을 포스팅 해볼려고 합니다 일단 포스팅을 읽기에 앞서 OpenCvSharp에
대해서 공부하.. codingman.tistory.com ](https://codingman.tistory.com/60)

이번 포스팅에서는 직선 검출을 해볼껀데요

OpenCv에서 직선 검출시 사용할 함수는 바로 HoughLines2()함수 입니다

[함수 설명]

C# : public CvSeq HoughLines2(CvMat lineStorage, HoughLinesMethod method,
double rho, double theta, int threshold, double param1, double param2);

  * lineStorage - 감지 된 라인의 스토리지입니다.
  * method - 허프 변환의 방법을 의미  
HoughLinesMethod.Standard : 기본 허프 변환  
HoughLinesMethod.Probabilistic : 확률적 허프변환, 전체 선이 아닌 선의 일부만 반환함. 선의 일부분은 시작점과
끝정보로 나타난다  
HoughLinesMethod.MultiScale : 기본 허프 변환에서 멀티 스케일 변형

  * rho - 필셀 단위로 나타나는 거리 값
  * theta - 라디안 단위로 나타나는 각도 값
  * threshold - 임계값, 해당 축적 값이 해당 값보다 크면 Line이 출력된다
  * param1 - 파라미터  
기본 허프 변환에서는 이 값이 사용되지 않는다  
Probabilistic 허프 변환에서는 선 길이의 최소 값을 나타낸다  
MultiScale 허프 변환에서는 거리 값에 대한 나누는 수를 의미한다  

  * param2 - 파라미터  
기본 허프 변환에서는 이 값이 사용되지 않는다  
Probabilistic 허프 변환에서는 선들 사이의 최대 갭을 의미한다  
MultiScale 허프 변환에서는 각도에 대한 나누는 수를 의미한다  

주요 함수 설명은 위와 같습니다 그럼 이제 구현을 하기 위한 디자인을 해보겟습니다

[디자인]

\- 메인폼의 Menu트립에서 다음과 같이 디자인 합니다

![](/assets/images/c_opencvsharp_이미지_직선_검출하기/img.jpg)

\- 해당 Menu 트립의 항목의 클릭 이벤트 설정

![](/assets/images/c_opencvsharp_이미지_직선_검출하기/img_1.jpg)

\- 클릭이벤트에 다음과 같은 코딩은 합니다

[Source Code]

    
    
            private void 허프직선ToolStripMenuItem_Click(object sender, EventArgs e)
            {
                using (hough Hg = new hough())
                using (IplImage temp = Hg.HoughLines(src))
                {
                    result = temp.Clone();
    
                }
                pictureBoxIpl2.ImageIpl = result;
    
            }

\- 직선 검출을 위한 Class파일을 생성합니다

(저는 Class명칭을 다음과 같이 hough.cs로 생성하엿습니다)

![](/assets/images/c_opencvsharp_이미지_직선_검출하기/img_2.jpg)

[Class Source Code]

    
    
    using System;
    using System.Collections.Generic;
    using System.Text;
    using OpenCvSharp;
    
    namespace OpenCV_V1
    {
        class hough : IDisposable
        {
            IplImage houghLine;
    
            public IplImage HoughLines(IplImage src)
            {
                // cvHoughLines2
                // 확률적 허프 변환을 지정해 선분의 검출을 실시한다
    
                // (1) 화상 읽기 
                using (IplImage srcImgStd = src.Clone())
                using (IplImage srcImgGray = new IplImage(src.Size, BitDepth.U8, 1))
                {
                    Cv.CvtColor(srcImgStd, srcImgGray, ColorConversion.BgrToGray);
    
                    // (2) 허프변환을 위한 캐니엣지 처리 
                    Cv.Canny(srcImgGray, srcImgGray, 50, 200, ApertureSize.Size3);
    
                    using (CvMemStorage storage = new CvMemStorage())
                    {
    
    
                        // (3) 표준적 허프 변환에 의한 선의 검출과 검출된 선 그리기
                        CvSeq lines = srcImgGray.HoughLines2(storage, HoughLinesMethod.MultiScale, 1, Math.PI / 180, 50, 0, 0);
                        int limit = Math.Min(lines.Total, 10);
                        for (int i = 0; i < limit; i++)
                        {
    
                            CvLineSegmentPolar elem = lines.GetSeqElem<CvLineSegmentPolar>(i).Value;
                            float rho = elem.Rho;
                            float theta = elem.Theta;
    
                            double a = Math.Cos(theta);
                            double b = Math.Sin(theta);
                            double x0 = a * rho;
                            double y0 = b * rho;
                            CvPoint pt1 = new CvPoint { X = Cv.Round(x0 + 1000 * (-b)), Y = Cv.Round(y0 + 1000 * (a)) };
                            CvPoint pt2 = new CvPoint { X = Cv.Round(x0 - 1000 * (-b)), Y = Cv.Round(y0 - 1000 * (a)) };
                            srcImgStd.Line(pt1, pt2, CvColor.Red, 3, LineType.AntiAlias, 0);
                        }
    
                        houghLine = srcImgStd.Clone();
                    }
    
                }
                return houghLine;
            }
    
    
            public void Dispose()
            {
                if (houghLine != null) Cv.ReleaseImage(houghLine);
            }
        }
    }
    

이렇게 Class파일까지 생성한 뒤 실행해서 확인해보면 다음과 같은 결과가 나타납니다

[결과 창]

![](/assets/images/c_opencvsharp_이미지_직선_검출하기/img_3.jpg)

이미지에서 Line을 검출하여 표시하는데 이미지처리를 하지 않고 원본 파일에서 그냥 검출 시도를 했을 경우

다음과 같이 인식율이 상당히 이상하게 나오네요

아마 인식율을 높이기 위해서는 이미지처리(흑백전환 및 픽셀 전환, 등)을 통해 직선을 좀 더 명확하게

구별할 수 있도록 변경한 후에 처리시키는게 좋을거 같네요

  

#c# #opencv #opencvsharp #이미지처리 #직선검출 #HoughLines2 #허프변환

