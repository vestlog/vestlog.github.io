---
categories:
  - 'Blog'
tags:
  - '어플만들기'
  - '앱만들기'
  - 'cross-platform'
  - '자마린'
  - 'Xamarin'
  - 'xamarin'
  - '로그인만들기'
  - '비쥬얼스튜디오'
last_modified_at: '2025-05-30T16:04:01+09:00'
title: '[2025-08-13] - Post'
excerpt: ''
layout: 'post'
lang: 'ko'
permalink: '/posts/2020-03-16-xamarin_forms_자마린으로_간단한_로그인_앱_만들기/'
alt_en: '/en/posts/2020-03-16-xamarin_forms_자마린으로_간단한_로그인_앱_만들기/'
---

## [Xamarin Forms] 자마린으로 간단한 로그인 앱 만들기

코딩정보/Android

2020-03-16 16:31:51

* * *

안녕하세요.

코딩연습생입니다

비쥬얼스튜디오 Xamarin을 이용한 로그인 창 만들기 입니다

저도 처음 접해보는 부분이라 많이 헷갈리고 연습을 하고 있습니다~

음..일단 시작에 앞서 비쥬얼스튜디오의 Cross-Platform에 대해 알아야 하는데요

간단하게 말해서 C#코드로 짠 앱 소스코드를 다양한 플렛폼에 간단하게 적용시킬수 있는 플랫폼이다

인데요...ㅎㅎ

아래 정말 설명을 잘 해 놓은 영상이 있어서 링크 걸어드리니 한번 보시는걸 추천 드립니다

