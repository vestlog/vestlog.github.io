---
categories:
  - 'Blog'
tags:
  - 'c#'
  - 'C#'
  - 'C#'
  - '픽쳐박스'
  - '투명팝업'
last_modified_at: '2025-05-30T16:04:02+09:00'
title: '[2025-08-13] - Post'
excerpt: ''
layout: 'post'
lang: 'ko'
permalink: '/posts/2020-04-22-c_투명_팝업창을_이용한_progressbar_만들기/'
alt_en: '/en/posts/2020-04-22-c_투명_팝업창을_이용한_progressbar_만들기/'
---

## [C#] 투명 팝업창을 이용한 ProgressBar 만들기

코딩정보/C#

2020-04-22 13:16:22

* * *

안녕하세요

코딩연습생입니다

이번 포스팅 주제는 투명 팝업창을 이용한 ProgressBar 만들기 입니다

프로그래스바란?

.NET에서 진행율을 표기하기 위한 그래픽 컨트롤 입니다

비쥬얼스튜디오의 도구 모음에 기본 도구로 있는데요

![](/assets/images/c_투명_팝업창을_이용한_progressbar_만들기/img.png)
![](/assets/images/c_투명_팝업창을_이용한_progressbar_만들기/img_1.png)

대충 이렇게 생긴 모습입니다

흔히 프로그램을 사용하다보면 업데이트나 데이터 처리를 할때 사용자에게 얼마큼 진행되었는지를 알려주기위해

사용합니다

이런 컨트롤을 팝업창을 통해 메인 Form위에 투명으로 띄워 진행 여부를 표시해주는 팝업을 생성해볼려고 합니다

일단 팝어창을 만들기 위해 From을 하나 생성합니다

그리고 생성된 폼 속정에서 TransparencyKey를 배경색과 동일하게 설정 합니다

![](/assets/images/c_투명_팝업창을_이용한_progressbar_만들기/img_2.png)

이렇게 설정하시면 해당 폼이 팝업으로 띄워졌을때 주변 배경이 투명으로 처리되어 보여지게 됩니다

그리고 무언가 처리중인걸 표시하기 위해 픽쳐박스 컨트롤에 GIF 파일을 넣어 줄겁니다

PictureBox 컨트롤을 팝업 폼에 생성하고 그림박스의 배경 이미지를 GIF 파일로 넣어줍니다

![](/assets/images/c_투명_팝업창을_이용한_progressbar_만들기/img.jpg)

참고로 진행 상태 GIF는 아래 링크 페이지를 활용하시면 됩니다

<https://www.sitepoint.com/demos/loading-images/>

