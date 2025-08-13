---
categories:
  - 'Blog'
tags:
  - '안드로이드'
  - '앱만들기'
  - '자마린'
  - 'Xamarin'
  - '앱'
  - '로그인앱만들기'
last_modified_at: '2025-05-30T16:04:01+09:00'
title: '[2025-08-13] - Post'
excerpt: ''
layout: 'post'
lang: 'ko'
permalink: '/posts/2020-03-19-xamarin_forms_자마린으로_간단한_앱_회원가입_만들기/'
alt_en: '/en/posts/2020-03-19-xamarin_forms_자마린으로_간단한_앱_회원가입_만들기/'
---

## [Xamarin Forms] 자마린으로 간단한 앱 회원가입 만들기

코딩정보/Android

2020-03-19 11:40:58

* * *

안녕하세요

포스팅으로 열공하고 있는 코딩연습생입니다

저번 포스팅에서 비쥬얼스튜디오 2017을 이용하여 간단한 로그인 앱 만드는 방법을 포스팅했는데요

그 포스팅에 이어 로그인 할때 계정이 없을 경우 회원가입을 해야 하지요?

그래서 MSSQL와 연동하여 회원가입이 가능하도록 한번 만들어 봤습니다

물론 회원가입시에 ID 중복체크, 패스워트 생성 규칙, 주소 검색, 등 많은 기능이 필요한데

이번 시간에는 기초적인 부분만 만들어 보았습니다

첫번째 ID생성(문자열)

두번째 패스워드(문자열)

세번째 이메일(문자열)

이렇게 3가지만 등록한뒤 생성 버튼을 클릭하면 DB에 Data가 생성되어 로그인이 되도록 하는 구조 입니다

이렇게 기초 적인 부분을 만든뒤 차츰차츰 기능을 하나씩 구현하는게 바로 코딩에 재미겠죠ㅎ

그럼 진행해 보도록 하겠습니다

일단 저번 시간 포스팅까지 완성이 되어야 이어서 가능하니 아래 링크를 통해서 로그인 샘플 먼저 완성해주세요

<https://codingman.tistory.com/96>

[ [Xamarin Forms] 자마린으로 간단한 로그인 앱 만들기 안녕하세요. 코딩연습생입니다 비쥬얼스튜디오 Xamarin을 이용한 로그인
창 만들기 입니다 저도 처음 접해보는 부분이라 많이 헷갈리고 연습을 하고 있습니다~ 음..일단 시작에 앞서 비쥬얼스튜디오의 Cross-
Platf.. codingman.tistory.com ](https://codingman.tistory.com/96)

그러면 해당 프로젝트 파일 중에 해당 위치로 찾아 갑니다

로그인 화면에서 이미 만들어져 있는 부분인데 그 부분에서 INSERT 부분만 추가가 된것입니다

*SignUpPage.xaml.cs
    
    
    using System;
    using System.Linq;
    using Xamarin.Forms;
    using System.Data;
    using System.Data.SqlClient;
    
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
    
                
                CreateSign();
    
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
    
            public void CreateSign()
            {
                SqlConnectionStringBuilder sqlConnectionStringBuilder = new SqlConnectionStringBuilder();
                sqlConnectionStringBuilder.DataSource = "서버IP";
                sqlConnectionStringBuilder.InitialCatalog = "DB명";
                sqlConnectionStringBuilder.UserID = "계정";
                sqlConnectionStringBuilder.Password = "계정암호";
                sqlConnectionStringBuilder.IntegratedSecurity = false;
                SqlConnection conn = new SqlConnection(sqlConnectionStringBuilder.ConnectionString);
                conn.Open();
    
                try
                {
                    string Query = "MERGE USER_MAST";
                    Query += "            USING(SELECT 'X' AS DUAL) AS B ";
                    Query += "               ON [USER_ID] = '" + usernameEntry.Text + "'";
                    Query += "            WHEN MATCHED THEN";
                    Query += "                 UPDATE SET USER_PSWD = '" + passwordEntry.Text + "'";
                    Query += "            WHEN NOT MATCHED THEN";
                    Query += "                 INSERT([USER_ID], USER_PSWD) VALUES ('" + usernameEntry.Text + "','" + passwordEntry.Text + "');";
                    SqlCommand cmd = new SqlCommand();
                    cmd.Connection = conn;
    
                    cmd.CommandText = Query;
                    cmd.ExecuteNonQuery();
                    conn.Close();
                }
                catch (Exception Ex)
                {
                    conn.Close();
                }
                finally
                {
                    conn.Close();
                }
            }
    
            bool AreDetailsValid (User user)
    		{
    			return (!string.IsNullOrWhiteSpace (user.Username) && !string.IsNullOrWhiteSpace (user.Password) && !string.IsNullOrWhiteSpace (user.Email) && user.Email.Contains ("@"));
    		}
    	}
    }
    

