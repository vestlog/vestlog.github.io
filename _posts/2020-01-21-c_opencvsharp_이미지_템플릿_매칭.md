---
categories:
  - 'Blog'
tags:
  - '비교'
  - '매칭'
  - 'c#'
  - '검출'
  - 'opencv'
  - 'opencvsharp'
  - '템플릿매칭'
  - '이미지비교'
  - '찾아내기'
last_modified_at: '2025-05-30T16:03:59+09:00'
title: '[2025-08-13] - Post'
excerpt: ''
layout: 'post'
lang: 'ko'
permalink: '/posts/2020-01-21-c_opencvsharp_이미지_템플릿_매칭/'
alt_en: '/en/posts/2020-01-21-c_opencvsharp_이미지_템플릿_매칭/'
---

<div class="lang-panel lang-ko" lang="ko">
## [C#] OpenCvSharp 이미지 템플릿 매칭

코딩정보/OpenCv

2020-01-21 10:13:45

* * *

안녕하세요

이번 시간 포스팅 내용은 제목과 똑같이 원본이미지에서 찾고자 하는 부분이미지를 매칭하여

원본이미지에 해당 부분을 검출해 내는 기능입니다

이미 인터넷상에 많은 정보가 있기에 별도 설명은 생략하고 바로 기능 구현으로 넘어가겠습니다

해당 포스팅도 저번 포스팅에 이어 진행됨에 따라 내용이 중간 생략 부분이 있을 수 있으니

이해가 잘되시면 이전 포스팅을 검색해 보시기 바랍니다

<https://codingman.tistory.com/49>

[ [C#]OpenCvSharp 라이브러리 사용하기 #1 안녕하세요 저번 포스팅에 C#으로 OpenCvSharp 라이브러리를 등록하여
구현하는 포스팅을 준비하던중에 OpenCv 3,4 버전에서 오류가 발생하는 문제가 있다는 얘길 듣고 부랴부랴 포스팅 내용을 검토해봤는데
역시.. codingman.tistory.com ](https://codingman.tistory.com/49)

템플릿 매칭을 하기 위해 두개의 이미지를 불러와야 하는데요

그러기 위한 디자인 UI 부터 보여드릴께요

[디자인]

\- 메뉴에서 유틸리티 -> 템플릿매칭 버튼을 생성

![](/assets/images/c_opencvsharp_이미지_템플릿_매칭/img.jpg)

\- 해당 버튼에서 발생할 클릭 이벤트 활성화

![](/assets/images/c_opencvsharp_이미지_템플릿_매칭/img_1.jpg)

\- 이벤트 구문에 다음과 같이 소스 코딩 합니다

    
    
            private void 템플릿매칭ToolStripMenuItem_Click(object sender, EventArgs e)
            {
                if (src == null) return;
                using (Match Sq = new Match())
                using (IplImage temp = Sq.Templit(src, src2))
                {
                    result = temp.Clone();
    
                }
    
                using (CvWindow wind = new CvWindow("결과창"))
                {
                    wind.Image = result;
                    Cv.WaitKey(0);
                }
            }

\- 템플릿 매칭 기능이 동작할 클래스를 하나 생성합니다

![](/assets/images/c_opencvsharp_이미지_템플릿_매칭/img_2.jpg)

\- 생성된 클래스에 다음과 같으 코딩합니다

    
    
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    using OpenCvSharp;
    
    namespace OpenCV_V1
    {
        class Match : IDisposable
        {
            IplImage match;
    
            public IplImage Templit(IplImage src, IplImage temp)
            {
                match = src;
                IplImage templit = temp;
                IplImage tm = new IplImage(new CvSize(match.Size.Width - templit.Size.Width + 1, match.Size.Height - templit.Size.Height + 1), BitDepth.F32, 1);
    
                CvPoint minloc, maxloc;
                Double minval, maxval;
    
                Cv.MatchTemplate(match, templit, tm, MatchTemplateMethod.SqDiffNormed);
    
                Cv.MinMaxLoc(tm, out minval, out maxval, out minloc, out maxloc);
    
                Cv.DrawRect(match, new CvRect(minloc.X, minloc.Y, templit.Width, templit.Height), CvColor.Red, 3);
    
                return match;
            }
    
            public void Dispose()
            {
                if (match != null) Cv.ReleaseImage(match);
            }
        }
    }
    

\- 그림읽기를 통해 원본 이미지를 불러옵니다

\- 그림읽기2를 통해 매칭 이미지를 불러옵니다

\- 유틸리티 -> 템플릿매칭 버튼을 눌러 결과를 확인 합니다

[결과 창]

![](/assets/images/c_opencvsharp_이미지_템플릿_매칭/img_3.jpg)

\- 이렇게 매칭 이미지(쯔위)를 원본이미지에서 검출해 내는것을 확인 할 수 있습니다

\- 프로그램을 구현하신뒤 다른 이미지로 테스트 해보시기 바랍니다

  

#비교 #매칭 #c# #검출 #opencv #opencvsharp #템플릿매칭 #이미지비교 #찾아내기


</div>
<div class="lang-panel lang-en" lang="en">
(*No embedded English lines found. Add translations later.*)

</div>
