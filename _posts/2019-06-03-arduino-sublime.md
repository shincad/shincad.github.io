---
layout: post
title:  "arduino IDE, 넌 너무 폰트가 싫어!"
date:   2019-06-03
comments: true
categories: arduino
---

arduino를 본격적으로 한번 해 보고 싶은데, 개발환경이며 특히 폰트... 정말로 꿀꿀하다. 좀 더 예쁘게 만들었으면 좋으련만... 그래서 다른 에디터를 쓰기로 했다. 저번에 설치했던 sublimetext3 ~ 요건 볼 때마다 뭔가 프로그램을 짜고 싶은 생각이 들게하는 에디터이다. 다 좋은데, 수정하고 바로 컴파일, 업로드하면 좋으련만.

그게 불편하다. 앗~ 하지만 된다. 그 기능이 된다. 약간의 설정만 해 주면 된다.

저번에 sublimetext3를 설치한 것을 기억하는가? 저번에 설치 안 했다면,  땜쟁이 포스팅 [mac에서 sublimetext3 설치](https://shincad.github.io/web/mac/2019/05/27/sublimetext.html) 편을 봐라. 설치가 됐다는 가정하에 설명한다.

그냥은 안된다. 세상에는 참 훌륭한 사람들 많다. 누가 또 훌륭하게 sublimetext3에서 arduino를 직접 컴파일, 업로드가 가능하도록 package화 했다. 대단하다. 

[stino download site](https://github.com/Robot-Will/Stino)

 위의 링크를 눌러보면 stino라는 github로 접속이 된다. 여기 들어가서 stino를 다운받는다.

![sublime-text-3 0](https://user-images.githubusercontent.com/20354551/58773375-c6c92c80-85f7-11e9-94ab-843326cb76d0.png)

위의 화면을 보면 설치하기 전 sublime text3이다. 맨 우측 메뉴가 Help이다. 

자, 그러면 arduino를 위한 메뉴를 설치해 보자.

![menu](https://user-images.githubusercontent.com/20354551/58773484-29bac380-85f8-11e9-85df-530ae3d84826.PNG)

preferences --> browse packages를 선택하면, 윈도우 창이 하나 나온다. 바로 package 들을 설치할 때 저장하는 방이다. 여기에 아까 다운받은 stino를 압축을 풀어서 넣는다. (간단하다. mac도 동일하게 하면 된다.)

그리고 sublime text3를 닫았다가 다시 실행한다.

![menu2](https://user-images.githubusercontent.com/20354551/58773681-f7f62c80-85f8-11e9-95ea-8928c8281de9.PNG)

어떤가? arduino menu가 생겼다. 컴파일도, 로딩도, 업로드도 된다. 훌륭하다. 위의 화면은 저번에 실험해봤던 blink.ino를 로딩한 화면이다. 폰트도 예쁘고, 아주 좋다. 프로그램하고 싶은 마음이 용솟음친다.

