---
categories:
  - 'Blog'
tags:
  - 'c#'
  - 'opencv'
  - 'opencvsharp'
  - 'FindContours'
  - 'ConvexHull2'
  - '피부색검출'
  - 'DrawContours'
  - 'ConvextyDefect'
  - 'CvBlobs'
  - 'ApproxPoly'
last_modified_at: '2025-05-30T16:03:59+09:00'
title: '[2025-08-13] - Post'
excerpt: ''
layout: 'post'
lang: 'ko'
permalink: '/posts/2020-01-17-c_opencvsharp_이미지_피부색검출하기/'
alt_en: '/en/posts/2020-01-17-c_opencvsharp_이미지_피부색검출하기/'
---

## [C#] OpenCvSharp 이미지 피부색검출하기

코딩정보/OpenCv

2020-01-17 23:22:39

* * *

안녕하세요

이번 포스팅에서는 OpenCvSharp 기능을 통해서 이미지속의 피부색을 검출하고 검출된 영역에

윤곽선을 표기하고 표시된 윤곽선 내부에 포함된 오목 부분을 추가 검출하여 손가락의 구분을

나누어 보도록 하겠습니다

이번 포스팅도 OpenCvSharp 기능 구현 포스팅으로 처음 포스팅 내용과 이어지는 부분이

존재합니다

이해가 잘 되지 않으시다면 앞전 포스팅을 읽어보시고 보신다면 이해가 좀 더 빠를거 같아서

아래 OpenCvSharp의 처음 포스팅을 링크해 드리겠습니다

<https://codingman.tistory.com/49>

