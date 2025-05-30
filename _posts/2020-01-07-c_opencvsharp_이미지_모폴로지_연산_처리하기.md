---
title:  "[2020-01-07] - [C#] OpenCvSharp 이미지 모폴로지 연산 처리하기"
categories:
  - Blog
tags:
  - "c#"
  - "opencv"
  - "팽창"
  - "침식"
  - "모폴로지"
  - "opencvsharp"
  - "이미지처리"
  - "이미지작업"
  - "모폴로지연산"
  - "형태학적"
last_modified_at: 2025-05-30T16:03:58+09:00
---

## [C#] OpenCvSharp 이미지 모폴로지 연산 처리하기

코딩정보/OpenCv

2020-01-07 15:03:46

* * *

안녕하세요

이번 OpenCvSharp를 이용한 포스팅에서 다룰 연산은 모폴로지 연산 입니다

모폴로지는 영상이나 이미지의 화소값을 이용하여 이미지의 형태학적 작업을 할 수 있습니다

[*모폴로지 연산의 종류와 간단한 설명]

  1. 팽장(Dilate)  
\- 255값의 화소가 부풀어서 커지는것

  2. 침식(Erode)  
\- 255값의 화소가 깎이는 것

  3. 열기연산(Opening)  
-작은 흰 점들을 없앤 뒤 큰 덩어리들은 다시 원래 크기로 키우는 연산
  4. 닫기연산(Closing)  
\- 약간 떨어진 선이나 공간을 잇거나 채우고 난 뒤 전체 크기를 원래대로 줄이는 연산

  5. 그라디언트연산(Gradient)  
\- 영역의 외곽선만 남기는 효과를 주는 연산

  6. 탑햇연산(TopHat)  
\- 열기연산(Opening)이 수행된 부분을 빼내는 연산

  7. 블랙연산(BalckHat)  
\- 원본 이미지에서 어두운 영역을 강조하는 연산

역시 영상, 이미지 분야는 어려운거 같다 모두 수학적 공식을 통해 색상을 조절하고 세밀한 조절을 통해

이미지나 영상의 효과나 처리를 주는데 비전공자로써는 도저히 이해가 되질 않는다ㅎ

나는 나의 전공으로 돌아와서 코딩을 해보겠다ㅋㅋ

이번 포스팅도 저번 포스팅에 이어 진행되므로 이전 포스팅을 읽고 진행 하는것이

이해가 빠를것이다

<https://codingman.tistory.com/62>

