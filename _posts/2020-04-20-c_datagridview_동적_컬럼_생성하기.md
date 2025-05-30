---
title:  "[2020-04-20] - [C#] DataGridView 동적 컬럼 생성하기"
categories:
  - Blog
tags:
  - "c#"
  - "MSSQL"
  - "엑셀불러오기"
  - "데이터그리드뷰"
  - "동적컬럼생성하기"
  - "DATAGRIDVIEW"
last_modified_at: 2025-05-30T16:04:02+09:00
---

## [C#] DataGridView 동적 컬럼 생성하기

코딩정보/C#

2020-04-20 14:19:42

* * *

안녕하세요

코딩연습생입니다

이번 시간에 포스팅하고자 하는건 제목에도 나와 있지만

MSSQL을 통해서 C#으로 DataGridView 컨트롤의 컬럼을 동적으로 생성하게 하여

한 페이지에서 여러 Data를 조회 할 수 있는 유동적인 DataGirdView를 사용하는 방법을 포스팅 해볼려고 합니다

말은 거창한데 결국은 데이터그리드뷰의 속성을 하나씩 설정해서 유동적으로 사용하게 하는 방법입니다

첫번째는 조회 타입에 따라 변화 할 그리드뷰의 속성을 MSSQL에서 프로시져로 지정 합니다

    
    
    IF @GUBUN = 'COL_CNT_MANDO'
    		BEGIN
    			SELECT 37 AS CNT    --전체 컬럼 출력수
    		END
    		
    		IF @GUBUN = 'COL_CNT_ETC'
    		BEGIN
    			SELECT 22 AS CNT    --전체 컬럼 출력수
    		END
    
    
    		IF @GUBUN = 'COL_NAD_MANDO'
    		BEGIN
    			SELECT '고객코드' AS COL_NM
    			UNION ALL
    			SELECT '고객명' AS COL_NM
    			UNION ALL
    			SELECT 'ERP 품번' AS COL_NM
    			UNION ALL
    			SELECT '거래선 도번' AS COL_NM
    			UNION ALL
    			SELECT '납품처코드' AS COL_NM
    			UNION ALL
    			SELECT '납품처명' AS COL_NM
    			UNION ALL
    			SELECT '차종명' AS COL_NM
    			UNION ALL
    			SELECT '*D+0(주간)' AS COL_NM
    			UNION ALL
    			SELECT '*D+0(야간)' AS COL_NM
    			UNION ALL
    			SELECT '*D+1(주간)' AS COL_NM
    			UNION ALL
    			SELECT '*D+1(야간)' AS COL_NM
    			UNION ALL
    			SELECT '*D+2(주간)' AS COL_NM
    			UNION ALL
    			SELECT '*D+2(야간)' AS COL_NM
    			UNION ALL
    			SELECT '*D+3(주간)' AS COL_NM
    			UNION ALL
    			SELECT '*D+3(야간)' AS COL_NM
    			UNION ALL
    			SELECT '*D+4(주간)' AS COL_NM
    			UNION ALL
    			SELECT '*D+4(야간)' AS COL_NM
    			UNION ALL
    			SELECT '*D+5(주간)' AS COL_NM
    			UNION ALL
    			SELECT '*D+5(야간)' AS COL_NM
    			UNION ALL
    			SELECT '*D+6(주간)' AS COL_NM
    			UNION ALL
    			SELECT '*D+6(야간)' AS COL_NM
    			UNION ALL
    			SELECT '*D+7(주간)' AS COL_NM
    			UNION ALL
    			SELECT '*D+7(야간)' AS COL_NM
    			UNION ALL
    			SELECT '*D+8(주간)' AS COL_NM
    			UNION ALL
    			SELECT '*D+8(야간)' AS COL_NM
    			UNION ALL
    			SELECT '*D+9(주간)' AS COL_NM
    			UNION ALL
    			SELECT '*D+9(야간)' AS COL_NM
    			UNION ALL
    			SELECT '*D+10(주간)' AS COL_NM
    			UNION ALL
    			SELECT '*D+10(야간)' AS COL_NM
    			UNION ALL
    			SELECT '*D+11(주간)' AS COL_NM
    			UNION ALL
    			SELECT '*D+11(야간)' AS COL_NM
    			UNION ALL
    			SELECT '*D+12(주간)' AS COL_NM
    			UNION ALL
    			SELECT '*D+12(야간)' AS COL_NM
    			UNION ALL
    			SELECT '*D+13(주간)' AS COL_NM
    			UNION ALL
    			SELECT '*D+13(야간)' AS COL_NM
    		END
    
    		IF @GUBUN = 'COL_NAD_ETC'
    		BEGIN
    			SELECT '고객코드' AS COL_NM
    			UNION ALL
    			SELECT '고객명' AS COL_NM
    			UNION ALL
    			SELECT 'ERP 품번' AS COL_NM
    			UNION ALL
    			SELECT '거래선 도번' AS COL_NM
    			UNION ALL
    			SELECT '납품처코드' AS COL_NM
    			UNION ALL
    			SELECT '납품처명' AS COL_NM
    			UNION ALL
    			SELECT '차종명' AS COL_NM
    			UNION ALL
    			SELECT '*D+0' AS COL_NM
    			UNION ALL
    			SELECT '*D+1' AS COL_NM
    			UNION ALL
    			SELECT '*D+2' AS COL_NM
    			UNION ALL
    			SELECT '*D+3' AS COL_NM
    			UNION ALL
    			SELECT '*D+4' AS COL_NM
    			UNION ALL
    			SELECT '*D+5' AS COL_NM
    			UNION ALL
    			SELECT '*D+6' AS COL_NM
    			UNION ALL
    			SELECT '*D+7' AS COL_NM
    			UNION ALL
    			SELECT '*D+8' AS COL_NM
    			UNION ALL
    			SELECT '*D+9' AS COL_NM
    			UNION ALL
    			SELECT '*D+10' AS COL_NM
    			UNION ALL
    			SELECT '*D+11' AS COL_NM
    			UNION ALL
    			SELECT '*D+12' AS COL_NM
    			UNION ALL
    			SELECT '*D+13' AS COL_NM
    		END

