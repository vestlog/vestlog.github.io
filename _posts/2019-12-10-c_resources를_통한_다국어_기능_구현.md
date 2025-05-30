---
title:  "[2019-12-10] - [C#] Resources를 통한 다국어 기능 구현"
categories:
  - Blog
tags:
  - "중국어"
  - "개발"
  - "한국어"
  - "c#"
  - "코딩"
  - "다국어"
  - "언어변경"
  - "Resource"
  - "인도네시아어"
last_modified_at: 2025-05-30T16:03:55+09:00
---

## [C#] Resources를 통한 다국어 기능 구현

코딩정보/C#

2019-12-10 12:05:18

* * *

안녕하세요.

코딩하는남자에 코딩연습생입니다

이번에 회사에서 관리하는 MES 프로그램에 갑작스런 외국인 사용자가 추가 되어

기존 한국어/인도네시아어만 사용되고 있었는데 중국어를 추가해야 될 일이 발생했어요~

그래서 어떤식으로 다국어 기능을 구현할까 고민하다가 좋은 정보가 있어 블로그에 기재하게 되었습니다

원리는 간단합니다

기존 프로젝트에 언어별 Resource 파일을 추가해서

컨트롤별 한국어/인도네이아어/중국어 작성해 놓고 이벤트에 따라 해당 리소스 파일의 정보를 보여주는식으로

구동 되어 집니다

[구현 방법]

1\. 기존 프로젝트에 폴더를 삽입

\- 저는 Language라고 햇어요

(솔루션 탐색기에서 폴더 추가하는 방법은 따로 설명하지 않을께요)

![](/assets/images/c_resources를_통한_다국어_기능_구현/img.jpg)

2\. Language 폴더에 리소스 파일을 생성합니다

\- 리소스파일명은 개인 취향입니다 저는 Str.resx라고 했어요

(Language폴더에서 마우스 오른쪽 버튼을 누루고 추가 새 항목 선택 후 리소스파일을 선택하면 됩니다)

![](/assets/images/c_resources를_통한_다국어_기능_구현/img_1.jpg)

\- 총 3개의 리소스 파일을 추가했습니다

(Str.resx : 기본 리소스 파일, Str.ko-KR.resx : 한국어 리소스 파일, Str.zh-CN.resx : 중국어 리소스
파일)

![](/assets/images/c_resources를_통한_다국어_기능_구현/img_2.jpg)

3\. 리소스 파일의 액세스 한정자 확인

\- Str.resx 기본 리소스 파일의 액세스 한정자 타입은 Internal 입니다

![](/assets/images/c_resources를_통한_다국어_기능_구현/img_3.jpg)

\- Str.ko-KR.resx와 Str.zh-CN.resx 파일의 액세스 한정자 타입은 코드 생성 안됨으로 하시면 됩니다

(보통 생성 순서에 따르 자동 지정되니 확인만 하시면 될거 같습니다)

![](/assets/images/c_resources를_통한_다국어_기능_구현/img_4.jpg)

4\. 디자인을 통해 언어 선택을 할 콤보박스를 생성

\- 저는 콤보박스로 했는데 이것도 개인취향이니 편하신데로 해도 되요

![](/assets/images/c_resources를_통한_다국어_기능_구현/img_5.jpg)

5\. 콤보박스 이벤트 생성

\- comboBox1_SelectedIndexChanged 이벤트 생성하여 콤보박스의 Index가 변경될때 발생하도록 합니다

![](/assets/images/c_resources를_통한_다국어_기능_구현/img_6.jpg)

6\. comboBox1_SelectedIndexChanged 코드 생성

\- CultureInfo 함수를 사용하기 위해서는 _**"using System.Globalization;"**_ 선언문을 꼭 해주셔야
합니다

    
    
    private void comboBox1_SelectedIndexChanged(object sender, EventArgs e)
            {
                if (comboBox1.SelectedIndex == 0)
                {
                    Thread.CurrentThread.CurrentUICulture = CultureInfo.GetCultureInfo("ko-KR");
                    SetTextLanguage();
                }
                else if (comboBox1.SelectedIndex == 1)
                {
                    Thread.CurrentThread.CurrentUICulture = CultureInfo.GetCultureInfo("zh-CN");
                    SetTextLanguage();
                }
    
            }

