---
categories:
  - 'Blog'
tags:
  - '공동개발'
  - '소스공유'
  - '팀'
  - 'visual'
  - 'live'
  - '비쥬얼스튜디오'
last_modified_at: '2025-05-30T16:03:59+09:00'
title: '[2025-08-13] - Post'
excerpt: ''
layout: 'post'
lang: 'ko'
permalink: '/posts/2020-01-16-visual_studio_2017_live_share_기능_사용하기/'
alt_en: '/en/posts/2020-01-16-visual_studio_2017_live_share_기능_사용하기/'
---

<div class="lang-panel lang-ko" lang="ko">
## [Visual Studio 2017] Live Share 기능 사용하기

코딩정보/IT 프로그램

2020-01-16 08:40:04

* * *

안녕하세요

비쥬얼 스튜디오 2017부터 확장 기능으로 사용가능한 Live Share 기능을 살펴보고

적용하는 방법에 대해 포스팅 해보도록 하겠습니다

일단 Live Share 기능에 대해 좀 설명을 드리자면

하나의 프로젝트를 열어서 팀원들과 공동 작업이 가능하고 팀원별 변경 이력과

팀원간 음성을 통해 뭔가 협력하는것이 가능하게 해주는 기능이라고 합니다

어떻게 보면 중요하지 않다고 생각하실수도 있지만 다른 면으로 보자면

소스 수정을 할 때 원격 교육이나 대규모 프로젝트 진행시 매우 유용하게 사용할 수 있는

핵심 기능이 되기 때문에 어떤 면에서는 상항히 중요한 기능이라고 생각할 수도 있습니다

Visual Studio 2019에서는 기본 기능으로 탑재되어 배포 되어지고 있는 Live Share 기능을

우리는 Visual Studio 2017에서 확장 적용을 하여 사용해 보도록 하겠습니다

[적용 방법]

1\. 비쥬얼 스튜디오 2017을 관리자 권한으로 실행하기

(저는 윈도우10 환경에서 진행 하였습니다)

![](/assets/images/visual_studio_2017_live_share_기능_사용하기/img.jpg)

2\. 관리자 권한으로 비쥬얼 스튜디오 2017이 실행이 되었다면

도구 -> 확장 및 업데이트를 통해 Live Share를 설치 합니다

![](/assets/images/visual_studio_2017_live_share_기능_사용하기/img_1.jpg)

3\. 확장 및 업데이트에서 Live Share를 검색 하는 방법은 아래 이미지를 참고하세요

![](/assets/images/visual_studio_2017_live_share_기능_사용하기/img_2.jpg)

\- 온라인 -> 검색창("Live Share") 입력 후 검색

![](/assets/images/visual_studio_2017_live_share_기능_사용하기/img_3.jpg)

4\. 다운로드 버튼을 클릭하여 설치 하기

![](/assets/images/visual_studio_2017_live_share_기능_사용하기/img_4.jpg)

\- 설치가 완료되면 아래 이미지와 같이 아래쪽 노란색 문구가 나타납니다

![](/assets/images/visual_studio_2017_live_share_기능_사용하기/img_5.jpg)

5\. 비쥬얼 스튜디오 2017을 종료하고 나면 자동으로 기능 확장 설치가 진행 됩니다

(컴터 사양에 따라 다소 늦게 설치가 진행 될 수 있으니 조금 기다리시기 바랍니다)

![](/assets/images/visual_studio_2017_live_share_기능_사용하기/img_6.jpg)

\- 설치를 위한 초기화 진행

![](/assets/images/visual_studio_2017_live_share_기능_사용하기/img_7.jpg)

\- 수정 버튼을 클릭하여 설치 진행을 계속 진행합니다

![](/assets/images/visual_studio_2017_live_share_기능_사용하기/img_8.jpg)

\- 수정 버튼 클릭 이후 별도 클릭 없이 자동 설치가 진행 되니 좀만 기다리시면 됩니다

![](/assets/images/visual_studio_2017_live_share_기능_사용하기/img_9.jpg)

\- 계속 기다리시면 됩니다

![](/assets/images/visual_studio_2017_live_share_기능_사용하기/img_10.jpg)

\- 설치 중

![](/assets/images/visual_studio_2017_live_share_기능_사용하기/img_11.jpg)

\- 설치가 완료 되어지면 위의 이미지와 같이 완료 글이 보이면서 닫기 버튼이 나타납니다

6\. Live Share 기능을 좀 더 확장성 있게 사용하기 위해서 환경설정을 변경 해줍니다

도구 -> 옵션 클릭

![](/assets/images/visual_studio_2017_live_share_기능_사용하기/img_12.jpg)

\- 옵션에서 Live Share -> 일반 -> 게스트 제한 증가 속성 변경, 게스트 제어 허용 속성 변경

![](/assets/images/visual_studio_2017_live_share_기능_사용하기/img_13.jpg)

\- 공동 편집 기능 옵션 확인

![](/assets/images/visual_studio_2017_live_share_기능_사용하기/img_14.jpg)

7\. Live Share가 정상 설치가 되었다면 비쥬얼 스튜디오 메인 화면 우측 상단에 다음과 같은 버튼이 생성 됩니다

![](/assets/images/visual_studio_2017_live_share_기능_사용하기/img_15.jpg)

8\. 버튼을 눌러 Live Share를 활성화 시켜줍니다

![](/assets/images/visual_studio_2017_live_share_기능_사용하기/img_16.jpg)

9\. 활성화가 완료가 되어지면 초대 가능한 URL 링크 주소가 나타나면서 Live Share 창이 생성됩니다

![](/assets/images/visual_studio_2017_live_share_기능_사용하기/img_17.jpg)

초대 URL를 통해 접속 하실수 있는데 이때 주의사항은 참여 할려는 사용자 역시 Live Share가 설치가 되어

있어야 참여가 가능하다는 점입니다

참여 하실려는 곳에도 똑같은 방법으로 Live Share를 설치 하신뒤 URL 링크를 통해 접속하시면

공동 소스 코드 수정이 가능하게 되어지며 원격으로 빌드 실행도 가능해 집니다

  

#공동개발 #소스공유 #팀 프로젝트 #visual studio 2017 #live share #비쥬얼스튜디오 확장 기능


</div>
<div class="lang-panel lang-en" lang="en">
(*No embedded English lines found. Add translations later.*)

</div>
