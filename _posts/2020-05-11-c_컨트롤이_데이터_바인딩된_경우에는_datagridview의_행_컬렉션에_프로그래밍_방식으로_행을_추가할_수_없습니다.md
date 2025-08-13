---
categories:
  - 'Blog'
tags:
  - 'C#'
  - '그리드뷰바인딩오류'
  - 'Row추가'
  - '그리드뷰'
  - '행'
last_modified_at: '2025-05-30T16:04:02+09:00'
title: '[2025-08-13] - Post'
excerpt: ''
layout: 'post'
lang: 'ko'
permalink: '/posts/2020-05-11-c_컨트롤이_데이터_바인딩된_경우에는_datagridview의_행_컬렉션에_프로그래밍_방식으로_행을_추가할_수_없습니다/'
alt_en: '/en/posts/2020-05-11-c_컨트롤이_데이터_바인딩된_경우에는_datagridview의_행_컬렉션에_프로그래밍_방식으로_행을_추가할_수_없습니다/'
---

<div class="lang-panel lang-ko" lang="ko">
## [C#]컨트롤이 데이터 바인딩된 경우에는 datagridview의 행 컬렉션에 프로그래밍 방식으로 행을 추가할 수 없습니다

코딩정보/C#

2020-05-11 10:29:04

* * *

안녕하세요

코딩연습생입니다

C# WINFORM 환경에서 DB 위치에서 데이터를 받아 DataGridView에 데이터를 바인딩 한뒤

Row추가 진행시 다음과 같은 오류가 발생합니다

![](/assets/images/c_컨트롤이_데이터_바인딩된_경우에는_datagridview의_행_컬렉션에_프로그래밍_방식으로_행을_추가할_수_없습니다/img.png)

이럴경우 DataTable를 이용해서 해결 할 수 있는데요

일단 프로시져의 내용을 DataGridView에 바인딩 시켜 줍니다.

    
    
    private void Load()
            {
                string query = "EXEC SP_SHIP_DELIVERY_LIST";
                query += "           'SELECT',";                         //구분
                query += "           '" + textBox1.Text + "',";          //Cust_Code
                query += "           '" + textBox3.Text + "',";          //Delivery_Code
                query += "           '" + textBox2.Text + "',";          //Part_Code
                query += "           '" + textBox4.Text + "',";          //Cust_GridNo
                query += "           '',";                               //Part_Name
                query += "           '',";                               //Active
                query += "           ''";                                //Remark
                SAC_MesDB db = new SAC_MesDB();
                
                dataGridView1.DataSource = db.ExcuteQuery(query);
    
                dataGridView1.Columns[0].ReadOnly = true;
                dataGridView1.Columns[1].ReadOnly = true;
                dataGridView1.Columns[2].ReadOnly = true;
            }

간단합니다.

MSSQL에 있는 SP_SHIP_DELIVERY_LIST 프로시져를 호출해서 DataGridView에 바인딩 시키는 부분입니다

그런데 문제는 이게 아니죠

DataGridView에 데이터바인딩 이후에 Row 추가를 하게 되면 다음과 같은 오류가 발생합니다

_"컨트롤이 데이터 바인딩된 경우에는 datagridview의 행 컬렉션에 프로그래밍 방식으로 행을 추가할 수 없습니다"_

그래서 폭풍 검색을 했더니 DataTable에 담아 그리드가 아닌 dt에 Row를 추가하면 동작한다고 해서 변경해 봤습니다

    
    
    private void Load()
            {
            	DataTable dt = new DataTable();
                
                string query = "EXEC SP_SHIP_DELIVERY_LIST";
                query += "           'SELECT',";                         //구분
                query += "           '" + textBox1.Text + "',";          //Cust_Code
                query += "           '" + textBox3.Text + "',";          //Delivery_Code
                query += "           '" + textBox2.Text + "',";          //Part_Code
                query += "           '" + textBox4.Text + "',";          //Cust_GridNo
                query += "           '',";                               //Part_Name
                query += "           '',";                               //Active
                query += "           ''";                                //Remark
                SAC_MesDB db = new SAC_MesDB();
                
                dt = new DataTable();
                
                dt = db.ExcuteQuery(query);
                
                dataGridView1.DataSource = dt;
    
                dataGridView1.Columns[0].ReadOnly = true;
                dataGridView1.Columns[1].ReadOnly = true;
                dataGridView1.Columns[2].ReadOnly = true;
            }

이렇게 구문을 바꾸어서 Row를 추가해 봤습니다

Row를 추가하는 버튼 이벤트 입니다

    
    
    private void hoverGradientButton3_Click(object sender, EventArgs e)
            {
                int MaxRow = dataGridView1.Rows.Count;
    
                if (MaxRow >= 0)
                {
                    if (dataGridView1.Rows[MaxRow - 1].Cells[0].Value.ToString() != "")
                    {
                        string[] row0 = { "", "", "", "", "", "", "" };
                        dt.Rows.Add(row0);
                        
                        dataGridView1.Rows[dataGridView1.Rows.Count - 1].Cells[0].Style.BackColor = Color.Yellow;
                        dataGridView1.Rows[dataGridView1.Rows.Count - 1].Cells[1].Style.BackColor = Color.Yellow;
                        dataGridView1.Rows[dataGridView1.Rows.Count - 1].Cells[2].Style.BackColor = Color.Yellow;
                    }
                    else
                    {
                        MessageBox.Show("추가 등록은 한번에 하나씩만 가능합니다.");
                    }
                }
            }

