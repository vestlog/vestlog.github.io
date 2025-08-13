---
categories:
  - 'Blog'
tags:
  - '통신'
  - 'RFID'
  - 'c#'
  - '비동기'
  - 'OMRON'
  - 'V680S'
  - 'soket통신'
last_modified_at: '2025-05-30T16:03:56+09:00'
title: '[2025-08-13] - Post'
excerpt: ''
layout: 'post'
lang: 'ko'
permalink: '/posts/2019-12-13-c_soket_통신으로_rfid_연결하기_2/'
alt_en: '/en/posts/2019-12-13-c_soket_통신으로_rfid_연결하기_2/'
---

<div class="lang-panel lang-ko" lang="ko">
## [C#] Soket 통신으로 RFID 연결하기 #2

코딩정보/C#

2019-12-13 09:31:31

* * *

안녕하세요

코딩하는남자 코딩연습생입니다

이번 블로그 내용은 저번 시간에 작성했던 비동기 Soket 통신을 이용해서

[OMRON] RFID Reader V680S 모델과 실질적인 통신 구현 방법과

V680S 통신 명령어에 대해 작성해 보도록 하겠습니다

참고로 저도 C# 언어로 회사일을 하고 있지만 코딩이라는게 손 놓으면 금방 까먹고

실력이 늘지 않아서 자기 개발을 위해 연습하고 기록하고 있습니다

제가 올린 게시글을 보고 연습하시다 혹시 잘 안되시거나 문제가 있을 경우 댓글 남겨주시면

제가 아는 범위 내에서 같이 공부 하는것도 나쁘지 않을거 같습니다

그럼 다시 이어서 저번 시간 게시 했던 비동기 Soket 구현 방법으로 구현한 프로젝트에

이어서 설명을 할거라서 혹시 이전글을 못 보신분들은 이건글을 확인 한뒤에 이어 가시면 될거 같습니다

<https://codingman.tistory.com/24>