[ [C#]OpenCvSharp 라이브러리 사용하기 #1 안녕하세요 저번 포스팅에 C#으로 OpenCvSharp 라이브러리를 등록하여
구현하는 포스팅을 준비하던중에 OpenCv 3,4 버전에서 오류가 발생하는 문제가 있다는 얘길 듣고 부랴부랴 포스팅 내용을 검토해봤는데
역시.. codingman.tistory.com ](https://codingman.tistory.com/49)

[디자인]

\- 메뉴버튼을 생성합니다

![](/assets/images/c_opencvsharp_이미지_피부색검출하기/img.jpg)

-생성한 메뉴에 클릭시 발생할 이벤트를 생성합니다

![](/assets/images/c_opencvsharp_이미지_피부색검출하기/img_1.jpg)

-생성된 클릭 이벤트 부분에 아래와 같이 코딩해줍니다

[Source Code]

    
    
            private void 피부색검출ToolStripMenuItem_Click(object sender, EventArgs e)
            {
                ConvextyDefect Cx = new ConvextyDefect();
                Cx.ConvextyDefectb();
            }

\- 그다음 피부색 검출을 위한 기능 구현을 위해 클래스 파일을 생성합니다

(클래스명칭은 ConvextyDefect.cs로 생성하였습니다.)

![](/assets/images/c_opencvsharp_이미지_피부색검출하기/img_2.jpg)

[Source Code]

    
    
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    using OpenCvSharp;
    using OpenCvSharp.Blob;
    using OpenCvSharp.CPlusPlus;
    using OpenCvSharp.UserInterface;
    
    namespace OpenCV_V1
    {
        class ConvextyDefect
        {
            public void ConvextyDefectb()
            {
                using (IplImage imgSrc = new IplImage("hand.jpg", LoadMode.Color))
                using (IplImage imgHSV = new IplImage(imgSrc.Size, BitDepth.U8, 3))
                using (IplImage imgH = new IplImage(imgSrc.Size, BitDepth.U8, 1))
                using (IplImage imgS = new IplImage(imgSrc.Size, BitDepth.U8, 1))
                using (IplImage imgV = new IplImage(imgSrc.Size, BitDepth.U8, 1))
                using (IplImage imgBackProjection = new IplImage(imgSrc.Size, BitDepth.U8, 1))
                using (IplImage imgFlesh = new IplImage(imgSrc.Size, BitDepth.U8, 1))
                using (IplImage imgHull = new IplImage(imgSrc.Size, BitDepth.U8, 1))
                using (IplImage imgDefect = new IplImage(imgSrc.Size, BitDepth.U8, 3))
                using (IplImage imgContour = new IplImage(imgSrc.Size, BitDepth.U8, 3))
                using (CvMemStorage storage = new CvMemStorage())
                {
                    //RGB -> HSV
                    Cv.CvtColor(imgSrc, imgHSV, ColorConversion.BgrToHsv);
                    Cv.CvtPixToPlane(imgHSV, imgH, imgS, imgV, null);
                    IplImage[] hsvPlanes = { imgH, imgS, imgV };
    
                    //피부색 영역을 구한다
                    RetrieveFleshRegion(imgSrc, hsvPlanes, imgBackProjection);
                    
                    //최대의 면적의 영역을 남긴다
                    FilterByMaximalBolb(imgBackProjection, imgFlesh);
                    Interpolate(imgFlesh);
    
                    //윤곽을 구한다
                    CvSeq<CvPoint> contours = FindContours(imgFlesh, storage);
                    if(contours != null)
                    {
                        Cv.DrawContours(imgContour, contours, CvColor.Red, CvColor.Green, 0, 3, LineType.AntiAlias);
    
                        //요철을 구한다
                        int[] hull;
                        Cv.ConvexHull2(contours, out hull, ConvexHullOrientation.Clockwise);
                        Cv.Copy(imgFlesh, imgHull);
    
                        DrawConvexHull(contours, hull, imgHull);
    
                        //오목한 상태 결손을 구한다
                        Cv.Copy(imgContour, imgDefect);
                        CvSeq<CvConvexityDefect> defect = Cv.ConvexityDefects(contours, hull);
                        DrawDefects(imgDefect, defect);
    
                    }
                    using (new CvWindow("src", imgSrc))
                    using (new CvWindow("back projection", imgBackProjection))
                    using (new CvWindow("hull", imgHull))
                    using (new CvWindow("defect", imgDefect))
                    {
                        Cv.WaitKey();
                    }
                }
            }
    
            ///<summary>
            ///백 프로젝션에 의해 피부색 영역을 구한다
            ///</summary>
            ///<param name="imgSrc"></param>
            ///<param name="hsvPlanes"></param>
            ///<param name="imgDst"></param>
            private void RetrieveFleshRegion(IplImage imgSrc, IplImage[] hsvPlanes, IplImage imgDst)
            {
                int[] histSize = new int[] { 30, 32 };
                float[] hRanges = { 0.0f, 20f };
                float[] sRanges = { 50f, 255f };
                float[][] ranges = { hRanges, sRanges };
                imgDst.Zero();
                using (CvHistogram hist = new CvHistogram(histSize, HistogramFormat.Array, ranges, true))
                {
                    hist.Calc(hsvPlanes, false, null);
                    float minValue, maxValue;
                    hist.GetMinMaxValue(out minValue, out maxValue);
                    hist.Normalize(imgSrc.Width * imgSrc.Height * 255 / maxValue);
                    Cv.CalcBackProject(hsvPlanes, imgDst, hist);
                }
            }
    
            ///<summary>
            ///라벨링에 의해 최대 면적의 영역을 남긴다
            ///</summary>
            ///<param name="imgSrc"></param>
            ///<param name="imgDst"></param>
            private void FilterByMaximalBolb(IplImage imgSrc, IplImage imgDst)
            {
                CvBlobs blobs = new CvBlobs();
    
                imgDst.Zero();
                blobs.Label(imgSrc);
                CvBlob max = blobs.GreaterBlob();
                if (max == null)
                {
                    return;
                }
                blobs.FilterByArea(max.Area, max.Area);
                blobs.FilterLabels(imgDst);
            }
    
            ///<summary>
            ///결손 영역을 보완한다
            ///</summary>
            ///<param name="img"></param>
            private void Interpolate(IplImage img)
            {
                Cv.Dilate(img, img, null, 2);
                Cv.Erode(img, img, null, 2);
            }
    
            ///<summary>
            ///윤곽을 얻는다
            ///</summary>
            ///<param name="img"></param>
            ///<param name="storage"></param>
            ///<returns></returns>
            private CvSeq<CvPoint> FindContours(IplImage img, CvMemStorage storage)
            {
                //윤곽 추출
                CvSeq<CvPoint> contours;
                using (IplImage imgClone = img.Clone())
                {
                    Cv.FindContours(imgClone, storage, out contours);
                    if(contours == null)
                    {
                        return null;
                    }
                    contours = Cv.ApproxPoly(contours, CvContour.SizeOf, storage, ApproxPolyMethod.DP, 3, true);
                }
    
                //제일 긴 것 같은 윤곽만을 얻는다
                CvSeq<CvPoint> max = contours;
                for(CvSeq<CvPoint> c = contours; c != null; c=c.HNext)
                {
                    if(max.Total < c.Total)
                    {
                        max = c;
                    }
                }
                return max;
            }
    
            ///<summary>
            ///ConvexHull 그리기
            ///</summary>
            ///<param name="contours"></param>
            ///<param name="hull"></param>
            ///<param name="img"></param>
            private void DrawConvexHull(CvSeq<CvPoint> contours, int[] hull, IplImage img)
            {
                CvPoint pt0 = contours[hull.Last()].Value;
    
                foreach(int idx in hull)
                {
                    CvPoint pt = contours[idx].Value;
                    Cv.Line(img, pt0, pt, new CvColor(255, 255, 255));
                    pt0 = pt;
                }
    
            }
    
            ///<summary>
            ///ConvexityDefects 그리기
            ///</summary>
            ///<param name="img"></param>
            ///<param name="defect"></param>
            private void DrawDefects(IplImage img, CvSeq<CvConvexityDefect> defect)
            {
                int count = 0;
                foreach(CvConvexityDefect item in defect)
                {
                    CvPoint p1 = item.Start, p2 = item.End;
                    double dist = Getdistance(p1, p2);
                    CvPoint2D64f mid = GetMidpoint(p1, p2);
                    img.DrawLine(p1, p2, CvColor.White, 3);
                    img.DrawCircle(item.DepthPoint, 10, CvColor.Green, -1);
                    img.DrawLine(mid, item.DepthPoint, CvColor.White, 1);
                    Console.WriteLine("No:{0} Depth:{1} Dist:{2}", count, item.Depth, dist);
                    count++;
                }
            }
    
            ///<summary>
            ///2점간의 거리를 얻는다
            ///</summary>
            ///<param name="p1"></param>
            ///<param name="p2"></param>
            ///<returns></returns>
            private double Getdistance(CvPoint p1, CvPoint p2)
            {
                return Math.Sqrt(Math.Pow(p1.X - p2.X, 2) + Math.Pow(p1.Y - p2.Y, 2));
            }
    
            ///<summary>
            ///2점의 중점을 얻는다
            ///</summary>
            ///<param name="p1"></param>
            ///<param name="p2"></param>
            ///<returns></returns>
            private CvPoint2D64f GetMidpoint(CvPoint p1, CvPoint p2)
            {
                return new CvPoint2D64f
                {
                    X = (p1.X + p2.X) / 2.0,
                    Y = (p1.Y + p2.Y) / 2.0
                };
            }
        }
    }
    

\- "hand.jgp"파일은 해당 프로젝트의 Debug 폴더에 넣으시면 되고 예제 파일은 제가 사용한 파일을 업로드

하겠습니다

[ hand.JPG 0.03MB ](./file/hand.JPG)

\- 이렇게 이미지 파일을 넣은 뒤 빌드하여 실행하시면 다음과 같은 결과가 나타나게 됩니다

[결과 창]

*원본이미지

![](/assets/images/c_opencvsharp_이미지_피부색검출하기/img_3.jpg)

* Back projection

![](/assets/images/c_opencvsharp_이미지_피부색검출하기/img_4.jpg)

*hull

![](/assets/images/c_opencvsharp_이미지_피부색검출하기/img_5.jpg)

*defect

![](/assets/images/c_opencvsharp_이미지_피부색검출하기/img_6.jpg)

  

#c# #opencv #opencvsharp #FindContours #ConvexHull2 #피부색검출 #DrawContours
#ConvextyDefect #CvBlobs #ApproxPoly

