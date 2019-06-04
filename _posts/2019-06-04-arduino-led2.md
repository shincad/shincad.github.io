---

layout: post
title:  "근데 보통 보던 LED랑 모양이 다르네??"
date:   2019-06-04
comments: true
categories: arduino

---

저번 내용을 보면 땜쟁이가 7개까지 LED를 솔더링했다. 그 전에 사진을 보신 분을 알겠지만, 맨날 보던 큰 LED랑 모양이 다르다. 작다. 그리고, 저항도 1KOhm을 달았다고 하는데 눈에 안 보인다. (색띠가 많은 저항이 왜 안 보일까?)

![](https://user-images.githubusercontent.com/20354551/58851481-e5015c00-86cd-11e9-8ce9-98cb981c6d1a.jpg)

위의 사진을 잘 봐라. Blue LED 크기가 무지 작다. 저거 뭐지? 우리가 맨날 보던 LED는 다음과 같다.

![Unknown](https://user-images.githubusercontent.com/20354551/58885820-d17de180-871d-11e9-884e-5b721b0dcb18.jpg)

요거다. Dip Type LED이다. 요건 사이즈도 크고, 땜쟁이가 사용한 Type 보다는 전력 소비도 좀 크다. 그리고, 결정적인 이유는 사무실에 DIP Type LED가 별로 없어서, 다음과 같은 Type을 썼다.

![Led_SMD_encendido](https://user-images.githubusercontent.com/20354551/58886132-5a951880-871e-11e9-8a16-fd7cbd4325d7.jpg)

SMD Type LED이다. 흔히 여러분들이 쓰시는 휴대폰이나 각종 전자제품에 아주 많이 사용된다. 사이즈가 작아서 소형기기에 많이 사용된다. 

<img width="190" alt="스크린샷 2019-06-04 오후 11 17 38" src="https://user-images.githubusercontent.com/20354551/58886514-fde62d80-871e-11e9-8531-219a1b0f6f8b.png">

저항도 보통은 이런 DIP type을 많이 봤을 것이다. 하지만, 땜쟁이는 이거보다 작은 저항을 사용했다. 바로 저항도 SMD Registor를 사용했다. 

![330_ohm_1%_SMD_0603_resistor_1](https://user-images.githubusercontent.com/20354551/58886737-51587b80-871f-11e9-81a6-28e7b297dee3.jpg)

이것이 SMD Type 저항이다. 이것도 소형가전제품이나 여러분들의 휴대폰에 엄청 들어간다.

저번에 봤던 Fade source를 타이밍을 약간 변경해 봤다.

[![Video Label](http://img.youtube.com/vi/UlVZxXTEEYw/0.jpg)](https://youtu.be/UlVZxXTEEYw)

가운데 1개가 심장박동처럼 움직인다.

여러분들도 Arduino sketch에 있는 예제 중에서 fade.ino의 타이밍을 약간 변경해 본 것이다. 여러분들도 실험을 해 보면서 변경해 보자. 자 오늘은 여기까지~