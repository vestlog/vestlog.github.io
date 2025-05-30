---
title:  "[2019-09-19] - [C#] CallBack 함수와 Delegate 사용하기"
categories:
  - Blog
tags:
  - "프로그래밍"
  - "RFID"
  - "delegate"
  - "c#"
  - "코딩"
  - "Callback"
  - "RFID"
  - "대리자"
  - "Soket"
  - "이더넷통신"
last_modified_at: 2025-05-30T16:03:55+09:00
---

## [C#] CallBack 함수와 Delegate 사용하기

코딩정보/C#

2019-09-19 09:18:39

* * *

안녕하세요

코딩하는남자의 코딩연습생입니다

프로그래밍을 하다보면 CallBack 함수를 사용해야 되는 상황이 발생합니다

예를들면 Soket통신을 구현할때 수신/응답을 비동기식으로 구현해야할 경우가 이에 해당하죠

Soket 통신의 원리르 보면 이더넷 환경의 장비에 응답코드를 송신하여 그에 해당하는 결과 값을 받아오게 되죠

이경우 두가지 형식으로 구현을 합니다 동기식/비동기식.

동기식은 송신후 응답코드가 수신될때까지 멈춰 대기 하게 됩니다

구현할려는 장비와 운영 방법에 따라 즉시 응답이 가능하다면 동기식으로 구현하는것이 맞겠죠

하기만 한번에 여러대의 장비와 통신을 해야 하는 경우 혹은 수신까지 걸리는 ReadTime이 길 경우에는 무한정

기다릴수 만은 없기 때문에 비동기식 구현 방법을 사용 합니다

비동기식은 동기식과 반대로 응답코드를 송신하고 수신이 올때까지 다른 대기자가 대기하고 다른 프로세스를 실행 할 수 있죠

비동식에서 사용해야 하는 "대리자"가 바로 이번 작성할려는 주제입니다

CallBack 함수를 사용할려면 누군가는 항상 값을 받을 준비를 하고 있어야 합니다

그 대리자가 Delegate 입니다

이번 C#으로 RFID 통신을 구현하면서 사용한 Source Code의 일부를 가지고 설명을 해드릴께요

1\. Delegate 선언

\- RFID Tag와 Reader간 통신을 하면서 Reader가 Tag의 값을 읽기 전까지 무한 대기 합니다

\- 그후 선언된 Delegate를 통해 Tag가 읽히게 되면 나머지 프로세서를 처리하게 되는 구조 입니다

\- Delegate선언 방법은 간단합니다

    
    
    //delegate 선언
    //CallBack Fucntion 타입 정의
    public delegate void OnSendToRFIDDelegate(int nCmdID, byte[] bBuf, int nSize, string sDump);
    public delegate void OnReceiveFromRFIDDelegate(int nCmdID, byte[] bBuf, int nSize, string sDump);
    public delegate void OnAddRFIDMsgDelegate(string sMsg);
    public delegate void OnRFIDExceptionDelegate();
    
    //CallBack 호출을 위한 전역함수 정의
    Public OnSendToRFIDDelegate OnSendToFRID;
    public OnReceiveFromRFIDDelegate OnReceiveFromRFID;
    public OnAddRFIDMsgDelegate OnAddRFIDMsg;
    public OnRFIDExceptionDelegate OnRFIDException;

다음과 같이 Delegate를 선언하고 그 Delegate 호출을 위한 전역함수를 선언합니다

그리고 Soket 통신을 위한 구문을 작성하죠.

    
    
    private byte[] RcvBuf = new byte[4096];
    byte[] sndBuf = new byte[12];
    
    using(Socket socket = new Socket(AddressFamily.interNetwork, SocketType.Stream, ProtocolType.Tcp))
    {
    	EndPoint plcEP = new IPEndPoint(IPAddress.Parse("IP주소"), 포트번호);
        
        socket.Connect(plcEP);
        socket.Send(sndBuf);
        
        //Delegate 사용
        if(OnSendToRFID != null)
        	OnSendToRFID(CurCmd, SndBuf, 12, DumpBytes(sndBuf, 12));
            
        int nRecv = 0;
        
        nRecv = socket.Receive(RcvBuf);
        
        //Delegate 사용
        if(OnReceiveFromRFID != null)
        	OnReceiveFromRFID(CurCmd, RcvBuf, nRecv, DumpBytes(RcvBuf, nRecv));
        
        socket.Close();
    }

운영 원리는 다음과 같습니다 Socket으로 접속하여 송신 응답 메세지를 보낸뒤 대리자를 선언하여 대리자가 null이 아닐때까지 By
Psss 되고 null이 아닌 값이 들어오게 되면 대리자를 호출하여 처리 요청을 한뒤 바로 다름 응답코드를 수신할 수 있도록 운영합니다.

해당 글은 필자가 개인적인 코딩 연습을 위한 구현이므로 실제 정의와는 다른 의미가 있을 수 있으니

참고하시기 바랍니다

  

#프로그래밍 #RFID #delegate #c# #코딩 #Callback #RFID Reader #대리자 #Soket #이더넷통신

