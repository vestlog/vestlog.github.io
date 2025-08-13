---
categories:
  - 'Blog'
tags:
  - '파이썬'
  - '파이썬'
  - 'kivy'
  - 'kivy'
last_modified_at: '2025-05-30T16:04:12+09:00'
title: '[2025-08-13] - Post'
excerpt: ''
layout: 'post'
lang: 'ko'
permalink: '/posts/2021-04-19-python_kivy_키비_실행_시키기/'
alt_en: '/en/posts/2021-04-19-python_kivy_키비_실행_시키기/'
---

## [PYTHON] Kivy[키비] 실행 시키기

2021-04-19 08:43:03

* * *

안녕하세요

코딩연습생입니다~

저번 포스팅에서 Kivy[키비]를 설치하는 방법을 포스팅 했는데요

<https://codingman.tistory.com/242>

[ [PYTHON] KIVY 윈도우환경에서 설치하기 안녕하세요 코딩연습생입니다 하 요즘은 24시간이 부족하네요ㅎㅎㅎ 주식 분석용 AI도
관리하고..블로그 포스팅.. 가상화폐 자동 매매 봇..ㅎㅎㅎ 이번생 한번 잘 살아볼려고 정말 아둥바둥 하네
codingman.tistory.com ](https://codingman.tistory.com/242)

이번 시간에는 정상적으로 Kivy[키비]가 설치 되었는지 확인 하기 위한

파이썬으로 키비 실행시키기 입니다

저도 초보자라서 하나씩 검색해서 실행시키고 그걸 기록하고 있는 단계라서ㅎㅎ

여러분도 같이 하나씩 따라 하시면서 연습하시면 좋을거 같습니다

일단 파이썬 샘플 소스입니다

    
    
    import kivy
    from kivy.app import App
    from kivy.uix.label import Label
    
    kivy.require('1.11.1')
    
    class TestApp(App):
        def build(self):
            return Label(text='Hello World.')
    
    if __name__ == '__main__':
        TestApp().run()

Kivy(키비)를 호출하여 Label에 Hello World(가장 기초)를 띄우는 소스입니다

만약 저번 포스팅에서 정상적으로 설치가 되셨다면 아래와 같이

실행되는 모습을 보실수 있습니다

![](/assets/images/python_kivy_키비_실행_시키기/img.png)

이렇게 Kivy[키비] 준비를 하고 아래와 같이 최종 실행이 됩니다

![](/assets/images/python_kivy_키비_실행_시키기/img_1.png)

  

#파이썬 키비 #파이썬 Kivy #kivy 실행하기 #kivy hello world