위의 쿼리내용을 보게 되면 미리 타입에 따라 컬럼 갯수와 컬럼명칭을 설정해서 가져오기 위한 쿼리 입니다

유동적인 그리드뷰를 적용시킬 윈폼 페이지 안에 아래와 같이 코딩을 합니다

    
    
    private void Grid_Column()
            {
                this.Cursor = Cursors.WaitCursor;   //마우스 커서를 Waitting
    
                dataGridView1.Rows.Clear();  //그리드뷰 초기화
                dataGridView1.Columns.Clear(); //
    
                string query = "";
                if (radioButton1.Checked == true)
                {
                    query += "EXEC SP_SHIP_CUST_PLAN ";
                    query += "     'COL_CNT_MANDO'";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
    
                }
                else
                {
                    query += "EXEC SP_SHIP_CUST_PLAN ";
                    query += "     'COL_CNT_ETC'";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                }
                
                
                //MSSQL 프로바이더
                DB db = new DB();
                DataTable dt = db.ExcuteQuery(query);
    
                //datatable의 내용을 그리드에 display
                foreach (DataRow row in dt.Rows)
                {
                    dataGridView1.ColumnCount = Convert.ToInt32(row[0].ToString());
                }
    
                dt.Clear();
    
    
                query = "";
                if (radioButton1.Checked == true)
                {
                    query += "EXEC SP_SHIP_CUST_PLAN ";
                    query += "     'COL_NAD_MANDO'";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                }
                else
                {
                    query += "EXEC SP_SHIP_CUST_PLAN ";
                    query += "     'COL_NAD_ETC'";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                    query += "    ,''";
                }
                dt = db.ExcuteQuery(query);
    
                int i = 0;
    
                //datatable의 내용을 그리드에 display
                foreach (DataRow row in dt.Rows)
                {
                    dataGridView1.Columns[i].Name = row["COL_NM"].ToString();
                    //sGridView1.Columns[i].SortMode = DataGridViewColumnSortMode.NotSortable;
    
                    //숫자컬럼은 앞에*를 붙였기때문에 숫자컬럼은 모두 오른쪽 정렬을 취함
                    if (row["COL_NM"].ToString().Substring(0, 1) == "*")
                    {
                        dataGridView1.Columns[i].DefaultCellStyle.Alignment = DataGridViewContentAlignment.MiddleRight;  //우측정렬
                    }
                    //문자열은 좌측정렬구분자를 공백으로 처리
                    else if (row["COL_NM"].ToString().Substring(0, 1) == " ")
                    {
                        dataGridView1.Columns[i].DefaultCellStyle.Alignment = DataGridViewContentAlignment.MiddleLeft;  //좌측정렬
                    }
                    else
                    {
                        dataGridView1.Columns[i].DefaultCellStyle.Alignment = DataGridViewContentAlignment.MiddleCenter;  //가운데정렬
                    }
    
                    i++;
                }
    
                this.Cursor = Cursors.Default;
                dataGridView1.AllowUserToAddRows = false;
            }

여기서 MSSQL DB에 접속하기 위한 프로바이더는 별도 함수로 작성해서 사용하였습니다

함수 제작하는 방법은 아래 링크 페이지에서 확인 하시기 바랍니다

<https://codingman.tistory.com/73>

