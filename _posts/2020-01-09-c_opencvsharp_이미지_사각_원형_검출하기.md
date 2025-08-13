---
categories:
  - 'Blog'
tags:
  - 'c#'
  - 'opencv'
  - '컨투어'
  - '윤곽선'
  - 'opencvsharp'
  - '모형검출'
  - '사각형검출'
  - '원형검출'
  - '이미지'
last_modified_at: '2025-05-30T16:03:58+09:00'
title: '[2025-08-13] - Post'
excerpt: ''
layout: 'post'
lang: 'ko'
permalink: '/posts/2020-01-09-c_opencvsharp_이미지_사각_원형_검출하기/'
alt_en: '/en/posts/2020-01-09-c_opencvsharp_이미지_사각_원형_검출하기/'
---

## [C#] OpenCvSharp 이미지 사각, 원형 검출하기

코딩정보/OpenCv

2020-01-09 12:15:04

* * *

안녕하세요

"코딩연습생"입니다ㅎㅎ

저번 포스팅에서 컨투어(윤곽선) 검출을 포스팅 했었는데요

<https://codingman.tistory.com/65>

[ [C#] OpenCvSharp 이미지 컨투어(윤곽선) 찾기 안녕하세요 요즘은 매일 OpenCvSharp 포스팅 자료 만들기 하는냐고
하루가 다 가는거 같네요 인터넷을 보고 따라하고 분석하고 오류 수정하고 그러고 실행해서 결과 분석하고 그 과정을 캡쳐 캡쳐 하여 포스팅
준.. codingman.tistory.com ](https://codingman.tistory.com/65)

컨투어 찾기 기능을 통해 모형이나 특정 조건에 의한 영역의 윤곽선을 찾기를 해볼려고 합니다

그래서 이번 포스팅에서 준비한것은 이미지의 사각, 원형에 대한 특정 조건을 검출하여 윤곽선을

표기 해보도록 하겠습니다

역시나 연속적인 OpenCvSharp 포스팅을 진행하고 있기에 기초 설정이라든지 공통 디자인 부분같은 경우

생략하고 진행하고 있습니다

불편하시더라도 기존 포스팅을 찾아 확인하신 다음에 이어 준비한 내용을 보시길 바랍니다

<https://codingman.tistory.com/49>

[ [C#]OpenCvSharp 라이브러리 사용하기 #1 안녕하세요 저번 포스팅에 C#으로 OpenCvSharp 라이브러리를 등록하여
구현하는 포스팅을 준비하던중에 OpenCv 3,4 버전에서 오류가 발생하는 문제가 있다는 얘길 듣고 부랴부랴 포스팅 내용을 검토해봤는데
역시.. codingman.tistory.com ](https://codingman.tistory.com/49)

그럼 시작해보도록 하겠습니다

언제나 처럼 사각,원형을 검출하기 위한 버튼이 있어야 겠죠?

[디자인]

\- 메뉴에서 다음과 같이 버튼 메뉴를 생성합니다

![](/assets/images/c_opencvsharp_이미지_사각_원형_검출하기/img.jpg)

\- 생성된 버튼에 클릭 했을때 동작 할 수 있도록 클릭 이벤트를 설정해 줍니다

![](/assets/images/c_opencvsharp_이미지_사각_원형_검출하기/img_1.jpg)
![](/assets/images/c_opencvsharp_이미지_사각_원형_검출하기/img_2.jpg)

\- 여기까지는 그렇게 어렵지 않습니다

[Source Code]

    
    
            private void 사각형찾기ToolStripMenuItem_Click(object sender, EventArgs e)
            {
                if (src == null) return;
                using (Squre Sq = new Squre())
                using (IplImage temp = Sq.Squares(src))
                {
                    result = temp.Clone();
    
                }
                pictureBoxIpl2.ImageIpl = result;
            }
    
            private void 원형찾기ToolStripMenuItem_Click(object sender, EventArgs e)
            {
                if (src == null) return;
                using (Squre Sq = new Squre())
                using (IplImage temp = Sq.HoughCircles(src))
                {
                    result = temp.Clone();
    
                }
                pictureBoxIpl2.ImageIpl = result;
            }

\- 다음에 사각과 원형을 검출해주고 그 위에 윤곽선을 그려줄 기능을 할 클래스를 작성 할께요

![](/assets/images/c_opencvsharp_이미지_사각_원형_검출하기/img_3.jpg)

\- 생성된 클래스 파일에 아래와 같이 소스코드를 생성해 줍니다

    
    
    using System;
    using System.Collections.Generic;
    using System.Text;
    using OpenCvSharp;
    
    namespace OpenCV_V1
    {
        class Squre : IDisposable
        {
            const int Thresh = 50;
            IplImage squr;
    
            static double Angle(CvPoint pt1, CvPoint pt2, CvPoint pt0)
            {
                double dx1 = pt1.X - pt0.X;
                double dy1 = pt1.Y - pt0.Y;
                double dx2 = pt2.X - pt0.X;
                double dy2 = pt2.Y - pt0.Y;
                return (dx1 * dx2 + dy1 * dy2) / Math.Sqrt((dx1 * dx1 + dy1 * dy1) * (dx2 * dx2 + dy2 * dy2) + 1e-10);
            }
    
            public IplImage Squares(IplImage src)
            {
    
                CvMemStorage storage = new CvMemStorage(0);
                DrawSquares(src, FindSquares4(src, storage));
                return squr;
    
            }
    
            //원형 검출
            public IplImage HoughCircles(IplImage src)
            {
                squr = new IplImage(src.Size, BitDepth.U8, 3);
                IplImage gray = new IplImage(src.Size, BitDepth.U8, 1);
    
                Cv.Copy(src, squr);
                Cv.CvtColor(src, gray, ColorConversion.BgrToGray);
                Cv.Smooth(gray, gray, SmoothType.Gaussian, 9);
    
                CvMemStorage Storage = new CvMemStorage();
                CvSeq<CvCircleSegment> circles = Cv.HoughCircles(gray, Storage, HoughCirclesMethod.Gradient, 1, 100, 150, 50, 0, 0);
    
                foreach (CvCircleSegment item in circles)
                {
                    Cv.Circle(squr, item.Center, (int)item.Radius, CvColor.Blue, 3);
                }
                return squr;
            }
    
            //사각 검출
            static CvPoint[] FindSquares4(IplImage img, CvMemStorage storage)
            {
                const int N = 11;
    
                CvSize sz = new CvSize(img.Width & -2, img.Height & -2);
                IplImage timg = img.Clone(); // make a copy of input image
                IplImage gray = new IplImage(sz, BitDepth.U8, 1);
                IplImage pyr = new IplImage(sz.Width / 2, sz.Height / 2, BitDepth.U8, 3);
                // create empty sequence that will contain points -
                // 4 points per square (the square's vertices)
                CvSeq<CvPoint> squares = new CvSeq<CvPoint>(SeqType.Zero, CvSeq.SizeOf, storage);
    
                // select the maximum ROI in the image
                // with the width and height divisible by 2
                timg.ROI = new CvRect(0, 0, sz.Width, sz.Height);
    
                // down-scale and upscale the image to filter out the noise
                Cv.PyrDown(timg, pyr, CvFilter.Gaussian5x5);
                Cv.PyrUp(pyr, timg, CvFilter.Gaussian5x5);
                IplImage tgray = new IplImage(sz, BitDepth.U8, 1);
    
                // find squares in every color plane of the image
                for (int c = 0; c < 3; c++)
                {
                    // extract the c-th color plane
                    timg.COI = c + 1;
                    Cv.Copy(timg, tgray, null);
    
                    // try several threshold levels
                    for (int l = 0; l < N; l++)
                    {
                        // hack: use Canny instead of zero threshold level.
                        // Canny helps to catch squares with gradient shading   
                        if (l == 0)
                        {
                            // apply Canny. Take the upper threshold from slider
                            // and set the lower to 0 (which forces edges merging) 
                            Cv.Canny(tgray, gray, 0, Thresh, ApertureSize.Size5);
                            // dilate canny output to remove potential
                            // holes between edge segments 
                            Cv.Dilate(gray, gray, null, 1);
                        }
                        else
                        {
                            // apply threshold if l!=0:
                            //     tgray(x,y) = gray(x,y) < (l+1)*255/N ? 255 : 0
                            Cv.Threshold(tgray, gray, (l + 1) * 255.0 / N, 255, ThresholdType.Binary);
                        }
    
                        // find contours and store them all as a list
                        CvSeq<CvPoint> contours;
                        Cv.FindContours(gray, storage, out contours, CvContour.SizeOf, ContourRetrieval.List, ContourChain.ApproxSimple, new CvPoint(0, 0));
    
                        // test each contour
                        while (contours != null)
                        {
                            // approximate contour with accuracy proportional
                            // to the contour perimeter
                            CvSeq<CvPoint> result = Cv.ApproxPoly(contours, CvContour.SizeOf, storage, ApproxPolyMethod.DP, contours.ContourPerimeter() * 0.02, false);
                            // square contours should have 4 vertices after approximation
                            // relatively large area (to filter out noisy contours)
                            // and be convex.
                            // Note: absolute value of an area is used because
                            // area may be positive or negative - in accordance with the
                            // contour orientation
                            if (result.Total == 4 && Math.Abs(result.ContourArea(CvSlice.WholeSeq)) > 1000 && result.CheckContourConvexity())
                            {
                                double s = 0;
    
                                for (int i = 0; i < 5; i++)
                                {
                                    // find minimum Angle between joint
                                    // edges (maximum of cosine)
                                    if (i >= 2)
                                    {
                                        double t = Math.Abs(Angle(result[i].Value, result[i - 2].Value, result[i - 1].Value));
                                        s = s > t ? s : t;
                                    }
                                }
    
                                // if cosines of all angles are small
                                // (all angles are ~90 degree) then write quandrange
                                // vertices to resultant sequence 
                                if (s < 0.3)
                                {
                                    for (int i = 0; i < 4; i++)
                                    {
                                        //Console.WriteLine(result[i]);
                                        squares.Push(result[i].Value);
                                    }
                                }
                            }
    
                            // take the next contour
                            contours = contours.HNext;
                        }
                    }
                }
    
                // release all the temporary images
                gray.Dispose();
                pyr.Dispose();
                tgray.Dispose();
                timg.Dispose();
    
                return squares.ToArray();
            }
    
    
            /// <summary>
            /// the function draws all the squares in the image
            /// </summary>
            /// <param name="img"></param>
            /// <param name="squares"></param>
            private void DrawSquares(IplImage img, CvPoint[] squares)
            {
                using (IplImage cpy = img.Clone())
                {
                    // read 4 sequence elements at a time (all vertices of a square)
                    for (int i = 0; i < squares.Length; i += 4)
                    {
                        CvPoint[] pt = new CvPoint[4];
    
                        // read 4 vertices
                        pt[0] = squares[i + 0];
                        pt[1] = squares[i + 1];
                        pt[2] = squares[i + 2];
                        pt[3] = squares[i + 3];
    
                        // draw the square as a closed polyline 
                        Cv.PolyLine(cpy, new CvPoint[][] { pt }, true, CvColor.Green, 3, LineType.AntiAlias, 0);
    
                    }
    
                    // show the resultant image
                    squr = cpy.Clone();
                }
            }
    
    
            public void Dispose()
            {
                if (squr != null) Cv.ReleaseImage(squr);
            }
        }
    }
    

\- 사실 이렇게 많은 소스코드 중에 핵심 함수는 두가지 밖에 없습니다

(제가 아는 범위에서 말씀드리는것이기 때문에 사실과 다를수 있습니다);;ㅎㅎ

*원형을 찾기 위한 함수 HoughCircles

*사각을 찾기 위한 함수 ApproxPoly

[결과 창]

*원형 검출 (검출 인식율 : 70%)

![](/assets/images/c_opencvsharp_이미지_사각_원형_검출하기/img_4.jpg)

*사각 검출(인식율 : 90%)

![](/assets/images/c_opencvsharp_이미지_사각_원형_검출하기/img_5.jpg)

이 두가지 함수를 공부 하시고 응용하시면 5각형, 6각형의 다각형 모형도 검출이 가능하니

공부해서 응용해보시면 좋을거 같아요

혹시 공부하시고 터득하신 정보가 있으시다면 공유 해주시기 바랍니다

감사합니다

  

#c# #opencv #컨투어 #윤곽선 #opencvsharp #모형검출 #사각형검출 #원형검출 #이미지 검출

