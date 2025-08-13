---
categories:
  - 'Blog'
tags:
  - 'c#'
  - 'RGB'
  - 'opencv'
  - 'Math.Round'
  - 'opencvsharp'
  - '픽셀변환'
  - 'CvColor'
last_modified_at: '2025-05-30T16:03:59+09:00'
title: '[2025-08-13] - Post'
excerpt: ''
layout: 'post'
lang: 'ko'
permalink: '/posts/2020-01-16-c_opencvsharp_이미지_픽셀변환_시키기/'
alt_en: '/en/posts/2020-01-16-c_opencvsharp_이미지_픽셀변환_시키기/'
---

## [C#] OpenCvSharp 이미지 픽셀변환 시키기

코딩정보/OpenCv

2020-01-16 14:33:51

* * *

안녕하세요

벌써 OpenCv에 대해 연구한지 꽤 시간이 흘렀습니다

점점 난이도가 올라가면서 포스팅 자료 만드는 시간이 오래 걸리고 있습니다ㅠ

쉬운 기능만 구현하기에는 연습에 의미가 없고...

그렇다고 재미있는 기능을 따라가자니 너무 어렵고...ㅎㅎㅎ

그래도 존버는 승리한다는 말이 있듯이 포기하지말고 힘내서 차근차근 하나씩 도전 해보도록 하겠습니다

이번 업로드할 포스팅 주제는 픽셀변환입니다

OpenCvSharp의 함수중 CvColor을 사용하여 R,G,B 영역을 변경시켜 전체영역의 색상을 변경 시키는 것인데요

기존에 포스팅했던 것을 쭉 같이 봐오셨다면 그렇게 어렵게 느껴지지는 않을거 같습니다

이전 자료는 블로그 내에서 찾아보시거나 아래 링크를 확인하시면 찾기 쉽습니다

<https://codingman.tistory.com/49>

[ [C#]OpenCvSharp 라이브러리 사용하기 #1 안녕하세요 저번 포스팅에 C#으로 OpenCvSharp 라이브러리를 등록하여
구현하는 포스팅을 준비하던중에 OpenCv 3,4 버전에서 오류가 발생하는 문제가 있다는 얘길 듣고 부랴부랴 포스팅 내용을 검토해봤는데
역시.. codingman.tistory.com ](https://codingman.tistory.com/49)

그러면 픽셀변환에 대해서 포스팅 시작하겠습니다

처음에 디자인으로 버튼 생성 부터 포스팅 할꼐요

[디자인]

\- 필터 메뉴에서 하부메뉴로 필셀변환이라고 등록합니다

![](/assets/images/c_opencvsharp_이미지_픽셀변환_시키기/img.jpg)

\- 그다음 픽셀변환 버튼에 클릭시 발생할 이벤트를 생성합니다

![](/assets/images/c_opencvsharp_이미지_픽셀변환_시키기/img_1.jpg)

\- 클릭 이벤트 발생시 시행될 코드는 다음과 같습니다

    
    
            private void 픽셀변환ToolStripMenuItem_Click(object sender, EventArgs e)
            {
                if (src == null) return;
                using (pix Px = new pix())
                using (IplImage temp = Px.PixelAccess(src))
                {
                    result = temp.Clone();
    
                }
                pictureBoxIpl2.ImageIpl = result;
            }

\- 그리고 필셀변환 기능을 수행할 클래스를 생성해야 겠지요?

![](/assets/images/c_opencvsharp_이미지_픽셀변환_시키기/img_2.jpg)

\- 저는 Pix.cs라는 명칭으로 생성하였습니다

[pix.cs Source Code]

    
    
    using System;
    using System.Collections.Generic;
    using System.Text;
    using OpenCvSharp;
    
    namespace OpenCV_V1
    {
        class pix : IDisposable
        {
            IplImage Px;
    
            public IplImage PixelAccess(IplImage src)
            {
    
                using (IplImage img = src.Clone())
                {
                    // (1) 픽셀 데이타(R,G,B)를 차례차례 취득해, 변경한다
                    // 저속이지만 간단한 방법
    
                    for (int y = 0; y < img.Height; y++)
                    {
                        for (int x = 0; x < img.Width; x++)
                        {
                            CvColor c = img[y, x];
                            img[y, x] = new CvColor
                            {
                                B = (byte)Math.Round(c.B * 0.7 + 10),
                                G = (byte)Math.Round(c.G * 1.0),
                                R = (byte)Math.Round(c.R * 0.0),
                            };
                        }
                    }
    
    
                    /*
                    // 포인터를 사용한 고속의 방법
                    unsafe
                    {
                        byte* ptr = (byte*) img.ImageData;    // 화소 데이터에의 포인터
                        for (int y = 0; y < img.Height; y++)
                        {
                            for (int x = 0; x < img.Width; x++)
                            {
                                int offset = (img.WidthStep * y) + (x * 3);
                                byte b = ptr[offset + 0];    // B
                                byte g = ptr[offset + 1];    // G
                                byte r = ptr[offset + 2];    // R
                                ptr[offset + 0] = (byte)Math.Round(b * 0.7 + 10);
                                ptr[offset + 1] = (byte)Math.Round(g * 1.0);
                                ptr[offset + 2] = (byte)Math.Round(r * 0.0);
                            }
                        }
                    }
                    //*/
                    /*
                    // unsafe는 아니고 IntPtr로 시도한 방법 (VB.NET 방향)
                    
                        IntPtr ptr = img.ImageData;
                        for (int y = 0; y < img.Height; y++)
                        {
                            for (int x = 0; x < img.Width; x++)
                            {
                                int offset = (img.WidthStep * y) + (x * 3);
                                byte b = Marshal.ReadByte(ptr, offset + 0);    // B
                                byte g = Marshal.ReadByte(ptr, offset + 1);    // G
                                byte r = Marshal.ReadByte(ptr, offset + 2);    // R
                                Marshal.WriteByte(ptr, offset + 0, (byte)Math.Round(b * 0.7 + 10));
                                Marshal.WriteByte(ptr, offset + 1, (byte)Math.Round(g * 1.0));
                                Marshal.WriteByte(ptr, offset + 2, (byte)Math.Round(r * 0.0));
                            }
                        }
                    
                    //*/
                    //*/
    
                    Px = img.Clone();
                    return Px;
    
                }
            }
            public void Dispose()
            {
                if (Px != null) Cv.ReleaseImage(Px);
            }
        }
    }
    

\- 이렇게 클래스 생성과 코딩까지 완료 하셨다면 빌드 하시고 실행시켜 픽셀변환을 실행해 보세요

[결과 창]

![](/assets/images/c_opencvsharp_이미지_픽셀변환_시키기/img_3.jpg)

  

#c# #RGB #opencv #Math.Round #opencvsharp #픽셀변환 #CvColor

