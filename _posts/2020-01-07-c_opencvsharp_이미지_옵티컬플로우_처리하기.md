---
categories:
  - 'Blog'
tags:
  - '이미지'
  - 'c#'
  - 'opencv'
  - 'opencvsharp'
  - '옵티컬플로우'
  - '광학처리'
  - '이미지'
  - '이미지'
  - '광류'
  - '이미지'
last_modified_at: '2025-05-30T16:03:58+09:00'
title: '[2025-08-13] - Post'
excerpt: ''
layout: 'post'
lang: 'ko'
permalink: '/posts/2020-01-07-c_opencvsharp_이미지_옵티컬플로우_처리하기/'
alt_en: '/en/posts/2020-01-07-c_opencvsharp_이미지_옵티컬플로우_처리하기/'
---

<div class="lang-panel lang-ko" lang="ko">
## [C#] OpenCvSharp 이미지 옵티컬플로우 처리하기

코딩정보/OpenCv

2020-01-07 12:51:20

* * *

안녕하세요

이번 포스팅은 OpenCvSharp로 이미지 옵티컬플로우 처리를 해보도록 하겠습니다

일단 옵티컬플로우가 무엇인지 알아야 이해가 빠를거 같은데요

저도 배우고 있는 단계라 정확한 정의는 못 내리겠습니다ㅠ

다만 제가 공부한걸로는 옵티컬플로우는 광류 또는 광학 흐름 뭐 이렇게 표현을 하더라구요

제가 이해한것을 쉽게 풀어서 설명을 하자면 영상이나 이미지의 역학적인 흐름을 표시하는겁니다

현재 프레임과 다음 프레임간의 매칭을 통해 어떠한 변화를 캣치해서 그걸 선이나 원으로 흐름을 표시하는것이죠

검색을 해보니 보통 이미지 보다는 영상쪽에서 많이 사용하는 기능같습니다

예를들면 현재 모습과 다음 모습을 비교했을때 이것이 동일한 위치에서 찍힌 이미지인지 판단을 하고 싶다고 했을때

옵티컬플로우로 이미지를 처리하게 되면 어떠한 조건에 의해 이미지속의 물체들이 광학 흐름을 했는지 표기를 한다는것

입니다

신기할 따름이죠ㅎ

저도 사진이나 영상편집의 전공자가 아니여서 좀 더 심도 있는 지식을 설명드리지 못해서 죄송합니다

하지만 분명한건 OpenCv를 공부하면 반드시 나오는 기능중에 하나라는게 핵심인거죠

그만큼 사용도가 많다는 얘기일거 같은데요

C#으로 옵티컬플로우를 구현해서 좀 더 분석 해보도록 하곘습니다

OpenCvSharp에서 옵티컬플로우를 사용하기 위한 주요 함수에 대한 설명 부터 할께요

바로 이 함수 CalcOpticalFlowBM() 입니다

C#에서 어떻게 사용되는지 설명해 드릴께요

    
    
    Cv.CalcOpticalFlowBM(srcImg1, srcImg2, block, shift, maxRange, false, velx, vely);

  * srcImg1 - 이전 프레임
  * srcImg2 - 현재 프레임
  * block - 검출에 사용할 블록의 크기
  * shift - 블록의 이격 거리를 의미(값이 낮을 수록 검출 간격이 촘촘해 집니다)
  * maxRange - 블록 주변의 인접한 블록 크기

이제 디자인을 만들어 보겟습니다

OpenCvSharp에 대한 연제 포스팅을 하다 보니 이미 만들어진 디자인에 살을 계속 붙여 나가는 식으로

개발을 진행하여 초기 디자인 생성에 대한 포스팅은 아래 링크를 확인해 주시기 바랍니다

<https://codingman.tistory.com/49>