[ [C#] OpenCvSharp 이미지 옵티컬플로우 처리하기 안녕하세요 이번 포스팅은 OpenCvSharp로 이미지 옵티컬플로우 처리를
해보도록 하겠습니다 일단 옵티컬플로우가 무엇인지 알아야 이해가 빠를거 같은데요 저도 배우고 있는 단계라 정확한 정의는 못 내리겠습니다..
codingman.tistory.com ](https://codingman.tistory.com/62)

모폴로지 연산처리를 위해 Menu에 버튼을 생성한다

[디자인]

\- 알고리즘 항목에 모폴로지를 만들고 세부 메뉴로 아래 리스트별로 생성 시킨다

![](/assets/images/c_opencvsharp_이미지_모폴로지_연산_처리하기/img.jpg)

\- 세부 메뉴로 생성된 모폴로지 연산 처리별 클릭 이벤트 생성

![](/assets/images/c_opencvsharp_이미지_모폴로지_연산_처리하기/img_1.jpg)
![](/assets/images/c_opencvsharp_이미지_모폴로지_연산_처리하기/img_2.jpg)
![](/assets/images/c_opencvsharp_이미지_모폴로지_연산_처리하기/img_3.jpg)
![](/assets/images/c_opencvsharp_이미지_모폴로지_연산_처리하기/img_4.jpg)
![](/assets/images/c_opencvsharp_이미지_모폴로지_연산_처리하기/img_5.jpg)
![](/assets/images/c_opencvsharp_이미지_모폴로지_연산_처리하기/img_6.jpg)
![](/assets/images/c_opencvsharp_이미지_모폴로지_연산_처리하기/img_7.jpg)

[Source Code]

\- 이벤트별 클래스 호출 코딩을 작성해 준다

    
    
            private void dilateToolStripMenuItem_Click(object sender, EventArgs e)
            {
                using (Morphology Mp = new Morphology())
                using (IplImage temp = Mp.DilateMorphology(src))
                {
                    result = temp.Clone();
    
                }
                pictureBoxIpl2.ImageIpl = result;
            }
    
            private void erodeToolStripMenuItem_Click(object sender, EventArgs e)
            {
                using (Morphology Mp = new Morphology())
                using (IplImage temp = Mp.ErodeMorphology(src))
                {
                    result = temp.Clone();
    
                }
                pictureBoxIpl2.ImageIpl = result;
            }
    
            private void openingToolStripMenuItem_Click(object sender, EventArgs e)
            {
                using (Morphology Mp = new Morphology())
                using (IplImage temp = Mp.OpenMorphology(src))
                {
                    result = temp.Clone();
    
                }
                pictureBoxIpl2.ImageIpl = result;
            }
    
            private void closingToolStripMenuItem_Click(object sender, EventArgs e)
            {
                using (Morphology Mp = new Morphology())
                using (IplImage temp = Mp.CloseMorphology(src))
                {
                    result = temp.Clone();
    
                }
                pictureBoxIpl2.ImageIpl = result;
            }
    
            private void gradientToolStripMenuItem_Click(object sender, EventArgs e)
            {
                using (Morphology Mp = new Morphology())
                using (IplImage temp = Mp.GradientMorphology(src))
                {
                    result = temp.Clone();
    
                }
                pictureBoxIpl2.ImageIpl = result;
            }
    
            private void topHatToolStripMenuItem_Click(object sender, EventArgs e)
            {
                using (Morphology Mp = new Morphology())
                using (IplImage temp = Mp.TopHatMorphology(src))
                {
                    result = temp.Clone();
    
                }
                pictureBoxIpl2.ImageIpl = result;
            }
    
            private void balckHatToolStripMenuItem_Click(object sender, EventArgs e)
            {
                using (Morphology Mp = new Morphology())
                using (IplImage temp = Mp.BlackHatMorphology(src))
                {
                    result = temp.Clone();
    
                }
                pictureBoxIpl2.ImageIpl = result;
            }

\- 모폴로지 클래스 파일 생성

(클래스명칭 : Morphology.cs)

![](/assets/images/c_opencvsharp_이미지_모폴로지_연산_처리하기/img_8.jpg)

[Source Code]

\- 생성한 클래스 파일에 다음과 같으 코딩 한다

    
    
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using OpenCvSharp;
    
    namespace OpenCV_V1
    {
        class Morphology : IDisposable
        {
            IplImage morph;
    
    
            public IplImage DilateMorphology(IplImage src)
            {
                // 구조 요소를 지정하고, 확장 모폴로지 연산을 행한다
    
                //(1) 화상 읽어들여, 연산 결과 화상 영역의 확보를 행한다
                using (IplImage srcImg = src.Clone())
                using (IplImage dstImg = srcImg.Clone())
                using (IplImage tmpImg = srcImg.Clone())
                {
                    //(2) 구조 요소를 생성한다 
                    IplConvKernel element = Cv.CreateStructuringElementEx(9, 9, 4, 4, ElementShape.Rect, null);
                    //(3) 모폴로지 연산을 실행한다 
                    Cv.Dilate(srcImg, dstImg, element, 1);
                    morph = dstImg.Clone();
    
                }
                return morph;
            }
    
            public IplImage ErodeMorphology(IplImage src)
            {
    
                // 구조 요소를 지정하고, 축소 모폴로지 연산을 행한다
    
                //(1) 화상 읽어들여, 연산 결과 화상 영역의 확보를 행한다
                using (IplImage srcImg = src.Clone())
                using (IplImage dstImg = srcImg.Clone())
                using (IplImage tmpImg = srcImg.Clone())
                {
                    //(2) 구조 요소를 생성한다 
                    IplConvKernel element = Cv.CreateStructuringElementEx(9, 9, 4, 4, ElementShape.Rect, null);
                    //(3) 모폴로지 연산을 실행한다 
                    Cv.Erode(srcImg, dstImg, element, 1);
                    morph = dstImg.Clone();
                }
                return morph;
            }
    
            public IplImage OpenMorphology(IplImage src)
            {
    
                // 구조 요소를 지정하고, 오픈 모폴로지 연산을 행한다
    
                //(1) 화상 읽어들여, 연산 결과 화상 영역의 확보를 행한다
                using (IplImage srcImg = src.Clone())
                using (IplImage dstImg = srcImg.Clone())
                using (IplImage tmpImg = srcImg.Clone())
                {
                    //(2) 구조 요소를 생성한다 
                    IplConvKernel element = Cv.CreateStructuringElementEx(9, 9, 4, 4, ElementShape.Rect, null);
                    //(3) 모폴로지 연산을 실행한다 
                    Cv.MorphologyEx(srcImg, dstImg, tmpImg, element, MorphologyOperation.Open, 1);
                    morph = dstImg.Clone();
    
                }
                return morph;
            }
    
            public IplImage CloseMorphology(IplImage src)
            {
    
                // 구조 요소를 지정하고, 닫힘 모폴로지 연산을 행한다
    
                //(1) 화상 읽어들여, 연산 결과 화상 영역의 확보를 행한다
                using (IplImage srcImg = src.Clone())
                using (IplImage dstImg = srcImg.Clone())
                using (IplImage tmpImg = srcImg.Clone())
                {
                    //(2) 구조 요소를 생성한다 
                    IplConvKernel element = Cv.CreateStructuringElementEx(9, 9, 4, 4, ElementShape.Rect, null);
                    //(3) 모폴로지 연산을 실행한다 
                    Cv.MorphologyEx(srcImg, dstImg, tmpImg, element, MorphologyOperation.Close, 1);
                    morph = dstImg.Clone();
    
                }
                return morph;
            }
    
            public IplImage GradientMorphology(IplImage src)
            {
    
                // 구조 요소를 지정하고, 그라디언트 모폴로지 연산을 행한다
    
                //(1) 화상 읽어들여, 연산 결과 화상 영역의 확보를 행한다
                using (IplImage srcImg = src.Clone())
                using (IplImage dstImg = srcImg.Clone())
                using (IplImage tmpImg = srcImg.Clone())
                {
                    //(2) 구조 요소를 생성한다 
                    IplConvKernel element = Cv.CreateStructuringElementEx(9, 9, 4, 4, ElementShape.Rect, null);
                    //(3) 모폴로지 연산을 실행한다 
                    Cv.MorphologyEx(srcImg, dstImg, tmpImg, element, MorphologyOperation.Gradient, 1);
                    morph = dstImg.Clone();
                }
                return morph;
            }
    
            public IplImage TopHatMorphology(IplImage src)
            {
    
                // 구조 요소를 지정하고, 탑햇 모폴로지 연산을 행한다
    
                //(1) 화상 읽어들여, 연산 결과 화상 영역의 확보를 행한다
                using (IplImage srcImg = src.Clone())
                using (IplImage dstImg = srcImg.Clone())
                using (IplImage tmpImg = srcImg.Clone())
                {
                    //(2) 구조 요소를 생성한다 
                    IplConvKernel element = Cv.CreateStructuringElementEx(9, 9, 4, 4, ElementShape.Rect, null);
                    //(3) 모폴로지 연산을 실행한다 
                    Cv.MorphologyEx(srcImg, dstImg, tmpImg, element, MorphologyOperation.TopHat, 1);
                    morph = dstImg.Clone();
                }
                return morph;
            }
    
            public IplImage BlackHatMorphology(IplImage src)
            {
    
                // 구조 요소를 지정하고, 블랙햇 모폴로지 연산을 행한다
    
                //(1) 화상 읽어들여, 연산 결과 화상 영역의 확보를 행한다
                using (IplImage srcImg = src.Clone())
                using (IplImage dstImg = srcImg.Clone())
                using (IplImage tmpImg = srcImg.Clone())
                {
                    //(2) 구조 요소를 생성한다 
                    IplConvKernel element = Cv.CreateStructuringElementEx(9, 9, 4, 4, ElementShape.Rect, null);
                    //(3) 모폴로지 연산을 실행한다 
                    Cv.MorphologyEx(srcImg, dstImg, tmpImg, element, MorphologyOperation.BlackHat, 1);
                    morph = dstImg.Clone();
                }
                return morph;
            }
    
            public void Dispose()
            {
                if (morph != null) Cv.ReleaseImage(morph);
            }
        }
    }
    

[결과 창]

*팽창 연산 결과 화면

![](/assets/images/c_opencvsharp_이미지_모폴로지_연산_처리하기/img_9.jpg)

*침식 연산 결과 화면

![](/assets/images/c_opencvsharp_이미지_모폴로지_연산_처리하기/img_10.jpg)

* 열기 연산 결과 화면

![](/assets/images/c_opencvsharp_이미지_모폴로지_연산_처리하기/img_11.jpg)

* 닫기 연산 결과 화면

![](/assets/images/c_opencvsharp_이미지_모폴로지_연산_처리하기/img_12.jpg)

*그라디언트연산 결과 화면

![](/assets/images/c_opencvsharp_이미지_모폴로지_연산_처리하기/img_13.jpg)

*탑햇 연산 결과 화면

![](/assets/images/c_opencvsharp_이미지_모폴로지_연산_처리하기/img_14.jpg)

*블랙햇 연산 결과 화면

![](/assets/images/c_opencvsharp_이미지_모폴로지_연산_처리하기/img_15.jpg)

각 결과 화면을 보면 모폴로지 연산별 차이를 확인 할 수 있습니다

  

#c# #opencv #팽창 #침식 #모폴로지 #opencvsharp #이미지처리 #이미지작업 #모폴로지연산 #형태학적

