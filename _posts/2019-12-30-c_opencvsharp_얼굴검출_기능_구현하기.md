---
categories:
  - 'Blog'
tags:
  - '얼굴인식'
  - 'c#'
  - 'opencv'
  - '이미지효과'
  - '이미지필터'
  - '이미지인식'
  - 'opencvsharp'
  - '얼굴검출'
last_modified_at: '2025-05-30T16:03:57+09:00'
title: '[2025-08-13] - Post'
excerpt: ''
layout: 'post'
lang: 'ko'
permalink: '/posts/2019-12-30-c_opencvsharp_얼굴검출_기능_구현하기/'
alt_en: '/en/posts/2019-12-30-c_opencvsharp_얼굴검출_기능_구현하기/'
---

<div class="lang-panel lang-ko" lang="ko">
## [C#] OpenCvSharp 얼굴검출 기능 구현하기

코딩정보/OpenCv

2019-12-30 13:20:36

* * *

안녕하세요

이번 포스팅은 OpenCvSharp을 이용한 이미지 얼굴 검출 기능 입니다

포스팅에 앞서 준비물이 필요합니다

1\. haarcascade_frontalface_alt.xml 파일을 다운로드 받아 해당 Degub 폴더에 삽입해주세요.

[ haarcascade_frontalface_alt.zip 0.10MB
](./file/haarcascade_frontalface_alt.zip)

자 이렇게 준비물이 준비가 완료가 되셨다면 아래 단계를 따라해 주세요

[디자인]

\- 메뉴에 얼굴검출 메뉴를 등록해 주세요

![](/assets/images/c_opencvsharp_얼굴검출_기능_구현하기/img.jpg)

[Source Code]

\- 해당 메뉴에 클릭이벤트를 기능을 만들어 주세요

![](/assets/images/c_opencvsharp_얼굴검출_기능_구현하기/img_1.jpg)

    
    
            private void haar얼굴검출ToolStripMenuItem_Click(object sender, EventArgs e)
            {
                using (Face FA = new Face())
                using (IplImage temp = FA.FaceDetect(src))
                {
                    result = temp.Clone();
    
                }
                pictureBoxIpl2.ImageIpl = result;
    
            }

그리고 클래스를 생성해 줍니다

[Source Code]

\- 저는 클래스명을 Face로 생성하였습니다

    
    
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    using System.Windows.Forms;
    using OpenCvSharp;
    
    namespace OpenCV_V1
    {
        class Face : IDisposable
        {
            IplImage FindFace;
    
            public IplImage FaceDetect(IplImage src)
            {
                // CvHaarClassifierCascade, cvHaarDetectObjects
                // 얼굴을 검출하기 위해서 Haar 분류기의 캐스케이드를 이용한다
    
                CvColor[] colors = new CvColor[]{
                    new CvColor(0,0,255),
                    new CvColor(0,128,255),
                    new CvColor(0,255,255),
                    new CvColor(0,255,0),
                    new CvColor(255,128,0),
                    new CvColor(255,255,0),
                    new CvColor(255,0,0),
                    new CvColor(255,0,255),
                };
    
                const double scale = 1.04;
                const double scaleFactor = 1.139;
                const int minNeighbors = 2;
    
                using (IplImage img = src.Clone())
                using (IplImage smallImg = new IplImage(new CvSize(Cv.Round(img.Width / scale), Cv.Round(img.Height / scale)), BitDepth.U8, 1))
                {
                    // 얼굴 검출용의 화상의 생성
                    using (IplImage gray = new IplImage(img.Size, BitDepth.U8, 1))
                    {
                        Cv.CvtColor(img, gray, ColorConversion.BgrToGray);
                        Cv.Resize(gray, smallImg, Interpolation.Linear);
                        Cv.EqualizeHist(smallImg, smallImg);
                    }
    
                    using (CvHaarClassifierCascade cascade = CvHaarClassifierCascade.FromFile(Application.StartupPath + "\\" + "haarcascade_frontalface_alt.xml"))
                    using (CvMemStorage storage = new CvMemStorage())
                    {
                        storage.Clear();
    
                        // 얼굴의 검출
    
                        CvSeq<CvAvgComp> faces = Cv.HaarDetectObjects(smallImg, cascade, storage, scaleFactor, minNeighbors, 0, new CvSize(30, 30), new CvSize(0, 0));
    
                        // 검출한 얼굴에 원을 그린다
                        for (int i = 0; i < faces.Total; i++)
                        {
                            CvRect r = faces[i].Value.Rect;
                            CvPoint center = new CvPoint
                            {
                                X = Cv.Round((r.X + r.Width * 0.5) * scale),
                                Y = Cv.Round((r.Y + r.Height * 0.5) * scale)
                            };
                            int radius = Cv.Round((r.Width + r.Height) * 0.25 * scale);
                            img.Circle(center, radius, colors[i % 8], 3, LineType.AntiAlias, 0);
                        }
                    }
                    FindFace = img.Clone();
                    return FindFace;
                }
            }
    
            public void Dispose()
            {
                if (FindFace != null) FindFace.Dispose();
            }
        }
    }
    

[결과 창]

\- 실행하게 되면 다음과 같은 결과가 나오게 됩니다

얼굴 인식율이 100%로는 아니지만 90%로 이상 검출이 가능한거 같네요

![](/assets/images/c_opencvsharp_얼굴검출_기능_구현하기/img_2.jpg)

  

#얼굴인식 #c# #opencv #이미지효과 #이미지필터 #이미지인식 #opencvsharp #얼굴검출


</div>
<div class="lang-panel lang-en" lang="en">
(*No embedded English lines found. Add translations later.*)

</div>