[ AJAX Loading Images Collections | SitePoint www.sitepoint.com ](https://www.sitepoint.com/demos/loading-images/)

여기까지 설정을 하셨다면 아래와 같은 화면이 구성 될겁니다

![](/assets/images/c_투명_팝업창을_이용한_progressbar_만들기/img_3.png)

그럼 cs코드 안으로 들어가서 아래와 같이 Using을 선언 합니다

    
    
    using System.Threading;
    using System.Runtime.InteropServices;
    using System.Resources;

쓰레드는 GIF를 움직이기 위해 필요하고

인터럽트서비스는 팝업창을 핸들링하기 위해 필요합니다

그리고 마지막 리소스는 GIF를 등록하게 되면 이미지가 리소스로 들어가기 때문에 선언 햇습니다

    
    
    public partial class SplashWnd : Form
        {
            Bitmap bit;
    
            #region Static Function
            /// 
            /// 스플래쉬 닫을 때 true로 세팅하는 값
            /// 
            private static bool isCloseCall = false;
    
            /// 
            /// 스플래쉬 띄우기
            /// 
            public static void SplashShow()
            {
                System.Diagnostics.Process process = System.Diagnostics.Process.GetCurrentProcess();
                Control mainWindow = Control.FromHandle(process.MainWindowHandle);
    
                isCloseCall = false;
                Thread thread = new Thread(new ParameterizedThreadStart(ThreadShowWait));
                thread.Start(new object[] { mainWindow });
            }
    
            /// 
            /// 스플래쉬 닫기
            /// 
            /// 스플래쉬를 닫은 후 맨 앞으로 가져올 폼
            public static void SplashClose(Form formFront)
            {
                //Thread의 loop 를 멈춘다.
                isCloseCall = true;
    
                //주어진 폼을 맨 앞으로
                SetForegroundWindow(formFront.Handle);
                formFront.BringToFront();
            }
    
            /// 
    
            /// 윈도우를 맨 앞으로 가져오기 위한 Win32 API 메서드
            /// 
            /// 윈도우 핸들
            /// 
            [DllImport("user32.dll")]
            private static extern bool SetForegroundWindow(IntPtr hWnd);
    
            /// 
    
            /// 스플래쉬를 띄우기 위한 Parameterized Thread Method
            /// 
            /// 메인 윈도(위치를 잡기 위해)
            private static void ThreadShowWait(object obj)
            {
                object[] objParam = obj as object[];
                SplashWnd splashWnd = new SplashWnd();
                Control mainWindow = objParam[0] as Control;
    
                if (mainWindow != null)
                {
                    //메인 윈도를 알 때에는 메인 윈도의 중앙
                    splashWnd.StartPosition = FormStartPosition.Manual;
                    splashWnd.Location = new Point(
                        mainWindow.Location.X + (mainWindow.Width - splashWnd.Width) / 2,
                        mainWindow.Location.Y + (mainWindow.Height - splashWnd.Height) / 2);
                }
                else
                {
                    //메인 윈도를 모를 땐 스크린 중앙
                    splashWnd.StartPosition = FormStartPosition.CenterScreen;
                }
    
                splashWnd.Show();
                splashWnd.BringToFront();
    
                //닫기 명령이 올 때 가지 0.01 초 단위로 루프
                while (!isCloseCall)
                {
                    Application.DoEvents();
                    Thread.Sleep(10);
                }
    
                //닫는다.
                if (splashWnd != null)
                {
                    splashWnd.CloseForce();
                    splashWnd = null;
                }
            }
    
            #endregion Static Function
    
    
            #region SplashWnd Member, Function, Event
    
            /// 
    
            /// 값이 true 이면 창이 닫히지 않음.
            /// 
            private bool cannotClose = true;
    
            /// 
    
            /// 생성자
            /// 
            public SplashWnd()
            {
                InitializeComponent();
    
                //투명도는 줘도 되고 안 줘도 되고
                this.Opacity = 0.7f;
    
            }
    
            /// 
    
            /// 사용자가 ALT+F4 등의 키로 닫는 걸 방지
            /// 
            /// 
            protected override void OnClosing(CancelEventArgs e)
            {
                if (cannotClose)
                {
                    e.Cancel = true;
                    return;
                }
    
                base.OnClosing(e);
            }
    
            /// 
    
            /// 이 메서드를 호출해야만 창이 닫힌다.
            /// 
            public void CloseForce()
            {
                //OnClose 에서 닫힐 수 있도록 세팅
                cannotClose = false;
                this.Close();
            }
            #endregion SplashWnd Member, Function, Event
    
            protected override void OnLoad(EventArgs e)
            {
                ResourceManager rm = Properties.Resources.ResourceManager;
                Bitmap normal = (Bitmap)rm.GetObject("loading14");
                bit = new Bitmap(normal);
                ImageAnimator.Animate(bit, new EventHandler(this.OnFrameChanged));
                base.OnLoad(e);
    
            }
    
            protected override void OnPaint(PaintEventArgs e)
            {
                ImageAnimator.UpdateFrames();
                Graphics g = pictureBox1.CreateGraphics();
                g.DrawImage(this.bit, new Point(0, 0));
                base.OnPaint(e);
            }
    
            private void OnFrameChanged(object sender, EventArgs e)
            {
                this.Invalidate();
            }
        }

그 다음 ProgressBar를 사용하시고자 하는 위치에서

    
    
    SplashWnd.SplashShow();

구분을 사용해서 팝업을 생성해주고

진행이 끝난뒤 아래 구분을 통해 팝업창을 해제 합니다

    
    
    SplashWnd.SplashClose(this);

사용자가 내가 만든 프로그램 안에서 어떤 행위가 진행 될때 알려주기 위한 표시기 역할로 만들것이기 때문에

프로그램에서 행위가 일어나기전과 끝난뒤에 위의 구문을 넣어주면 무언가 진행되어지는것을 알려줄수 있습니다

  

#c# #C# 프로그래바 #C# GIF 움직이기 #픽쳐박스 GIF #투명팝업

