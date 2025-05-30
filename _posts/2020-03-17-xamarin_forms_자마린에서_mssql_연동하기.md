---
title:  "[2020-03-17] - [Xamarin Forms] 자마린에서 MSSQL 연동하기"
categories:
  - Blog
tags:
  - "MSSQL"
  - "DB"
  - "xamarin"
  - "로그인"
  - "안드로이드"
  - "MSSQL"
last_modified_at: 2025-05-30T16:04:01+09:00
---

## [Xamarin Forms] 자마린에서 MSSQL 연동하기

코딩정보/Android

2020-03-17 09:09:46

* * *

안녕하세요

코딩연습생입니다~

오늘 포스팅은 저번 시간 포스팅에 이어서 진행 하고자 합니다

저번 시간 포스팅에서 자마린 Cross-Platform을 사용해서 로그인 화면을 만들어 봤습니다

정보는 아래 링크를 참고해 주세요

<https://codingman.tistory.com/96>

[ [Xamarin Forms] 자마린으로 간단한 로그인 앱 만들기 안녕하세요. 코딩연습생입니다 비쥬얼스튜디오 Xamarin을 이용한 로그인
창 만들기 입니다 저도 처음 접해보는 부분이라 많이 헷갈리고 연습을 하고 있습니다~ 음..일단 시작에 앞서 비쥬얼스튜디오의 Cross-
Platf.. codingman.tistory.com ](https://codingman.tistory.com/96)

저번 시간에 만들었던 로그인 앱에서 로그인 인증 시도 할때

MSSQL과 연동시켜 인증처리 되도록 구현을 해볼려고 합니다

앱에서 MSSQL과 연동 할때 여러가지 방법이 있다고 합니다

하지만 저는 C# 개발자였기에;; 기존과 비슷한 벙법으로 MSSQL에 접속을 구현해 봤습니다

자마린에서 MSSQL에 접속을 하기 위해서는 몇가지 사전 준비가 필요한데요

Nuget을 사용해서 필요한 패키지를 설치 하면 됩니다 어렵지는 않아요

1\. Nuget을 사용하기

\- C# 프로젝트 위치에서 Nuget 패키지 관리를 클릭 합니다

![](/assets/images/xamarin_forms_자마린에서_mssql_연동하기/img.jpg)

2\. System.Data.SqlClient 설치 하기

\- Nuget 패키지 관리창에서 System.Data.SqlClient를 검색하여 설치 합니다

![](/assets/images/xamarin_forms_자마린에서_mssql_연동하기/img_1.jpg)

3\. using문 선언

\- SQL 클래스 사용을 위한 using문을 선업합니다

    
    
    using System.Data;
    using System.Data.SqlClient;

4\. 로그인 인증을 위한 단계 구성

\- 기존 로그인 앱에서 Login 버튼이 활성화 되는 위치에서 DB 정보를 불러오도록 할겁니다

*LiginPage.xaml.cs

① 해당 위치에서 로그인 버튼 클릭이 일어는 위치를 다음과 같이 수정 합니다 Connet();만 추가했습니다

② Connet() 구문을 추가 했습니다

    
    
    async void OnLoginButtonClicked (object sender, EventArgs e)
    		{
    			var user = new User {
    				Username = usernameEntry.Text,
    				Password = passwordEntry.Text
    			};
    
                Connet();
    
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
    
    
    public void Connet()
            {
                DataRowCollection Rs = null;
    
                SqlConnectionStringBuilder sqlConnectionStringBuilder = new SqlConnectionStringBuilder();
                sqlConnectionStringBuilder.DataSource = "서버IP주소";
                sqlConnectionStringBuilder.InitialCatalog = "DB명";
                sqlConnectionStringBuilder.UserID = "계정ID";
                sqlConnectionStringBuilder.Password = "계정 비밀 번호";
                sqlConnectionStringBuilder.IntegratedSecurity = false;
                SqlConnection conn = new SqlConnection(sqlConnectionStringBuilder.ConnectionString);
                conn.Open();
    
                try
                {
                    SqlDataAdapter adapter = new SqlDataAdapter();
                    string Query = "SELECT [USER_ID], USER_PSWD";
                    Query += "        FROM USER_MAST";
                    Query += "       WHERE 1=1";
                    Query += "         AND [USER_ID] = '" + usernameEntry.Text + "'";
                    adapter.SelectCommand = new SqlCommand(Query, conn);
                    DataSet ds = new DataSet();
                    adapter.Fill(ds);
                    DataTable table = ds.Tables[0];
                    Rs = table.Rows;
    
                    if (Rs != null && Rs.Count > 0)
                    {
                        Constants.Username = Rs[0]["USER_ID"].ToString();
                        Constants.Password = Rs[0]["USER_PSWD"].ToString();
                    }
                }
                catch (Exception Ex)
                {
                    conn.Close();
                }
                finally
                {
                    if (Rs != null) { Rs.Clear(); Rs = null; }
                    conn.Close();
                }
            }

*LoginPageCS.cs

위와 동일하게 적용해 줍니다

    
    
    async void OnLoginButtonClicked (object sender, EventArgs e)
    		{
    			var user = new User {
    				Username = usernameEntry.Text,
    				Password = passwordEntry.Text
    			};
    
                Connet();
    
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
    
    
    public void Connet()
            {
                DataRowCollection Rs = null;
    
                SqlConnectionStringBuilder sqlConnectionStringBuilder = new SqlConnectionStringBuilder();
                sqlConnectionStringBuilder.DataSource = "서버IP주소";
                sqlConnectionStringBuilder.InitialCatalog = "DB명";
                sqlConnectionStringBuilder.UserID = "계정ID";
                sqlConnectionStringBuilder.Password = "계정 비밀 번호";
                sqlConnectionStringBuilder.IntegratedSecurity = false;
                SqlConnection conn = new SqlConnection(sqlConnectionStringBuilder.ConnectionString);
                conn.Open();
    
                try
                {
                    SqlDataAdapter adapter = new SqlDataAdapter();
                    string Query = "SELECT [USER_ID], USER_PSWD";
                    Query += "        FROM USER_MAST";
                    Query += "       WHERE 1=1";
                    Query += "         AND [USER_ID] = '" + usernameEntry.Text + "'";
                    adapter.SelectCommand = new SqlCommand(Query, conn);
                    DataSet ds = new DataSet();
                    adapter.Fill(ds);
                    DataTable table = ds.Tables[0];
                    Rs = table.Rows;
    
                    if (Rs != null && Rs.Count > 0)
                    {
                        Constants.Username = Rs[0]["USER_ID"].ToString();
                        Constants.Password = Rs[0]["USER_PSWD"].ToString();
                    }
                }
                catch (Exception Ex)
                {
                    conn.Close();
                }
                finally
                {
                    if (Rs != null) { Rs.Clear(); Rs = null; }
                    conn.Close();
                }
            }

이렇게 하시면 MSSQL에 접속하여 인증을 받아 로그인 성공/실패가 됩니다

다음시간에는 SignUpPageCS.cs부분인 회원가입 부분을 수정해서 MSSQL와 연동한

계정 등록 방법에 대해 포스팅 해보도록 할께요~

  

#MSSQL #DB #xamarin mssql #로그인 앱 #안드로이드 MSSQL 연동 #MSSQL 연동

