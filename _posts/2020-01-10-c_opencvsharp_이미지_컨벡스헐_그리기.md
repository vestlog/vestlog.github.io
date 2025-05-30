---
title:  "[2020-01-10] - [C#] OpenCvSharp 이미지 컨벡스헐 그리기"
categories:
  - Blog
tags:
  - "c#"
  - "opencv"
  - "Hull"
  - "opencvsharp"
  - "컨벡스헐"
  - "점선그리기"
  - "ConvexHull2"
  - "점선연결하기"
  - "외곽선그리기"
last_modified_at: 2025-05-30T16:03:58+09:00
---

## [C#] OpenCvSharp 이미지 컨벡스헐 그리기

코딩정보/OpenCv

2020-01-10 13:06:41

* * *

안녕하세요

저번 포스팅에서 점멸을 포함하는 사각형 그리기에 대해 포스팅 했었는데요

<https://codingman.tistory.com/67>

[ [C#] OpenCvSharp 포인트를 찾아 영역 지정 하기 안녕하세요 이번 포스팅은 저번 포스팅에 이어서 랜덤 포인터로 점을 그리고 그
점들을 모두 포함하는 사각형을 그리는 방법을 포스팅 할려고 합니다 포인터 영역 지정을 할때 응용하면 참 좋을거 같은데요 저번..
codingman.tistory.com ](https://codingman.tistory.com/67)

이번 포스팅에서는 형태와 상관없이 외곽 점들을 연결시켜 영역을 지정하는것을 해볼려고 합니다

OpenCvSharp 함수 중에 ConvexHull2 이라는 함수를 사용해서 구현을 해볼려고 합니다

이번 포스팅 역시 OpenCvSharp를 이어서 진행 되니 처음 시작 하시는 분의 경우 앞 포스팅을 확인하시기

바랍니다

<https://codingman.tistory.com/49>

[ [C#]OpenCvSharp 라이브러리 사용하기 #1 안녕하세요 저번 포스팅에 C#으로 OpenCvSharp 라이브러리를 등록하여
구현하는 포스팅을 준비하던중에 OpenCv 3,4 버전에서 오류가 발생하는 문제가 있다는 얘길 듣고 부랴부랴 포스팅 내용을 검토해봤는데
역시.. codingman.tistory.com ](https://codingman.tistory.com/49)

처음에 할 것을 역시 버튼 만들기 겠죠?

[디자인]

\- Menu에서 다음과 같이 메뉴를 등록시켜 주세요

![](/assets/images/c_opencvsharp_이미지_컨벡스헐_그리기/img.jpg)

\- 다음은 컨벡스 헐이라는 메뉴를 클릭 했을때 동작 할 수 있도록 클릭 이벤트를 생성 합니다

![](/assets/images/c_opencvsharp_이미지_컨벡스헐_그리기/img_1.jpg)

\- 클릭 이벤트를 생성한뒤 해당 이벤트 발생 지점에 다음과 같으 코딩을 해줍니다

    
    
            private void 컨벡스헐ToolStripMenuItem_Click(object sender, EventArgs e)
            {
                CvWindow wind = new CvWindow("결과창");
                convex Cx = new convex();
                Cx.ConvexHull(this.pictureBoxIpl1, this.pictureBoxIpl2, wind);
            }

\- 랜덤 점 생성과 생성된 점들의 외곽을 구하고 그 외곽을 연결시키는 기능을 실행할 클래스를 생성합니다

(클래스 파일 생성은 첫 포스팅에서 확인하세요)

![](/assets/images/c_opencvsharp_이미지_컨벡스헐_그리기/img_2.jpg)

\- 생성된 클래스 파일에 다음과 같은 기능을 할 코딩 소스를 넣어 짭니다

(오류 수정과 테스트로 인한 주석이 존재하니 양해 바랍니다)

    
    
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    using OpenCvSharp;
    using OpenCvSharp.UserInterface;
    
    namespace OpenCV_V1
    {
        class convex
        {
            IplImage _dst;
    
            public void ConvexHull(PictureBoxIpl p1, PictureBoxIpl p2, CvWindow wind)
            {
    
                IplImage img = Cv.CreateImage(new CvSize(500, 500), BitDepth.U8, 3);
                Random rand = new Random();
    
                int count = rand.Next() % 100 + 1;
    
                //임의의 점 생성
                CvPoint[] ptseq = new CvPoint[count];
                for (int i = 0; i < count; i++)
                {
                    ptseq[i] = new CvPoint
                    {
                        X = rand.Next() % (img.Width),
                        Y = rand.Next() % (img.Height)
                    };
    
                    /*
                    CvPoint pt = new CvPoint
                    {
                        X = rand.Next() % (img.Width / 2) + img.Width / 4,
                        Y = rand.Next() % (img.Height / 2) + img.Height / 4
                    };
                    Cv.SeqPush<CvPoint>(ptseq, pt);
                    */
                }
    
    
                // 점 그리기
                Cv.Zero(img);
                foreach(CvPoint pt in ptseq)
                {
                    Cv.Circle(img, pt, 2, new CvColor(255, 0, 0), -1);
                }
    
                /*
                for (int i = 0; i < count; i++)
                {
                    CvPoint pt = Cv.GetSeqElem<CvPoint>(ptseq, i).Value;
                    Cv.Circle(img, pt, 2, new CvColor(255, 0, 0), -1);
                }
                */
    
                //임의의 점 그린 사진 보여주기
                p1.ImageIpl = img;
    
                _dst = img.Clone();
    
                // Hull 찾기
                CvPoint[] hull;
                Cv.ConvexHull2(ptseq, out hull, ConvexHullOrientation.Clockwise);
    
                //Hull 그리기
                CvPoint pt0 = hull[hull.Length - 1];
                foreach (CvPoint pt in hull)
                {
                    Cv.Line(_dst, pt0, pt, CvColor.Green, 3, LineType.AntiAlias);
                    pt0 = pt;
                }
    
                /*
                for (int i = 0; i < hull.Total; i++)
                {
                    CvPoint pt = Cv.GetSeqElem<Pointer<CvPoint>>(hull, i).Value.Entity;             // CvPoint pt = **CV_GET_SEQ_ELEM( CvPoint*, hull, i );
                    Cv.Line(img, pt0, pt, new CvColor(0, 255, 0));
                    pt0 = pt;
                }
                */
    
                p2.ImageIpl = _dst;
                wind.Image = _dst;
                img.Dispose();
            }
        }
    }
    

\- 필드 후 실행한 결과 화면 입니다

![](/assets/images/c_opencvsharp_이미지_컨벡스헐_그리기/img_3.jpg)

![](/assets/images/c_opencvsharp_이미지_컨벡스헐_그리기/img_4.jpg)

  

#c# #opencv #Hull #opencvsharp #컨벡스헐 #점선그리기 #ConvexHull2 #점선연결하기 #외곽선그리기

