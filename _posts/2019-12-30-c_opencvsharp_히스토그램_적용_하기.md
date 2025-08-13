---
categories:
  - 'Blog'
tags:
  - 'c#'
  - 'opencv'
  - '히스토그램'
  - '이미지효과'
  - '이미지필터'
  - 'opencvsharp'
last_modified_at: '2025-05-30T16:03:57+09:00'
title: '[2025-08-13] - Post'
excerpt: ''
layout: 'post'
lang: 'ko'
permalink: '/posts/2019-12-30-c_opencvsharp_히스토그램_적용_하기/'
alt_en: '/en/posts/2019-12-30-c_opencvsharp_히스토그램_적용_하기/'
---

<div class="lang-panel lang-ko" lang="ko">
## [C#] OpenCvSharp 히스토그램 적용 하기

코딩정보/OpenCv

2019-12-30 12:58:33

* * *

안녕하세요

이번 포스팅은 OpenCv를 통한 히스토그램을 확인 할 수 있는 히스토그램 적용하기 입니다

히스토그램이 뭔지 저도 잘 몰랐는데요 이번에 OpenCv를 공부하면서 생소한 이미지 관련 용어들을 많이 접하게 되네요

일단 구글에서 정의하는 히스토그램이란?

**__『도수 분포표의 하나. 가로축에 계급을, 세로축에 도수를 취하고, 도수 분포의 상태를 직사각형의 기둥 모양으로 나타낸 그래프. 주상
도표(柱狀圖表).』__**

이렇게 정의하고 있습니다

무슨말인지..도통 감이 안오는데요.. 그래서 좀 더 구체적으로 검색을 해봤습니다

![](/assets/images/c_opencvsharp_히스토그램_적용_하기/img.png)

역시 어렵네요ㅎㅎ

좀 더 폭풍 검색을 해서 좀 더 이해가 쉬운 포스팅을 가져 왔습니다

1\. 히스토그램이란?

히스토그램은 이미지를 구성하는 픽셀값 분포에 대한 그래프입니다.

X축은 픽셀값으로 범위는 0 ~ 255 사이입니다. Y축은 이미지에서 해당 픽셀값을 가진 픽셀의 개수입니다.

히스토그램의 왼쪽에는 가장 어두운 검은색 픽셀(0)의 갯수를 보여주며 오른쪽으로 갈 수록 밝은

픽셀의 갯수를 보여줍니다.

가장 이해가 되는 값인거 같습니다

여기서 X축과 Y축에 대한 이미지 설명입니다

![](/assets/images/c_opencvsharp_히스토그램_적용_하기/img.jpg)

아마 이미지의 밝기의 분포도를 보기 위한 그래프인거 같습니다

좀 더 자세한 부분은 다음 포스팅을 확인 하시면 좋을거 같습니다

(공개 여부를 확인하지 않고 링크한것이므로 문제가 될 시 삭제 조치 하겠습니다)

<https://webnautes.tistory.com/1274>