[ [C#]OpenCvSharp 라이브러리 사용하기 #1 안녕하세요 저번 포스팅에 C#으로 OpenCvSharp 라이브러리를 등록하여
구현하는 포스팅을 준비하던중에 OpenCv 3,4 버전에서 오류가 발생하는 문제가 있다는 얘길 듣고 부랴부랴 포스팅 내용을 검토해봤는데
역시.. codingman.tistory.com ](https://codingman.tistory.com/49)

[디자인]

\- Menu에 비교 대상 이미지를 불러오기 위한 메뉴를 생성합니다

(저는 그림읽기, 그림읽기2로 만들었는데요)

(그림읽기 버튼은 pictureBoxIpl1(좌측)에 이미지 넣기 용도)

(그림읽기2 버튼은 pictureBoxIpl2(우측)에 이미지 넣기 용도)

![](/assets/images/c_opencvsharp_이미지_옵티컬플로우_처리하기/img.jpg)

\- 두번재로 옵티컬플로우 처리를 위한 메뉴도 생성해 줍니다

![](/assets/images/c_opencvsharp_이미지_옵티컬플로우_처리하기/img_1.jpg)

\- 그다음 그림읽기, 그림읽기2, 옵티컬플로우 순서로 클릭 이벤트를 생성 합니다

(순서는 상관 없습니다)

![](/assets/images/c_opencvsharp_이미지_옵티컬플로우_처리하기/img_2.jpg)

[Source Code]

    
    
            private void 옵티컬플로우ToolStripMenuItem_Click(object sender, EventArgs e)
            {
                src = Cv.LoadImage(openFileDialog1.FileName, LoadMode.Color);
                result = Cv.LoadImage(openFileDialog2.FileName, LoadMode.Color);
    
                pictureBoxIpl1.ImageIpl = src;
                pictureBoxIpl2.ImageIpl = result;
    
                using (optical Op = new optical())
                {
                    Op.OpticalFlowBM(openFileDialog1.FileName, openFileDialog2.FileName);
                }
            }

![](/assets/images/c_opencvsharp_이미지_옵티컬플로우_처리하기/img_3.jpg)

[Source Code]

    
    
            private void 그림읽기ToolStripMenuItem_Click(object sender, EventArgs e)
            {
                if (openFileDialog1.ShowDialog() == DialogResult.OK)  //파일 읽어 오기 추가
                {
                    loadImage(openFileDialog1.FileName);
                }
                else
                {
                    return;
                }
    
            }
            
            private void loadImage(String filename)
            {
                src = new IplImage(filename, LoadMode.AnyColor); //Opencv형태로 그림 파일을 읽어다 src에 저장
                pictureBoxIpl1.ImageIpl = src;
            
            }

![](/assets/images/c_opencvsharp_이미지_옵티컬플로우_처리하기/img_4.jpg)

[Source Code]

    
    
            private void 그림읽기2ToolStripMenuItem_Click(object sender, EventArgs e)
            {
                if (openFileDialog2.ShowDialog() == DialogResult.OK)  //파일 읽어 오기 추가
                {
                    loadImage2(openFileDialog2.FileName);
                }
                else
                {
                    return;
                }
            }
            
            private void loadImage2(String filename)
            {
                src2 = new IplImage(filename, LoadMode.AnyColor); //Opencv형태로 그림 파일을 읽어다 src에 저장
                pictureBoxIpl2.ImageIpl = src2;
    
            }

\- 옵티컬플로우 처리를 위한 클래스 생성

![](/assets/images/c_opencvsharp_이미지_옵티컬플로우_처리하기/img_5.jpg)

[Source Code]

    
    
    using System;
    using System.Collections.Generic;
    using System.Text;
    using OpenCvSharp;
    
    namespace OpenCV_V1
    {
        class optical : IDisposable
        {
            public void OpticalFlowBM(String file1, String file2)
            {
                // cvCalcOpticalFlowBM
                // 블록 매칭에 의한 옵티컬 플로우의 계산
    
                const int blockSize = 10;
                const int shiftSize = 1;
    
                CvSize block = new CvSize(blockSize, blockSize);
                CvSize shift = new CvSize(shiftSize, shiftSize);
                CvSize maxRange = new CvSize(50, 50);
    
                using (IplImage srcImg1 = Cv.LoadImage(file1, LoadMode.GrayScale))
                using (IplImage srcImg2 = Cv.LoadImage(file2, LoadMode.GrayScale))
                using (IplImage dstImg = Cv.LoadImage(file2, LoadMode.Color))
                {
                    CvSize VelSize = new CvSize
                    {
                        Width = (dstImg.Width - block.Width + shift.Width) / shift.Width,
                        Height = (dstImg.Height - block.Height + shift.Height) / shift.Height
                    };
    
                    using (CvMat velx = Cv.CreateMat(VelSize.Height, VelSize.Width, MatrixType.F32C1))
                    using (CvMat vely = Cv.CreateMat(VelSize.Height, VelSize.Width, MatrixType.F32C1))
                    {
                        Cv.SetZero(velx);
                        Cv.SetZero(vely);
                        
                        // (2) 옵티컬 플로우의 계산 
                        Cv.CalcOpticalFlowBM(srcImg1, srcImg2, block, shift, maxRange, false, velx, vely);
                        
                        // (3) 계산된 플로우를 그리기
                        for (int i = 0; i < velx.Rows; i++)
                        {
                            for (int j = 0; j < vely.Cols; j++)
                            {
                                int dx = (int)Cv.GetReal2D(velx, i, j);
                                int dy = (int)Cv.GetReal2D(vely, i, j);
    
                                Cv.Line(dstImg,
                                    new CvPoint(j * shiftSize, i * shiftSize),
                                    new CvPoint(j * shiftSize + dx, i * shiftSize + dy),
                                    new CvColor(255, 0, 0), 1, LineType.AntiAlias, 0);
    
                            }
                        }
                    }
    
                    using (CvWindow w = new CvWindow("옵티컬플로우"))
                    {
                        w.Image = dstImg;
                        Cv.WaitKey(0);
                    }
                }
            }
            public void Dispose()
            {
            }
        }
    }
    

* 해당 CalcOpticalFlowBM 위치에서 Exception이 발생할 경우

\- dstImg의 크기가 원본 이미지 보다 클경우 발생하오니 디버깅 해보시기 바랍니다

(검색을 해보니 OpenCvSharp 버전에 따라서 발생하기도 한다고 합니다)

(참고로 저는 문제가 발생하여 VelSize를 통해 가로, 세로 길이를 구하도록 변경하엿습니다)

[결과 창]

![](/assets/images/c_opencvsharp_이미지_옵티컬플로우_처리하기/img_6.jpg)

* 예제로 사용할려는 이미지가 좌측과 우측에 사물 이동의 흔적이 있어야 처리가 되오니 

샘플용 사진을 사용할때 주의하시기 바랍니다

  

#이미지 편집 #c# #opencv #opencvsharp #옵티컬플로우 #광학처리 #이미지 광학 #이미지 처리 #광류 #이미지 광류


</div>
<div class="lang-panel lang-en" lang="en">
(*No embedded English lines found. Add translations later.*)

</div>