\- 언어 선택에 다른 컨트롤 변경 코드 생성

    
    
    public void SetTextLanguage()
            {
                lblUSERMODE.Text = POPMachine.Language.Str.lblUSERMODE;
                label4.Text = POPMachine.Language.Str.label4;
                NAME_DATE.Text = POPMachine.Language.Str.NAME_DATE;
                button1.Text = POPMachine.Language.Str.button1;
                button3.Text = POPMachine.Language.Str.button3;
                button4.Text = POPMachine.Language.Str.button4;
                label5.Text = POPMachine.Language.Str.label5;
                label14.Text = POPMachine.Language.Str.label14;
                label2.Text = POPMachine.Language.Str.label2;
                label8.Text = POPMachine.Language.Str.label8;
                label10.Text = POPMachine.Language.Str.label10;
                label7.Text = POPMachine.Language.Str.label7;
                label9.Text = POPMachine.Language.Str.label9;
                label6.Text = POPMachine.Language.Str.label6;
                label16.Text = POPMachine.Language.Str.label16;
                label11.Text = POPMachine.Language.Str.label11;
                label13.Text = POPMachine.Language.Str.label13;
                cmdRun_WMIX_NO1.Text = POPMachine.Language.Str.cmdRun_WMIX_NO1;
                cmdRun_WMIX_NO2.Text = POPMachine.Language.Str.cmdRun_WMIX_NO2;
                cmdRun_WMIX_NO3.Text = POPMachine.Language.Str.cmdRun_WMIX_NO3;
                cmdRun_WHLOT_NO.Text = POPMachine.Language.Str.cmdRun_WHLOT_NO;
                cmdRun_WRACK_NO.Text = POPMachine.Language.Str.cmdRun_WRACK_NO;
                cmdRun_NG_SELFCHACK.Text = POPMachine.Language.Str.cmdRun_NG_SELFCHACK;
                cmdRun_WPART_CUST.Text = POPMachine.Language.Str.cmdRun_WPART_CUST;
                cmdRun_WFORM_MCPLAN.Text = POPMachine.Language.Str.cmdRun_WFORM_MCPLAN;
                cmdRun_WLOT_NO.Text = POPMachine.Language.Str.cmdRun_WLOT_NO;
                hoverGradientButton1.Text = POPMachine.Language.Str.hoverGradientButton1;
                cmdRun_WPCardScan.Text = POPMachine.Language.Str.cmdRun_WPCardScan;
                cmdRun_WStart.Text = POPMachine.Language.Str.cmdRun_WStart;
                cmdRun_WOKQty.Text = POPMachine.Language.Str.cmdRun_WOKQty;
                cmdRun_WPrint.Text = POPMachine.Language.Str.cmdRun_WPrint;
                cmdRun_WMCStopHist.Text = POPMachine.Language.Str.cmdRun_WMCStopHist;
                cmdRun_WFinish.Text = POPMachine.Language.Str.cmdRun_WFinish;
                cmdRun_WProcImage.Text = POPMachine.Language.Str.cmdRun_WProcImage;
                cmdRun_WNGQty.Text = POPMachine.Language.Str.cmdRun_WNGQty;
                cmdRun_WLPrint.Text = POPMachine.Language.Str.cmdRun_WLPrint;
                cmdRun_WWaiting.Text = POPMachine.Language.Str.cmdRun_WWaiting;
                button5.Text = POPMachine.Language.Str.button5;
                cmdRun_Workers.Text = POPMachine.Language.Str.cmdRun_Workers;
                cmdRun_WorkHist.Text = POPMachine.Language.Str.cmdRun_WorkHist;
                cmdRun_Mold.Text = POPMachine.Language.Str.cmdRun_Mold;
                cmdRun_Wheel.Text = POPMachine.Language.Str.cmdRun_Wheel;
                cmdRun_SubPartImage.Text = POPMachine.Language.Str.cmdRun_SubPartImage;
                cmdRun_PCardStatus.Text = POPMachine.Language.Str.cmdRun_PCardStatus;
                cmdRun_Video.Text = POPMachine.Language.Str.cmdRun_Video;
                cmdRun_Call.Text = POPMachine.Language.Str.cmdRun_Call;
                cmdRun_Setting.Text = POPMachine.Language.Str.cmdRun_Setting;
                cmdRun_Exit.Text = POPMachine.Language.Str.cmdRun_Exit;
    
            }

저는 해당 화면에 컨트롤이 많아 이렇게 나열했지만 좀 더 응용하면 Resource 파일을 연계하여

같은 종류의 컨트롤별 자동 지정되도록 구현하면 Source Code가 좀 더 깔끔해질거 같네요

이렇게 구현하게되면 나중에 언어가 추가 될때 당황하지 않고 Resorce파일만 추가하여 적용해주면

더 많은 언어들의 쉽게 적용할 수 있습니다

한번 도전해 보세요^^

감사합니다

  

#중국어 #개발 #한국어 #c# #코딩 #다국어 #언어변경 #Resource #인도네시아어

