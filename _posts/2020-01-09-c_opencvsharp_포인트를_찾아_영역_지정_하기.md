---
title:  "[2020-01-09] - [C#] OpenCvSharp 포인트를 찾아 영역 지정 하기"
categories:
  - Blog
tags:
  - "Rectangle"
  - "c#"
  - "opencv"
  - "opencvsharp"
  - "BoundingRect"
  - "사각그리기"
last_modified_at: 2025-05-30T16:03:58+09:00
---

## [C#] OpenCvSharp 포인트를 찾아 영역 지정 하기

코딩정보/OpenCv

2020-01-09 13:45:48

* * *

안녕하세요

이번 포스팅은 저번 포스팅에 이어서 랜덤 포인터로 점을 그리고 그 점들을 모두 포함하는 사각형을

그리는 방법을 포스팅 할려고 합니다

포인터 영역 지정을 할때 응용하면 참 좋을거 같은데요

저번 포스팅에서 사용한 원형, 사각형 검출 포스팅에 이어져서 보시면 좋을거 같습니다

<https://codingman.tistory.com/66>

[ [C#] OpenCvSharp 이미지 사각, 원형 검출하기 안녕하세요 "코딩연습생"입니다ㅎㅎ 저번 포스팅에서 컨투어(윤곽선) 검출을
포스팅 했었는데요 https://codingman.tistory.com/65 [C#] OpenCvSharp 이미지 컨투어(윤곽선) 찾기
안녕하세요 요즘은 매일 OpenCvSh.. codingman.tistory.com
](https://codingman.tistory.com/66)

반복 내용은 생략하고 진행 하도록 할께요

[디자인]

\- 아래 이미지와 같이 메뉴를 생성해 주세요

![](/assets/images/c_opencvsharp_포인트를_찾아_영역_지정_하기/img.jpg)

\- 생성된 메뉴에 클릭 이벤트 지정

![](/assets/images/c_opencvsharp_포인트를_찾아_영역_지정_하기/img_1.jpg)

[Source Code]

    
    
            private void 바운딩ToolStripMenuItem_Click(object sender, EventArgs e)
            {
    
                CvWindow wind = new CvWindow("결과창");
                Bounding Bd = new Bounding();
                Bd.BoundingRect(this.pictureBoxIpl1, this.pictureBoxIpl2, wind);
                
            }

\- 임의 점과 점들을 포함하는 사각형을 그리기 위한 클래스 생성

![](/assets/images/c_opencvsharp_포인트를_찾아_영역_지정_하기/img_2.jpg)

[Source Code]

    
    
    using System;
    using System.Collections.Generic;
    using System.Text;
    using OpenCvSharp;
    using OpenCvSharp.UserInterface;
    
    namespace OpenCV_V1
    {
        class Bounding
        {
            public void BoundingRect(PictureBoxIpl p1, PictureBoxIpl p2, CvWindow wind)
            {
                // cvBoundingRect 
                // 점렬을 포함 하는 사각형을 구한다
    
                // (1) 화상과 메모리스트레이지를 확보해 초기화한다
                using (IplImage img = new IplImage(640, 480, BitDepth.U8, 3))
                using (CvMemStorage storage = new CvMemStorage(0))
                {
                    img.Zero();
                    CvRNG rng = new CvRNG(DateTime.Now);
                    // (2) 점렬을 생성한다
                    ///*
                    // 간단한 방법 (보통 배열을 사용한다)
                    CvPoint[] points = new CvPoint[50];
                    for (int i = 0; i < 50; i++)
                    {
                        points[i] = new CvPoint()
                        {
                            X = (int)(rng.RandInt() % (img.Width / 2) + img.Width / 4),
                            Y = (int)(rng.RandInt() % (img.Height / 2) + img.Height / 4)
                        };
                        img.Circle(points[i], 3, new CvColor(0, 255, 0), Cv.FILLED);
                    }
    
                    p1.ImageIpl = img;
    
                    // (3) 점렬을 포함 하는 사각형을 구해 그린다
                    CvRect rect = Cv.BoundingRect(points);
                    img.Rectangle(new CvPoint(rect.X, rect.Y), new CvPoint(rect.X + rect.Width, rect.Y + rect.Height), new CvColor(255, 0, 0), 2);
    
                    p2.ImageIpl = img;
                    wind.Image = img;
    
                }
            }
        }
    }
    

\- 빌드 후 오류 없이 빌드가 된다면 실행 하게 되면 다음과 같은 결과가 나타납니다

[결과 창]

![](/assets/images/c_opencvsharp_포인트를_찾아_영역_지정_하기/img_3.jpg)

  

#Rectangle #c# #opencv #opencvsharp #BoundingRect #사각그리기

