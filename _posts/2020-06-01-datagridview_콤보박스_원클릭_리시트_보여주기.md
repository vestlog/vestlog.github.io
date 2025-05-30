---
title:  "[2020-06-01] - [DataGridView] 콤보박스 원클릭 리시트 보여주기"
categories:
  - Blog
tags:
  - "드롭다운"
  - "콤보박스"
  - "데이터그리드뷰"
  - "CellClick"
  - "콤보박스리스트"
last_modified_at: 2025-05-30T16:04:02+09:00
---

## [DataGridView] 콤보박스 원클릭 리시트 보여주기

코딩정보/C#

2020-06-01 09:31:10

* * *

안녕하세요

코딩연습생입니다

C# Winform에서 데이터그리드뷰를 사용해서 이런저런(?) 프로그램을 구현하실때

데이터그리드뷰에 생성한 콤보박스가 꼭 두번씩 클릭해야 리스트를 보여주는 현상을 보신적 있으실거 같은데요

저만 그런건지는 잘 모르겠지만...

제가 파악해본결과 데이터 그리드뷰의 콤보박스 Cell이 활성화 된 이후 드롭다운이 발생할때 리스트를 보여주기 때문에

활성화 1번 클릭 -> 드롭다운 1번 클릭 = 2번클릭

이렇게 되는거 같습니다 저는 한번에 클릭해서 처리하고 싶은데 말이죠

그래서 이번 포스팅에서 그걸 해결 할 수 있는 팁을 알려드릴려고 합니다

제가 할려는 방법 이외에 더 쉬운 방법이나 정보가 있으면 공유 부탁드립니다ㅎ

일단 현상 부터 한번 보시죠

1) 제가 만든 데이터 그리드뷰에 이렇게 연속적인 콤보박스가 두개 존재합니다

\- 1개는 공백이 들어가 있는 콤보박스

\- 1개는 Y/N이 표시되는 콤보박스

![](/assets/images/datagridview_콤보박스_원클릭_리시트_보여주기/img.jpg)

2) 마우스를 한번 클릭 했을때의 모습입니다

\- 클릭한 콤보박스 영역이 선택은 되었지만 리스트는 드릴다운이 되지 않았습니다

![](/assets/images/datagridview_콤보박스_원클릭_리시트_보여주기/img_1.jpg)

3) 활성화된 콤보박스를 마우스로 재 클릭 했을때 모습 입니다

\- 이제서야 드릴다운이 되면서 리스트가 보입니다

![](/assets/images/datagridview_콤보박스_원클릭_리시트_보여주기/img_2.jpg)

자 이제 해결하기 위해서 그리드 뷰의 CellClick 이벤트를 생성하겠습니다

1) 디자인화면에서 데이터그리드 이벤트중 CellClick 이벤트를 다음과 같이 생성합니다

![](/assets/images/datagridview_콤보박스_원클릭_리시트_보여주기/img.png)

2) 소스코드를 작성합니다

    
    
            private void dataGridView1_CellClick(object sender, DataGridViewCellEventArgs e)
            {
                var datagridview = sender as DataGridView;
    
                if (e.ColumnIndex == 11 || e.ColumnIndex == 9)
                {
                    datagridview.BeginEdit(true);
                    ((ComboBox)datagridview.EditingControl).DroppedDown = true;
                }
            }

3) 디버깅 이후 실행해서 테스트 합니다

\- 활성화와 드릴다운이 동시에 진행 됩니다

![](/assets/images/datagridview_콤보박스_원클릭_리시트_보여주기/img_3.jpg)

  

#드롭다운 #콤보박스 원클릭 #데이터그리드뷰 콤보박스 클릭이벤트 #CellClick #콤보박스리스트

