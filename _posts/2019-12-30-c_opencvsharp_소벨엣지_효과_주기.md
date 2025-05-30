---
title:  "[2019-12-30] - [C#] OpenCvSharp 소벨엣지 효과 주기"
categories:
  - Blog
tags:
  - "c#"
  - "opencv"
  - "이미지효과"
  - "이미지필터"
  - "opencvsharp"
  - "소벨엣지효과"
  - "소벨엣지"
last_modified_at: 2025-05-30T16:03:57+09:00
---

## [C#] OpenCvSharp 소벨엣지 효과 주기

코딩정보/OpenCv

2019-12-30 10:25:32

* * *

안녕하세요

저번 시간에 캐니엣지 효과 주기를 포스팅 했었는데요

이어서 이번에는 이미지에 소벨엣지 효과 주기를 포스팅 해보도록 하겠습니다

저번 포스팅과 연결되어 진행 되오니 아래 링크를 확인해서 저번 포스팅을 확인해 보세요

<https://codingman.tistory.com/53>

[ [C#] OpenCvSharp 캐니엣지 효과 주기 안녕하세요 저번 시간에 이미지 이진화 효과 주기를 포스팅 했었는데요 이어서 이번에는
이미지에 캐니엣지 효과 주기를 포스팅 해보도록 하겠습니다 저번 포스팅과 연결되어 진행 되오니 아래 링크를 확인해서 저..
codingman.tistory.com ](https://codingman.tistory.com/53)

[디자인]

\- Menu에 다음과 같이 필터 -> 소벨엣지 메뉴를 등록해 줍니다

![](/assets/images/c_opencvsharp_소벨엣지_효과_주기/img.jpg)

[Source Code]

\- 소벨엣지 메뉴에 클릭이벤트 생성

![](/assets/images/c_opencvsharp_소벨엣지_효과_주기/img_1.jpg)

\- 이벤트 위치에 다음과 같이 코딩해 줍니다

    
    
            private void 소벨엣지ToolStripMenuItem_Click(object sender, EventArgs e)
            {
                using (gray gg = new gray())
                using (IplImage temp = gg.BuildSobel(src))
                {
                    result = temp.Clone();
    
                }
                pictureBoxIpl2.ImageIpl = result;
            }

\- 그레이효과 적용시에 등록한 gray.cs 클래스 파일을 이용합니다

<https://codingman.tistory.com/51>

[ [C#] OpenCvSharp 그레이 효과 주기 안녕하세요 요즘 C#으로 연습중인 OpenCv에서 불러온 이미지에 전체 그레이 효과를
주는 이벤트를 제작해 보겠습니다 C#을 통해 OpenCv 라이브러리 등록방법은 아래 링크를 확인해주세요
https://codingman.tistor.. codingman.tistory.com
](https://codingman.tistory.com/51)

[결과창]

![](/assets/images/c_opencvsharp_소벨엣지_효과_주기/img_2.jpg)

  

#c# #opencv #이미지효과 #이미지필터 #opencvsharp #소벨엣지효과 #소벨엣지

