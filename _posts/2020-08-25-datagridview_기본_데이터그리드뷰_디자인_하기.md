---
categories:
  - 'Blog'
tags:
  - 'c#'
  - 'DataGridView'
  - '커스텀디자인'
  - '데이터그리드뷰'
  - '그리드뷰'
  - '그리드뷰'
  - '그리드뷰'
last_modified_at: '2025-05-30T16:04:03+09:00'
title: '[2025-08-13] - Post'
excerpt: ''
layout: 'post'
lang: 'ko'
permalink: '/posts/2020-08-25-datagridview_기본_데이터그리드뷰_디자인_하기/'
alt_en: '/en/posts/2020-08-25-datagridview_기본_데이터그리드뷰_디자인_하기/'
---

<div class="lang-panel lang-ko" lang="ko">
## [DataGridView] 기본 데이터그리드뷰 디자인 하기!!

코딩정보/C#

2020-08-25 10:31:26

* * *

안녕하세요

코딩연습생입니다~

아직 끝나지 않은 코로나로 인해 여간 힘든게 아니네요~

여러분들도 모두 코로나 감염으로 부터 조심하시길 바랍니다

![](/assets/images/datagridview_기본_데이터그리드뷰_디자인_하기/img.png)

이번 포스팅은 비쥬얼스튜디오(Microsoft Visual Studio)에서 기본으로 제공되고 있는 데이터그리드뷰(DataGridView)를

사용할때 기본 디자인이 너무 구리죠?ㅎㅎ

![](/assets/images/datagridview_기본_데이터그리드뷰_디자인_하기/img_1.png)

갠취이긴 하지만 저는 너무 구리게 느껴집니다 그래서 약간의 설정으로 그래도 조금 있어보이는(?) 그런 그리드뷰로

변경할 수 있는 설정법을 알려드릴려고 합니다

비쥬얼스튜디오(Microsoft Visual Studio)를 많이 사용하신분들이면 누구나 알고 계시겠지만 저는 어디까지나

초보(?) 아니면 연습생(?) 이런 분들을 위한 포스팅이니 이미 알고 계신분들이라면 뒤로가기를 누루시기 바랍니다ㅎㅎ

간혹 이런거 포스팅 하지 말아라 라고 말씀하시는 분들고 계셔서 맘이 아플때가 있어서..ㅠ

![](/assets/images/datagridview_기본_데이터그리드뷰_디자인_하기/img_2.png)

[디자인]

1\. C#의 Form에 비쥬얼스튜디오(Microsoft Visual Studio)에서 기본적으로 제공하는
데이터그리드뷰(DataGridView)를 삽입합니다

\- 삽입하는 방법은 좌측 도구상자탭에서 모든 Windows Forms 항목 중에 DataGridView 컨트롤을 마우스로 드래그앤드롭하여
사입합니다

![](/assets/images/datagridview_기본_데이터그리드뷰_디자인_하기/img_3.png)

2\. 삽입된 데이터그리드뷰(DataGridView)를 마우스로 클릭하여 속성창에서 아래와 같이 수정합니다

\- AllowUserToAddRows의 속성을 False로 변경

\- AllowUserToAddRows는 기본상태에서 Rows 한줄을 보여줄것인지 하는것 입니다

\- SelectionMode를 FullRowSelect로 변경

\- 데이터그리드뷰(DataGrideView)의 내용을 선택했을때 선택 방법을 설정합니다

(사용 용도에 따라 사용하셔도 됩니다)

![](/assets/images/datagridview_기본_데이터그리드뷰_디자인_하기/img.jpg)

\- 다음 모양 속성 변경입니다 위에서 아래로 상세 설정 화면입니다

![](/assets/images/datagridview_기본_데이터그리드뷰_디자인_하기/img_1.jpg)

\- AlternatingRowsDefaultCell 속성

\- 데이터그리드뷰(DataGrideView)의 내용 부분을 별도 설정없이 Row의 구분 색상을 표현 해줍니다

(말로 이해가 안되시는분은 제일 마지막 완성 이미지를 보시면 이해 하실겁니다)

![](/assets/images/datagridview_기본_데이터그리드뷰_디자인_하기/img_2.jpg)

\- ColumnHeadersDefaultCell 기본 헤더 디자인 변경

\- 헤더의 기본 색생, 정렬, 크기등을 설정합니다

![](/assets/images/datagridview_기본_데이터그리드뷰_디자인_하기/img_3.jpg)

\- ★ EnableHeadersVisualStyles 값을 False로 변경

(해당 옵션을 변경하지 않으면 디자인을 변경하셔도 화면에 표시되지 않습니다)

이렇게 기본 데이터그리드뷰(DataGridView) 속성을 몇개를 바꾸고 적용하면 아래와 같이

멋있는(?) 그리드뷰로 변경됩니다~

![](/assets/images/datagridview_기본_데이터그리드뷰_디자인_하기/img_4.png)

![](/assets/images/datagridview_기본_데이터그리드뷰_디자인_하기/img_4.jpg)

앞서 말씀드렸듯이 어디까지나 갠취입니다;;ㅎㅎ 욕하지 마세요~

  

#c# #DataGridView #커스텀디자인 #데이터그리드뷰 디자인 #그리드뷰 속성 #그리드뷰 디자인 변경 #그리드뷰 커스텀


</div>
<div class="lang-panel lang-en" lang="en">
(*No embedded English lines found. Add translations later.*)

</div>
