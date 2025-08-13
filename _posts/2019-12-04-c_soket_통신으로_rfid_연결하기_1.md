---
categories:
  - 'Blog'
tags:
  - '통신'
  - 'RFID'
  - 'c#'
  - '모듈'
  - '비동기식'
  - 'Soket'
  - '이더넷통신'
  - 'V680S'
  - '비동기식'
  - 'C#통신모듈'
last_modified_at: '2025-05-30T16:03:55+09:00'
title: '[2025-08-13] - Post'
excerpt: ''
layout: 'post'
lang: 'ko'
permalink: '/posts/2019-12-04-c_soket_통신으로_rfid_연결하기_1/'
alt_en: '/en/posts/2019-12-04-c_soket_통신으로_rfid_연결하기_1/'
---

<div class="lang-panel lang-ko" lang="ko">
## [C#] Soket 통신으로 RFID 연결하기 #1

코딩정보/C#

2019-12-04 13:34:23

* * *

안녕하세요.

코딩하는남자의 코딩연습생입니다

이번 블로그 주제는 C#의 Soket 통신을 이용해서 OMRON RFID V680S 모델과 통신을 해서

단거리 무선 통신을 구현해볼려고 해요

이걸 시도하게 된 계기는 회사에서 진행되는 프로젝트 때문인데요

특정 바구니에 RFID Tag를 달고 임의 위치에 바구니가 사용될 때마다 Tag를 읽어들여

바누니의 현재 상황을 파악하기 위해 구성해봤습니다

현재 프로젝트의 규모는 RFID Reader 20ea + RFID Tag 80ea정도 공사가 진행되었구요

제가 만든 프로그램에서 20개의 Reader를 동시에 제어하여 20곳에 사용될 바구니의 정보를

실시간 습득합니다

전체 SourceCode를 Open할수 있다면 좋을거 같은데 아무래도 상용의 목적으로 구축된 부분이라

일부만 공개할수 있어서 아쉽습니다

혹시 저와 비슷한 프로그램을 목적으로 구성중이시라면 도움이 되셨으면 좋겠습니다

내용이 많아서 이번 블로그에서는 C#으로 소켓 통신 하는 부분만 설명 하겠습니다

[Source Code]

    
    
    using System.Net;
    using System.Net.Sockets;
    
    
    public class AsynchronousClient
    {
        private Socket rfSocket = null;
        private EndPoint rfEP;
        private ManualResetEvent connectDone = new ManualResetEvent(false);
        private ManualResetEvent DisconnectDone = new ManualResetEvent(false);
        private ManualResetEvent sendDone = new ManualResetEvent(false);
        private ManualResetEvent receiveDone = new ManualResetEvent(false);
    
        private string response = string.Empty;
    
    
    
        private int pByteSize = 0;
        private int pWordSize = 0;
    
    
    
    public void StartClient()
    {
        connectDone.Reset();
       DisconnectDone.Reset();
    
       try
       {
          rfSocket = new Socket(AddressFamily.InterNetwork, SocketType.Stream, ProtocolType.Tcp);
          rfEP = new IPEndPoint(IPAddress.Parse(RFIDIP), RFIDPORT);
    
          connectDone.Reset();
          rfSocket.BeginConnect(rfEP, new AsyncCallback(ConnectCallback), rfSocket);
          connectDone.WaitOne();
       }
       catch (Exception e)
       {
          Console.WriteLine(e.ToString());
       }
    }
    
    
    
    private void Disconnect()
    {
          if((rfSocket != null) && (rfSocket.Connected))
          {
              DisconnectDone.Reset();
              rfSocket.Shutdown(SocketShutdown.Both);
              rfSocket.BeginDisconnect(true, DisconnectCallback, rfSocket);
          }
          else
         {
             StartClient();
         }
    
    }
    
    
    
    private void ConnectCallback(IAsyncResult ar)
    {
        connectDone.Set();
    
        try
        {
           Socket client = (Socket)ar.AsyncState;
           client.EndConnect(ar);
    
          Send();     
          Receive();
        }
        catch (Exception e)
       {
          Console.WriteLine(e.ToString());
          Disconnect();
       }
    }
    
    
    
    private void DisconnectCallback(IAsyncResult ar)
    {
        DisconnectDone.Set();
    
        try
        {
           Socket client = (Socket)ar.AsyncState;
           client.EndDisconnect(ar);
           client.Close();
        }
        catch (Exception e)
        {
           Console.WriteLine(e.ToString());
        }
    
           StartClient();
    }
    
    
    
    private void Receive()
    {
        try
        {
           rfSocket.BeginReceive(StateObject.buffer, 0, StateObject.BufferSize, 0,
    
                                        new AsyncCallback(ReceiveCallback), rfSocket);
        }
        catch (Exception e)
        {
           Console.WriteLine(e.ToString());
           Disconnect();
           return;
        }
    }
    
    
    
    private void ReceiveCallback(IAsyncResult ar)
    {
        try
        {
            Socket client = (Socket)ar.AsyncState;
            client.EndReceive(ar);
    
        }
    
        catch (Exception e)
        {
            Console.WriteLine(e.ToString());
            if (rfSocket.Connected)
               Send();
            else
               StartClient();
            return;
        }
    }
    
    
    
    private void Send()
    {
         try
        {
            if ((rfSocket != null) && (rfSocket.Connected))
            {
                   rfSocket.BeginSend(CurrfidCommand(), 0, CurrfidCommand().Length, 0,
    
                                            new AsyncCallback(SendCallback), rfSocket);
            }
        }
        catch (Exception e)
        {
           Console.WriteLine(e.ToString());
           Disconnect();
        }
    }
    
    
    
    public void Reset_Send()
    {
        try
        {
             if ((rfSocket != null) && (rfSocket.Connected))
             {
                    rfSocket.BeginSend(ResetCommand(), 0, ResetCommand().Length, 0,
    
                                             new AsyncCallback(SendCallback), rfSocket);
              }
        }
        catch (Exception e)
        {
            Console.WriteLine(e.ToString());
            Disconnect();
        }
    }
    
    
    
    private void SendCallback(IAsyncResult ar)
    {
         try
        {
              Socket client = (Socket)ar.AsyncState;
    
              int bytesSent = client.EndSend(ar);
    
              sendDone.Set();
    
        }
        catch (Exception e)
        {
              Console.WriteLine(e.ToString());
              Disconnect();
              return;
        }
    }
    
    }

해당 위의 Source Code는 비동기식 Soket 통신입니다

그래서 BeginConnect(), BeginReceive(), BeginSend()를 사용합니다

해당 공개한 Source Code를 응용해서 비동기식 Soket 통신 모듈을 직접 개발하여 이더넷 여러 기기와

통신이 가능한 프로그램 제작을 시도해 보시면 좋을거 같습니다

이어 두번째 영상에는 현재 만들어진 비동기식 Soket 프로그램을 통해 OMRON RFID V680S 모델과

통신하는 방법에 대한 글을 이어서 작성하도록 하겠습니다

  

#통신 #RFID #c# #모듈 #비동기식 #Soket #이더넷통신 #V680S #비동기식 Soket통신 #C#통신모듈


</div>
<div class="lang-panel lang-en" lang="en">
(*No embedded English lines found. Add translations later.*)

</div>