[https://www.youtube.com/watch?v=B_cjRSDve8Q&list=PLZiskT3TqIThspx9OPBNFY5xGKTKJFelG](https://www.youtube.com/watch?v=B_cjRSDve8Q&list=PLZiskT3TqIThspx9OPBNFY5xGKTKJFelG)

이번에 만들 로그인창도 Cross-Platform 환경에서 제작을 할 것입니다

다소 복작하고 어려울수 있으나 일단 한번 따라서 완성 시키시고 나면 금방 이해가 가실거라 생각합니다

1\. 프로젝트 생성

\- 비쥬얼스튜디오 2017환경에서 개발하엿습니다 참고해서 봐주세요

\- 파일 -> 새로만들기 -> 프로젝트

![](/assets/images/xamarin_forms_자마린으로_간단한_로그인_앱_만들기/img.jpg)

\- 프로젝트 형식은 Cross-Platform 형식이며, 모바일 앱(Xamarin.Forms) 형식의 폼을 구성해서 만듭니다

![](/assets/images/xamarin_forms_자마린으로_간단한_로그인_앱_만들기/img_1.jpg)

\- Cross Platform의 세부 설정입니다 빈화면에 호환되는 플랫폼의 종류 등을 설정 합니다

![](/assets/images/xamarin_forms_자마린으로_간단한_로그인_앱_만들기/img_2.jpg)

2\. 폼 구성하기

\- Cross Platform 솔루션 구성을 먼저 이해해야 합니다

\- 전체 프로젝트를 감싸는 솔루션 밑에 플랫폼을 관장해야할 C# 프로젝트가 있고

그 밑에 각 플렛폼에 따른 프로젝트가 있습니다

\- 프로젝트명.Droid : 안드로이드 플렛폼

\- 프로젝트명.IOS : 애플 플렛폼

\- 프로젝트폄.UWP : 테블릿 플렛폼

\- 저희가 수정할 부분은 C# 프로젝트 입니다

\- C#프로젝트 부분에서 App.xaml 파일을 마우스 오른쪽 버튼을 눌러 삭제 합니다

![](/assets/images/xamarin_forms_자마린으로_간단한_로그인_앱_만들기/img_3.jpg)

\- C# 프로젝트에서 마우스 오른쪽 버튼을 통해 새항목을 선택합니다

![](/assets/images/xamarin_forms_자마린으로_간단한_로그인_앱_만들기/img_4.jpg)

\- App.cs 클래스 파일을 추가합니다

![](/assets/images/xamarin_forms_자마린으로_간단한_로그인_앱_만들기/img_5.jpg)

\- App.cs 클래스 파일에 다음과 같이 코딩합니다

*App.cs
    
    
    using Xamarin.Forms;
    
    namespace LoginNavigation
    {
    	public class App : Application
    	{
    		public static bool IsUserLoggedIn { get; set; }
    
    		public App ()
    		{
    			if (!IsUserLoggedIn) {
    				MainPage = new NavigationPage (new LoginPage ());
    			} else {
    				MainPage = new NavigationPage (new LoginNavigation.MainPage ());
    			}
    		}
    
    		protected override void OnStart ()
    		{
    			// Handle when your app starts
    		}
    
    		protected override void OnSleep ()
    		{
    			// Handle when your app sleeps
    		}
    
    		protected override void OnResume ()
    		{
    			// Handle when your app resumes
    		}
    	}
    }
    
    

\- 다시 C# 프로젝트에서 마우스 오른쪽 버튼을 클릭하여 클래스 파일을 추가 합니다

![](/assets/images/xamarin_forms_자마린으로_간단한_로그인_앱_만들기/img_6.jpg)

\- 클래스 명은 Constants.cs로 만들고 추가 합니다

![](/assets/images/xamarin_forms_자마린으로_간단한_로그인_앱_만들기/img_7.jpg)

\- 새로 추가된 클래스 파일에 아래와 같이 코딩합니다

*Constants.cs
    
    
    using System;
    using System.Data;
    
    namespace LoginNavigation
    {
        public static class Constants
        {
            public static string Username = string.Empty;
            public static string Password = string.Empty;
    
    	}
    }
    

\- 다시 항목 추가를 해줍니다

![](/assets/images/xamarin_forms_자마린으로_간단한_로그인_앱_만들기/img_8.jpg)

\- 이번에는 LoginPage.xaml 이름을 가진 콘텐츠 페이지를 추가합니다

![](/assets/images/xamarin_forms_자마린으로_간단한_로그인_앱_만들기/img_9.jpg)

\- 콘텐츠 페이지는 디자인 부분과 CS 부분의 소스가 두개로 입력됩니다

\- 처음 LoginPage.xaml 디자인 부분에 아래와 같이 코딩합니다

*LoginPage.xaml
    
    
    <?xml version="1.0" encoding="UTF-8"?>
    <ContentPage xmlns="http://xamarin.com/schemas/2014/forms" xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml" x:Class="LoginNavigation.LoginPage" Title="Login">
    	<ContentPage.ToolbarItems>
    		<ToolbarItem Text="Sign Up" Clicked="OnSignUpButtonClicked" />
    	</ContentPage.ToolbarItems>
    	<ContentPage.Content>
    		<StackLayout VerticalOptions="StartAndExpand">
    			<Label Text="Username" />
    			<Entry x:Name="usernameEntry" Placeholder="username" />
    			<Label Text="Password" />
    			<Entry x:Name="passwordEntry" IsPassword="true" />
    			<Button Text="Login" Clicked="OnLoginButtonClicked" />
    			<Label x:Name="messageLabel" />
    		</StackLayout>
    	</ContentPage.Content>
    </ContentPage>

\- 다음 LoginPage.xaml.cs 부분에 아래와 같이 코딩합니다

*LoginPage.xaml.cs
    
    
    using System;
    using Xamarin.Forms;
    using System.Data;
    using System.Data.SqlClient;
    
    namespace LoginNavigation
    {
    	public partial class LoginPage : ContentPage
    	{
    		public LoginPage ()
    		{
    			InitializeComponent ();
    		}
    
    		async void OnSignUpButtonClicked (object sender, EventArgs e)
    		{
    			await Navigation.PushAsync (new SignUpPage ());
    		}
    
    		async void OnLoginButtonClicked (object sender, EventArgs e)
    		{
    			var user = new User {
    				Username = usernameEntry.Text,
    				Password = passwordEntry.Text
    			};
    
                var isValid = AreCredentialsCorrect (user);
    			if (isValid) {
    				App.IsUserLoggedIn = true;
    				Navigation.InsertPageBefore (new MainPage (), this);
    				await Navigation.PopAsync ();
    			} else {
    				messageLabel.Text = "Login failed";
    				passwordEntry.Text = string.Empty;
    			}
    		}
    
    
            bool AreCredentialsCorrect (User user)
    		{
                return user.Username == Constants.Username && user.Password == Constants.Password;
    		}
    	}
    }
    

\- 다시 C# 프로젝트에서 신규 클래스 파일을 추가합니다

![](/assets/images/xamarin_forms_자마린으로_간단한_로그인_앱_만들기/img_10.jpg)

\- 클래스 명칭은 LoginPageCs.cs파일로 합니다

![](/assets/images/xamarin_forms_자마린으로_간단한_로그인_앱_만들기/img.png)

\- 신규로 생성한 클래스 파일에 아래와 같이 코딩을 합니다

*LoginPageCS.cs
    
    
    using System;
    using Xamarin.Forms;
    using System.Data;
    using System.Data.SqlClient;
    
    namespace LoginNavigation
    {
    	public class LoginPageCS : ContentPage
    	{
    		Entry usernameEntry, passwordEntry;
    		Label messageLabel;
    
    		public LoginPageCS ()
    		{
    			var toolbarItem = new ToolbarItem {
    				Text = "Sign Up"
    			};
    			toolbarItem.Clicked += OnSignUpButtonClicked;
    			ToolbarItems.Add (toolbarItem);
    
    			messageLabel = new Label ();
    			usernameEntry = new Entry {
    				Placeholder = "username"	
    			};
    			passwordEntry = new Entry {
    				IsPassword = true
    			};
    			var loginButton = new Button {
    				Text = "Login"
    			};
    			loginButton.Clicked += OnLoginButtonClicked;
    
    			Title = "Login";
    			Content = new StackLayout { 
    				VerticalOptions = LayoutOptions.StartAndExpand,
    				Children = {
    					new Label { Text = "Username" },
    					usernameEntry,
    					new Label { Text = "Password" },
    					passwordEntry,
    					loginButton,
    					messageLabel
    				}
    			};
    		}
    
    		async void OnSignUpButtonClicked (object sender, EventArgs e)
    		{
    			await Navigation.PushAsync (new SignUpPageCS ());
    		}
    
    		async void OnLoginButtonClicked (object sender, EventArgs e)
    		{
    			var user = new User {
    				Username = usernameEntry.Text,
    				Password = passwordEntry.Text
    			};
    
                var isValid = AreCredentialsCorrect (user);
    			if (isValid) {
    				App.IsUserLoggedIn = true;
    				Navigation.InsertPageBefore (new MainPageCS (), this);
    				await Navigation.PopAsync ();
    			} else {
    				messageLabel.Text = "Login failed";
    				passwordEntry.Text = string.Empty;
    			}
    		}
    
            bool AreCredentialsCorrect (User user)
    		{
    			return user.Username == Constants.Username && user.Password == Constants.Password;
    		}
    	}
    }
    
    
    

\- 다음 MainPage.xaml 파일에 아래와 같이 코딩 해줍니다

\- 콘텐츠 페이지 이기 때문에 xaml과 cs 부분으로 나뉘어져 있으니 주의 하시기 바랍니다

\- MainPage.xaml 부분 코딩 입니다

*MainPage.xaml
    
    
    <?xml version="1.0" encoding="UTF-8"?>
    <ContentPage xmlns="http://xamarin.com/schemas/2014/forms" xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml" x:Class="LoginNavigation.MainPage" Title="Main Page">
    	<ContentPage.ToolbarItems>
    		<ToolbarItem Text="Logout" Clicked="OnLogoutButtonClicked" />
    	</ContentPage.ToolbarItems>
    	<ContentPage.Content>
    		<StackLayout>
    			<Label Text="Main app content goes here" HorizontalOptions="Center" VerticalOptions="CenterAndExpand" />
    		</StackLayout>
    	</ContentPage.Content>
    </ContentPage>

* MainPage.xaml.cs
    
    
    using System;
    using Xamarin.Forms;
    
    namespace LoginNavigation
    {
    	public partial class MainPage : ContentPage
    	{
    		public MainPage ()
    		{
    			InitializeComponent ();
    		}
    
    		async void OnLogoutButtonClicked (object sender, EventArgs e)
    		{
    			App.IsUserLoggedIn = false;
    			Navigation.InsertPageBefore (new LoginPage (), this);
    			await Navigation.PopAsync ();
    		}
    	}
    }
    

\- 다음 다시 신규 클래스 파일을 추가 합니다

![](/assets/images/xamarin_forms_자마린으로_간단한_로그인_앱_만들기/img_11.jpg)

\- 신규 클래스의 명칭은 MainPageCS.cs파일로 지정합니다

![](/assets/images/xamarin_forms_자마린으로_간단한_로그인_앱_만들기/img_12.jpg)

\- 생성된 클래스 파일에 아래와 같이 코딩 합니다

*MainPageCS.cs
    
    
    using System;
    using Xamarin.Forms;
    
    namespace LoginNavigation
    {
    	public class MainPageCS : ContentPage
    	{
    		public MainPageCS ()
    		{
    			var toolbarItem = new ToolbarItem {
    				Text = "Logout"
    			};
    			toolbarItem.Clicked += OnLogoutButtonClicked;
    			ToolbarItems.Add (toolbarItem);
    
    			Title = "Main Page";
    			Content = new StackLayout { 
    				Children = {
    					new Label {
    						Text = "Main app content goes here",
    						HorizontalOptions = LayoutOptions.Center,
    						VerticalOptions = LayoutOptions.CenterAndExpand
    					}
    				}
    			};
    		}
    
    		async void OnLogoutButtonClicked (object sender, EventArgs e)
    		{
    			App.IsUserLoggedIn = false;
    			Navigation.InsertPageBefore (new LoginPageCS (), this);
    			await Navigation.PopAsync ();
    		}
    	}
    }
    

\- 다시 컨텐츠 페이지를 하나 추가 합니다

![](/assets/images/xamarin_forms_자마린으로_간단한_로그인_앱_만들기/img_13.jpg)

\- 추가될 컨텐츠 페이지의 명칭은 signUpPage.xaml 입니다

![](/assets/images/xamarin_forms_자마린으로_간단한_로그인_앱_만들기/img_14.jpg)

\- SignUpPage.xaml과 SignUpPage.xaml.cs 파일에 아래와 같이 따로 코딩을 합니다

*SignUpPage.xaml 
    
    
    <?xml version="1.0" encoding="UTF-8"?>
    <ContentPage xmlns="http://xamarin.com/schemas/2014/forms" 
    			 xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml" 
    			 x:Class="LoginNavigation.SignUpPage"
    			 Title="Sign Up">
    	<ContentPage.Content>
    		<StackLayout VerticalOptions="StartAndExpand">
    			<Label Text="Username" />
    			<Entry x:Name="usernameEntry" Placeholder="username" />
    			<Label Text="Password" />
    			<Entry x:Name="passwordEntry" IsPassword="true" />
    			<Label Text="Email address" />
    			<Entry x:Name="emailEntry" />
    			<Button Text="Sign Up" Clicked="OnSignUpButtonClicked" />
    			<Label x:Name="messageLabel" />
    		</StackLayout>
    	</ContentPage.Content>
    </ContentPage>

*SignUpPage.xaml.cs
    
    
    using System;
    using System.Linq;
    using Xamarin.Forms;
    
    namespace LoginNavigation
    {
    	public partial class SignUpPage : ContentPage
    	{
    		public SignUpPage ()
    		{
    			InitializeComponent ();
    		}
    
    		async void OnSignUpButtonClicked (object sender, EventArgs e)
    		{
    			var user = new User () {
    				Username = usernameEntry.Text,
    				Password = passwordEntry.Text,
    				Email = emailEntry.Text
    			};
    
    			// Sign up logic goes here
    
    			var signUpSucceeded = AreDetailsValid (user);
    			if (signUpSucceeded) {
    				var rootPage = Navigation.NavigationStack.FirstOrDefault ();
    				if (rootPage != null) {
    					App.IsUserLoggedIn = true;
    					Navigation.InsertPageBefore (new MainPage (), Navigation.NavigationStack.First ());
    					await Navigation.PopToRootAsync ();
    				}
    			} else {
    				messageLabel.Text = "Sign up failed";
    			}
    		}
    
    		bool AreDetailsValid (User user)
    		{
    			return (!string.IsNullOrWhiteSpace (user.Username) && !string.IsNullOrWhiteSpace (user.Password) && !string.IsNullOrWhiteSpace (user.Email) && user.Email.Contains ("@"));
    		}
    	}
    }
    

\- 다시 클래스 파일을 추가 합니다

![](/assets/images/xamarin_forms_자마린으로_간단한_로그인_앱_만들기/img_15.jpg)

\- 추가될 클래스 파일의 명칭은 SingUppageCS.cs 입니다

![](/assets/images/xamarin_forms_자마린으로_간단한_로그인_앱_만들기/img_1.png)

\- 추가된 클래스 파일에 아래와 같이 코딩 합니다

*SignUpPage.xaml.cs
    
    
    using System;
    using System.Linq;
    using Xamarin.Forms;
    
    namespace LoginNavigation
    {
    	public class SignUpPageCS : ContentPage
    	{
    		Entry usernameEntry, passwordEntry, emailEntry;
    		Label messageLabel;
    
    		public SignUpPageCS ()
    		{
    			messageLabel = new Label ();
    			usernameEntry = new Entry {
    				Placeholder = "username"	
    			};
    			passwordEntry = new Entry {
    				IsPassword = true
    			};
    			emailEntry = new Entry ();
    			var signUpButton = new Button {
    				Text = "Sign Up"
    			};
    			signUpButton.Clicked += OnSignUpButtonClicked;
    
    			Title = "Sign Up";
    			Content = new StackLayout { 
    				VerticalOptions = LayoutOptions.StartAndExpand,
    				Children = {
    					new Label { Text = "Username" },
    					usernameEntry,
    					new Label { Text = "Password" },
    					passwordEntry,
    					new Label { Text = "Email address" },
    					emailEntry,
    					signUpButton,
    					messageLabel
    				}
    			};
    		}
    
    		async void OnSignUpButtonClicked (object sender, EventArgs e)
    		{
    			var user = new User () {
    				Username = usernameEntry.Text,
    				Password = passwordEntry.Text,
    				Email = emailEntry.Text
    			};
    
    			// Sign up logic goes here
    
    			var signUpSucceeded = AreDetailsValid (user);
    			if (signUpSucceeded) {
    				var rootPage = Navigation.NavigationStack.FirstOrDefault ();
    				if (rootPage != null) {
    					App.IsUserLoggedIn = true;
    					Navigation.InsertPageBefore (new MainPageCS (), Navigation.NavigationStack.First ());
    					await Navigation.PopToRootAsync ();
    				}
    			} else {
    				messageLabel.Text = "Sign up failed";
    			}
    		}
    
    		bool AreDetailsValid (User user)
    		{
    			return (!string.IsNullOrWhiteSpace (user.Username) && !string.IsNullOrWhiteSpace (user.Password) && !string.IsNullOrWhiteSpace (user.Email) && user.Email.Contains ("@"));
    		}
    	}
    }
    

\- 다시 클래스 파일을 하나더 추가 합니다

![](/assets/images/xamarin_forms_자마린으로_간단한_로그인_앱_만들기/img_16.jpg)

\- 클래스 명칭은 User.cs 입니다

![](/assets/images/xamarin_forms_자마린으로_간단한_로그인_앱_만들기/img_2.png)

\- 추가된 User.cs 파일에 아래와 같이 코딩 합니다

*User.cs
    
    
    namespace LoginNavigation
    {
    	public class User
    	{
    		public string Username { get; set; }
    
    		public string Password { get; set; }
    
    		public string Email { get; set; }
    	}
    }
    

이제 여기까지 완료 하셨다면 코딩은 모두 끝낫습니다

빌드를 돌려 에뮬레이터를 실행해 주세요.

혹시 저와 같이 디바이스 빌드를 하실 분이라면 아래 링크를 참고해 주세요

<https://codingman.tistory.com/95>

[ [Microsoft Visual Studio 2017] Xamarin 디바이스로 디버깅 하기 안녕하세요 코딩연습생입니다 요즘 코로나
때문에 난리도 아니죠?ㅠ 제 주변에도 온통 관심사가 코로나에 가있습니다 이런 시국에 회사에서는 왜이렇게 일을 많이 주는걸까요....참
이해하기 힘든...ㅋㅋ 이번 포.. codingman.tistory.com ](https://codingman.tistory.com/95)

빌드가 완료가 되면 앱이 실행됩니다

![](/assets/images/xamarin_forms_자마린으로_간단한_로그인_앱_만들기/img_17.jpg)

정말 심플한 화면이 나오게 됩니다

다음번 포스팅에서 MSSQL와 연동하여 로그인 시키는 부분을 포스팅 하도록 하겠습니다

감사합니다~

  

#어플만들기 #앱만들기 #cross-platform #자마린 #Xamarin Forms #xamarin 로그인페이지 #로그인만들기
#비쥬얼스튜디오 앱 만들기