[ OpenCV Python 강좌 - 히스토그램(Histogram) 이미지에서 히스토그램을 구하는 방법과 응용으로 Histogram
Equalization, CLAHE을 설명합니다. 다음 OpenCV Python 튜토리얼을 참고하여 강좌를 비정기적로 포스팅하고 있습니다.
https://docs.opencv.org/4.0.0.. webnautes.tistory.com
](https://webnautes.tistory.com/1274)

다시 C#으로 넘어와서 OpenCv로 히스토그램을 적용시켜 보도록 하겠습니다

1\. 메뉴 등록

[디자인]

\- Menu에 다음과 같이 "히스토그램" 메뉴를 등록해 주세요

![](/assets/images/c_opencvsharp_히스토그램_적용_하기/img_1.jpg)

[Source Code]

\- 클릭 이벤트 생성 후 코딩

![](/assets/images/c_opencvsharp_히스토그램_적용_하기/img_2.jpg)

    
    
            private void 히스토그램ToolStripMenuItem_Click(object sender, EventArgs e)
            {
                using (Hist Hi = new Hist())
                using (IplImage temp = Hi.BuildHist(src))
                {
                    result = temp.Clone();
    
                }
                pictureBoxIpl2.ImageIpl = result;
    
            }

2\. 히스토그램을 위한 클래스 생성

\- 클래스 추가 하기

(클래스명은 임의로 설정하셔도 됩니다)

![](/assets/images/c_opencvsharp_히스토그램_적용_하기/img_3.jpg)
![](/assets/images/c_opencvsharp_히스토그램_적용_하기/img_4.jpg)

[Source Code]

    
    
    using System;
    using System.Collections.Generic;
    using System.Text;
    using OpenCvSharp;
    
    namespace OpenCV_V1
    {
        class Hist : IDisposable
        {
            IplImage DstHist;
    
            public IplImage BuildHist(IplImage src)
            {
                const int histSize = 64;
                float[] range0 = { 0, 256 };
                float[][] ranges = { range0 };
    
                // 화상의 읽기
                using (IplImage srcImg = new IplImage(src.Size, BitDepth.U8, 1))
                using (IplImage dstImg = new IplImage(src.Size, BitDepth.U8, 1))
                using (IplImage histImg = new IplImage(new CvSize(400, 400), BitDepth.U8, 1))
                using (CvHistogram hist = new CvHistogram(new int[] { histSize }, HistogramFormat.Array, ranges, true))
                {
                    src.CvtColor(srcImg, ColorConversion.BgrToGray);
                    srcImg.Copy(dstImg);
    
                    using (CvWindow windowImage = new CvWindow("image", WindowMode.AutoSize))
                    using (CvWindow windowHist = new CvWindow("histogram", WindowMode.AutoSize))
                    {
    
                        // 트랙바가 동작되었을 때의 처리
                        CvTrackbar ctBrightness = null;
                        CvTrackbar ctContrast = null;
                        CvTrackbarCallback callback = delegate (int pos)
                        {
                            int brightness = ctBrightness.Pos - 100;
                            int contrast = ctContrast.Pos - 100;
                            // LUT의 적용
                            byte[] lut = CalcLut(contrast, brightness);
                            srcImg.LUT(dstImg, lut);
                            // 히스토그램 그리기
                            CalcHist(dstImg, hist);
                            DrawHist(histImg, hist, histSize);
                            // 윈도우에 표시
                            DstHist = histImg.Clone();
                            windowImage.ShowImage(dstImg);
                            windowHist.ShowImage(histImg);
                            dstImg.Zero();
                            histImg.Zero();
                        };
    
                        // 트랙바의 작성
                        ctBrightness = windowImage.CreateTrackbar("brightness", 100, 200, callback);
                        ctContrast = windowImage.CreateTrackbar("contrast", 100, 200, callback);
                        // 첫회 그리기
                        callback(0);
    
                        // 키 입력대기
                        Cv.WaitKey(0);
                    }
                    return DstHist;
                }
            }
    
            //contrast와 brightness의 값으로부터 LUT의 값을 계산해, byte 배열로 돌려준다
            private static byte[] CalcLut(int contrast, int brightness)
            {
                byte[] lut = new byte[256];
                /*
                 * The algorithm is by Werner D. Streidt
                 * (http://visca.com/ffactory/archives/5-99/msg00021.html)
                 */
                if (contrast > 0)
                {
                    double delta = 127.0 * contrast / 100;
                    double a = 255.0 / (255.0 - delta * 2);
                    double b = a * (brightness - delta);
                    for (int i = 0; i < 256; i++)
                    {
                        int v = Cv.Round(a * i + b);
                        if (v < 0)
                            v = 0;
                        if (v > 255)
                            v = 255;
                        lut[i] = (byte)v;
                    }
                }
                else
                {
                    double delta = -128.0 * contrast / 100;
                    double a = (256.0 - delta * 2) / 255.0;
                    double b = a * brightness + delta;
                    for (int i = 0; i < 256; i++)
                    {
                        int v = Cv.Round(a * i + b);
                        if (v < 0)
                            v = 0;
                        if (v > 255)
                            v = 255;
                        lut[i] = (byte)v;
                    }
                }
                return lut;
            }
            //히스토그램 계산
            private static void CalcHist(IplImage img, CvHistogram hist)
            {
                hist.Calc(img);
                float minValue, maxValue;
                hist.GetMinMaxValue(out minValue, out maxValue);
                Cv.Scale(hist.Bins, hist.Bins, ((double)img.Height) / maxValue, 0);
            }
            //히스토그램 그리기
            private static void DrawHist(IplImage img, CvHistogram hist, int histSize)
            {
                img.Set(CvColor.White);
                int binW = Cv.Round((double)img.Width / histSize);
                for (int i = 0; i < histSize; i++)
                {
                    img.Rectangle(
                        new CvPoint(i * binW, img.Height),
                        new CvPoint((i + 1) * binW, img.Height - Cv.Round(hist.Bins[i])),
                        CvColor.Black, -1, LineType.AntiAlias, 0
                    );
                }
            }
    
            public void Dispose()
            {
                if (DstHist != null) Cv.ReleaseImage(DstHist);
            }
        }
    }
    

[결과창]

![](/assets/images/c_opencvsharp_히스토그램_적용_하기/img_5.jpg)

  

#c# #opencv #히스토그램 #이미지효과 #이미지필터 #opencvsharp


</div>
<div class="lang-panel lang-en" lang="en">
(*No embedded English lines found. Add translations later.*)

</div>