[ [C#] MSSQL 접속하고 사용하기 안녕하세요 C# 컨텐츠로 블로그를 운영중인 코딩 연습생입니다 이번 포스팅에서는 C#으로 MSSQL를
접속하고 쿼리문을 전송시켜 연동시키기까지 한번 해보도록 하겠습니다 일반적인 방법으로는 1) 접속정보 생성 2)..
codingman.tistory.com ](https://codingman.tistory.com/73)

이렇게 타입에 따른 그리드뷰 상세 옵션을 MSSQL에서 불러와서 그리드를 그려준뒤에 각 컬럼에 맞게 뿌려주면 됩니다

저는 유동적으로 생성된 그리드뷰에 엑셀파일을 불러오기로 구현하였습니다

    
    
    private void hoverGradientButton3_Click(object sender, EventArgs e)
            {
                OpenFileDialog oFileDialog = new OpenFileDialog();
                oFileDialog.Filter = "Excel (*.xlsx)|*.xlsx|Excel 97-2003 (*.xls)|*.xls";
    
                if (oFileDialog.ShowDialog() != DialogResult.OK)
                {
                    return;
                }
    
                Excel.Application xlApp;
                Excel.Workbook xlWorkBook;
                Excel.Worksheet xlWorkSheet;
                Excel.Range range;
    
                string str;
                int rCnt = 0;
                int cCnt = 0;
                string sCellData = "";
                double dCellData;
    
                xlApp = new Excel.Application();
                xlApp.DisplayAlerts = false;
                xlApp.Visible = false;
                xlApp.ScreenUpdating = false;
                xlApp.DisplayStatusBar = false;
                xlApp.EnableEvents = false;
    
                SplashWnd.SplashShow();
    
                try
                {
                    xlWorkBook = xlApp.Workbooks.Open(oFileDialog.FileName, 0, true, 5, "", "", true, Excel.XlPlatform.xlWindows, "\t", false, false, 0, true, 1, 0);
                    xlWorkSheet = (Excel.Worksheet)xlWorkBook.Worksheets.get_Item(1);
    
                    range = xlWorkSheet.UsedRange;
    
                    DataTable dt = new DataTable();
    
                    // 첫 행을 제목으로
                    for (cCnt = 1; cCnt <= range.Columns.Count; cCnt++)
                    {
                        str = (string)(range.Cells[1, cCnt] as Excel.Range).Value2;
                        dt.Columns.Add(str, typeof(string));
                    }
    
                    for (rCnt = 3; rCnt <= range.Rows.Count; rCnt++)
                    {
                        string sData = "";
                        for (cCnt = 1; cCnt <= range.Columns.Count; cCnt++)
                        {
                            try
                            {
                                sCellData = (string)(range.Cells[rCnt, cCnt] as Excel.Range).Value2;
                                sData += sCellData + "|";
                            }
                            catch (Exception ex)
                            {
                                dCellData = (double)(range.Cells[rCnt, cCnt] as Excel.Range).Value2;
                                sData += dCellData.ToString() + "|";
                            }
                        }
                        sData = sData.Remove(sData.Length - 1, 1);
                        dt.Rows.Add(sData.Split('|'));
                    }
    
                    int i = 0;
    
                    if (radioButton1.Checked == true)
                    {
                        foreach (DataRow row in dt.Rows)
                        {
                            dataGridView1.Rows.Add(1);
    
                            for (int j=0; j<= 34; j++)
                            {    
                                dataGridView1.Rows[i].Cells[j].Value = dt.DefaultView[i][j].ToString();
                            }
                           
                            i++;
                        }
                    }
                    else
                    {
                        foreach (DataRow row in dt.Rows)
                        {
                            dataGridView1.Rows.Add(1);
    
                            for (int j = 0; j <= 20; j++)
                            {
                                dataGridView1.Rows[i].Cells[j].Value = dt.DefaultView[i][j].ToString();
                            }
    
    
                            i++;
                        }
                    }
                    
                    //dataGridView1.DataSource = dt.DefaultView;
    
                    xlWorkBook.Close(true, null, null);
                    xlApp.Quit();
    
                    releaseObject(xlWorkSheet);
                    releaseObject(xlWorkBook);
                    releaseObject(xlApp);
    
                    SplashWnd.SplashClose(this);
    
                }
                catch (Exception ex)
                {
                    MessageBox.Show("파일 열기 실패! : " + ex.Message);
                    return;
                }
            }
    
            private void releaseObject(object obj)
            {
                try
                {
                    System.Runtime.InteropServices.Marshal.ReleaseComObject(obj);
                    obj = null;
                }
                catch (Exception ex)
                {
                    obj = null;
                    MessageBox.Show("Unable to release the Object " + ex.ToString());
                }
                finally
                {
                    GC.Collect();
                }
            }

이렇게 되면 불러오고자 하는 엑셀 문서의 타입에 따라 데이터그리드뷰를 생성시켜 주고 그 위에 엑셀의 내용을

불러오기 하여 보여질수 있게 됩니다

엑셀 양식 불러오기를 사용할때 고객의 종류? 양식의 타입?에 따라 변동이 많을시에 이렇게 데이터그리드뷰를

유동적으로 변화시킬수 있다면 굳이 여러개의 폼을 만들지 않고 하나의 폼에서 처리가 가능하니 조금 사용자 입장에서

편리할수 있다고 생각해서 구현해 봤습니다

  

#c# #MSSQL 연동 #엑셀불러오기 #데이터그리드뷰 동적컬럼 #동적컬럼생성하기 #DATAGRIDVIEW 해더생성