*SignUpPageCS.cs
    
    
    using System;
    using System.Linq;
    using Xamarin.Forms;
    using System.Data;
    using System.Data.SqlClient;
    
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
    
                CreateSign();
    
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
    
            public void CreateSign()
            {
                SqlConnectionStringBuilder sqlConnectionStringBuilder = new SqlConnectionStringBuilder();
                sqlConnectionStringBuilder.DataSource = "서버IP";
                sqlConnectionStringBuilder.InitialCatalog = "DB명";
                sqlConnectionStringBuilder.UserID = "계정";
                sqlConnectionStringBuilder.Password = "계정암호";
                sqlConnectionStringBuilder.IntegratedSecurity = false;
                SqlConnection conn = new SqlConnection(sqlConnectionStringBuilder.ConnectionString);
                conn.Open();
    
                try
                {
                    string Query = "MERGE USER_MAST";
                    Query += "            USING(SELECT 'X' AS DUAL) AS B ";
                    Query += "               ON [USER_ID] = '" + usernameEntry.Text + "'";
                    Query += "            WHEN MATCHED THEN";
                    Query += "                 UPDATE SET USER_PSWD = '" + passwordEntry.Text + "'";
                    Query += "            WHEN NOT MATCHED THEN";
                    Query += "                 INSERT([USER_ID], USER_PSWD) VALUES ('" + usernameEntry.Text + "','" + passwordEntry.Text + "');";
                    SqlCommand cmd = new SqlCommand();
                    cmd.Connection = conn;
    
                    cmd.CommandText = Query;
                    cmd.ExecuteNonQuery();
                    conn.Close();
                }
                catch (Exception Ex)
                {
                    conn.Close();
                }
                finally
                {
                    conn.Close();
                }
            }
    
            bool AreDetailsValid (User user)
    		{
    			return (!string.IsNullOrWhiteSpace (user.Username) && !string.IsNullOrWhiteSpace (user.Password) && !string.IsNullOrWhiteSpace (user.Email) && user.Email.Contains ("@"));
    		}
    	}
    }
    

그런데 위의 INSERT 구문을 보시면 일반적인 INSERT문하고 조금 차이가 있죠??

제가 올린 포스팅 내용중에 보시면 INSERT와 UPDATE를 한번에 처리하는 구문입니다

자세한건 아래 링크를 통해서 확인해보시면 됩니다

<https://codingman.tistory.com/98>

[ [MSSQL] MERGE를 이용한 INSERT와 UPDATE 한번에 하기 안녕하세요~ 코딩 연습생입니다 코로나 사태 여러분
괜찮으신가요?? 언제쯤 잠잠해질지 참...얼른 백신이나 대책이 나왔으면 좋겠는데 마스크 때문에 숨도 잘 안쉬어지네요~ 그래도 할건
해야겠죠?ㅎㅎ 그래서 저.. codingman.tistory.com ](https://codingman.tistory.com/98)

이렇게 소스코딩을 완료 하셨다면 이제 빌드를 진행하여 실행을 해봐야겠죠?

로그인 메인 화면에서 우측 상단에 있는 SIGN UP이라는 글씨를 클릭하면 회원가입 화면으로 이동합니다

![](/assets/images/xamarin_forms_자마린으로_간단한_앱_회원가입_만들기/img.jpg)

회원 가입 페이지로 이동하게 되면 아래와 같은 화면이 보이게 됩니다

![](/assets/images/xamarin_forms_자마린으로_간단한_앱_회원가입_만들기/img_1.jpg)

회원가입 화면에서 Username(계정명), Password(패스워트), Email address(이메일) 정보를 입력합니다

*굳이 저랑 똑같이 입력하지 않으셔도 됩니다

저는 빨간색 글씨 처럼 입력 하였습니다

정보 입력이 모두 되셨다면 아래 SIGN UP 버튼을 누루시면 컨텐츠 메인 화면으로 이동하게 됩니다

![](/assets/images/xamarin_forms_자마린으로_간단한_앱_회원가입_만들기/img_2.jpg)

컨텐츠 메인 화면으로 정상적으로 이동하셨다면 다음과 같이 우측 상단의 글씨 LOGOUT으로 변경이 됩니다

![](/assets/images/xamarin_forms_자마린으로_간단한_앱_회원가입_만들기/img_3.jpg)

그러면 MSSQL DB에 정상적으로 데이터가 입력되었는지 확인해 볼까요?

SQL에서 USER_MAST 테이블을 조회해 보니 정상적으로 값이 INSERT 되었네요

만약에 이미 USER_MAST 테이블에 "테스트"라는 계정이 존재했다면 INSERT가 아니라 UPDATE가 진행되었을 겁니다

![](/assets/images/xamarin_forms_자마린으로_간단한_앱_회원가입_만들기/img.png)

회원가입의 기본적인 기능이 담겨 있는 내용인데요

이부분에서 앞써 말씀드렸던 추가적인 기능들이 첨가가 된다면 좀더 있어보이는(?)ㅎ 그런 회원가입이 되지 않을까요?ㅎ

저도 시간을 투자해서 좀 더 발전시켜 봐야겠습니다

  

#안드로이드 #앱만들기 #자마린 #Xamarin 회원가입 #앱 회원가입 #로그인앱만들기