[ [C#] Soket 통신으로 RFID 연결하기 #1 안녕하세요. 코딩하는남자의 코딩연습생입니다 이번 블로그 주제는 C#의 Soket
통신을 이용해서 OMRON RFID V680S 모델과 통신을 해서 단거리 무선 통신을 구현해볼려고 해요 이걸 시도하게 된 계기는 회사에서
진.. codingman.tistory.com ](https://codingman.tistory.com/24)

아 참고로 게시글을 읽다 보면 SourceCode 부분에 자꾸 자동 광고가 삽입되어서

난감하던 찰라에 "코드블럭"이란 기능이 있다는걸 이제야 알게 되었습니다ㅎㅎ

앞으로 좀 더 편하게 보실 수 있도록 글쓰기 연습을 많이 하겠습니다

C#으로 비동기식 Soket을 구현하셨다면 이번에는 [OMRON] RFID V680S에 대해 알아야 하는데요

이더넷 통신이 가능한 RFID Reader로 명령어를 Send해서 Resceive받아 내는 형식으로 동작 합니다

좀 더 자세한 이해를 위해서는 V680S 모델의 매뉴얼을 보시는게 좋은데요

이것 또한 제 블로그에 기재 했으니 검색 or 링크를 통해 한번 읽어 주시면 되겠습니다

<http://htps://codingman.tistory.com/23>

불러오는 중입니다...

매뉴얼까지 읽어 보셨다면 지금 부터 설명 드리는것에 대한 이해가 빠르실겁니다

비동기식 Soket 통신의 시작으로 BeginConnect()를 실행시키고 나면

Callback이 실행 되면서 Send() 명령어를 처음에 타게 됩니다

이런 구조의 이유는 V680S의 교신 방식 때문인데요 매뉴얼을 읽어 보시면 V680S의 교신 방법이

3가지가 있습니다

첫번째는 1회성 교신

두번째는 자동 교신

세번째는 FIFO. 트리거 교신

![](/assets/images/c_soket_통신으로_rfid_연결하기_2/img.jpg)

교신 방법별 특징은 매뉴얼에 상세히 나와 있으니 참고 하시면 될거 같구요

![](/assets/images/c_soket_통신으로_rfid_연결하기_2/img_1.jpg)

이런식으로 V680S는 교신 이후 교신처리 단계를 거치게 됩니다

즉, 명령어로 "너 읽어라"라는 신호를 주기 전까지는 대기를 한다는 뜻입니다

그래서 V680S에게 "너 읽어라"라는 명령어를 주기 위해 처음 Send를 보내게 됩니다

Send부분에서는 Byte형식의 Buffer 배열을 V680S로 명령어를 전송 줍니다

    
    
    byte[] sndBuf = new byte[12];
    sndBuf[0] = 0x00;   // 트랜잭션 식별자 상위
    sndBuf[1] = 0x00;   // 트랜잭션 식별자 하위
    sndBuf[2] = 0x00;   // 프로토콜 식별자 상위
    sndBuf[3] = 0x00;   // 프로토콜 식별자 하위
    sndBuf[4] = 0x00;   // 필드길이 상위
    sndBuf[5] = 0x06;   // 필드길이 하위
    sndBuf[6] = 0xFF;   // 유니트 식별자 (고정)
    sndBuf[7] = 0x03;   // 펑션코드
    sndBuf[8] = 0x00;   // (byte)((nAdr & 0xFF00) >> 8);       // 레지스터번호 상위
    sndBuf[9] = 0x00;   // (byte)(nAdr & 0x00FF);              // 레지스터번호 하위
    sndBuf[10] = (byte)((pWordSize & 0xFF00) >> 8); // 워드카운트 상위
    sndBuf[11] = (byte)(pWordSize & 0x00FF);        // 워드카운트 상위

이런 형식의 Buffer를 생성하는 이유는 V680S가 알아 듣는 형식이 이렇기 때문이에요

![](/assets/images/c_soket_통신으로_rfid_연결하기_2/img_2.jpg)

자 이렇게 메뉴얼에 나와 있듯이 V680S는 Hex값을 분석하여 지금 나의 행동을 파악하게 되는 구조입니다

C#에서 Hex값을 만들기위해 저는 Byte형식을 사용한 것입니다

자 이렇게 읽어와라는 명령어를 Send()를 통해 전달을 하게 되면 V680S는 RFID Tag를 읽어 들여 Receive하게

그럼 당연히 Callback에서 Send 호출이후에는 당연히 Receive를 해야겠죠?

Receive역시 저는 비동기식 Soket을 구현하였기 때문에 BeginReceive로 사용합니다

BeginReceive를 호출하게 되면 역시 Callback을 호출하게 되구요

    
    
    private void Receive()
            {
                try
                {
                    rfSocket.BeginReceive(StateObject.buffer, 0, StateObject.BufferSize, 0, new AsyncCallback(ReceiveCallback), rfSocket);
                }
                catch (Exception e)
                {
                    Console.WriteLine(e.ToString());
                    Disconnect();
                    return;
                }
            }

Receive 코드는 이렇습니다

그 다음 ReceiveCallback에서는 V680S에게 리턴 받은 값을 처리하는 구문을 작성하면 됩니다

이해가 좀 되셨나요??

나름 자세히 설명한다고 했는데 처음에는 저도 많이 해매면서 공부한것이라

정리를 하면

1\. V680S와 Soket통신을 구현하고

2\. V680S에게 Send를 통해 명령어를 전달하고

3\. V680S의 리턴값을 받아 저장 또는 출력을 시킨다

이렇게 됩니다

해당 글을 읽으면서 시도하시다 막히는 부분이나 이해가 되지 않는 부분은 댓글 남겨주시면

제가 아는 범위에서 성심껏 답변드리도록 하겠습니다

감사합니다~

  

#통신 #RFID #c# #비동기 #OMRON #V680S #soket통신


</div>
<div class="lang-panel lang-en" lang="en">
(*No embedded English lines found. Add translations later.*)

</div>