오옷!! 동작을 합니다

![](/assets/images/c_컨트롤이_데이터_바인딩된_경우에는_datagridview의_행_컬렉션에_프로그래밍_방식으로_행을_추가할_수_없습니다/img_1.png)
처음 바인딩 후 동작

단, 이상한 현상이 발생했습니다

처음 데이터 바인딩 이후에는 잘 추가가 되는데 한번 바인딩이 된 이후에 데이터가 재 바인딩 되면 MaxRow를

찾기 못하고 추가가 되지 않는 현상이 발생합니다

![](/assets/images/c_컨트롤이_데이터_바인딩된_경우에는_datagridview의_행_컬렉션에_프로그래밍_방식으로_행을_추가할_수_없습니다/img_2.png)
재바인딩 후 동작

음...뭐가 문제인지 모르겠지만 구문을 다시 한번 바꾸어 봤습니다

폼의 상단에 DataTable를 선언합니다

    
    
    private DataTable dt;

조회되는 부분에서는 프로시져만 호출하고 바인딩 시킵니다

    
    
    private void Load()
            {
                string query = "EXEC SP_SHIP_DELIVERY_LIST";
                query += "           'SELECT',";                         //구분
                query += "           '" + textBox1.Text + "',";          //Cust_Code
                query += "           '" + textBox3.Text + "',";          //Delivery_Code
                query += "           '" + textBox2.Text + "',";          //Part_Code
                query += "           '" + textBox4.Text + "',";          //Cust_GridNo
                query += "           '',";                               //Part_Name
                query += "           '',";                               //Active
                query += "           ''";                                //Remark
                SAC_MesDB db = new SAC_MesDB();
    
                dataGridView1.DataSource = db.ExcuteQuery(query);
    
                dataGridView1.Columns[0].ReadOnly = true;
                dataGridView1.Columns[1].ReadOnly = true;
                dataGridView1.Columns[2].ReadOnly = true;
    
            }

Row 추가 이벤트 구문에서 DataTable를 선언하고 Row 추가 이후에 DataTable에 신규 Row를 추가 합니다

    
    
            private void hoverGradientButton3_Click(object sender, EventArgs e)
            {
                int MaxRow = dataGridView1.Rows.Count;
    
                if (MaxRow >= 0)
                {
                    if (dataGridView1.Rows[MaxRow - 1].Cells[0].Value.ToString() != "")
                    {
                        dt = new DataTable();
                        dt = dataGridView1.DataSource as DataTable;
                        string[] row0 = { "", "", "", "", "", "", "" };
                        dt.Rows.Add(row0);
                        dataGridView1.DataSource = dt;
                        
                        dataGridView1.Rows[dataGridView1.Rows.Count - 1].Cells[0].Style.BackColor = Color.Yellow;
                        dataGridView1.Rows[dataGridView1.Rows.Count - 1].Cells[1].Style.BackColor = Color.Yellow;
                        dataGridView1.Rows[dataGridView1.Rows.Count - 1].Cells[2].Style.BackColor = Color.Yellow;
                    }
                    else
                    {
                        MessageBox.Show("추가 등록은 한번에 하나씩만 가능합니다.");
                    }
                }
            }

이렇게 변경하고 실행을 해 보았습니다

![](/assets/images/c_컨트롤이_데이터_바인딩된_경우에는_datagridview의_행_컬렉션에_프로그래밍_방식으로_행을_추가할_수_없습니다/img_3.png)

역시 처음 바인딩시에는 정상적으로 잘 되는것을 확인했습니다

다음은 재바인딩 후에 실행해 보겠습니다

![](/assets/images/c_컨트롤이_데이터_바인딩된_경우에는_datagridview의_행_컬렉션에_프로그래밍_방식으로_행을_추가할_수_없습니다/img_4.png)

정상적으로 추가되는 모습을 확인할 수 있습니다

이렇게 동일한 방식으로도 어는 위치에서 동작하는지에 따라 문제가 될 수 있다는걸 알 수 있는 계기였습니다ㅎ

(이걸 찾아내는냐고 2시간을 버렸네요..ㅠ)

![](/assets/images/c_컨트롤이_데이터_바인딩된_경우에는_datagridview의_행_컬렉션에_프로그래밍_방식으로_행을_추가할_수_없습니다/img_5.png)
문제없이 디버깅 통과 모습

저와 같은 문제로 고민 하는 분이라면 이렇게 DataTable 위치를 변경해서 구동 해 보시기 바랍니다

  

#C# 오류 #그리드뷰바인딩오류 #Row추가 #그리드뷰 Row 추가하기 #행 컬렉션에 프로그래밍 방식으로 행을 추가할 수 없습니다


</div>
<div class="lang-panel lang-en" lang="en">
(*No embedded English lines found. Add translations later.*)

</div>
