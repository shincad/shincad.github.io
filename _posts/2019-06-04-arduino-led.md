---
layout: post
title:  "귀찮아도 달아보자. LED~"
date:   2019-06-04
comments: true
categories: arduino
---

귀찮다고 아무 것도 안하면, 아무 것도 안된다. 

자, 한번 달아보자. LED. 

보통 다들 설명할 때, **브레드보드(BreadBoard)**, 일명 빵판을 이용한다. 바로 연결하기 쉽고, 분해도 쉽고. 근데, 땜쟁이는 빵판이 지금 없다. 업으로 하다보니, 빵판을 쓸일이 별로 없다. 

![만능기판](https://user-images.githubusercontent.com/20354551/58850633-53dcb600-86ca-11e9-95f9-289be383997c.PNG)



위의 사진 같은 보드를 본 적 있는가? **만능기판**이라고 하는 건데, 보통 개발 당 시 테스트 회로등을 구성해서 여기에 실제 wrapping wire로 결선을 해서 만든다. 이 작업을 할 때는 잡념이 싹~ 사라진다. 오로지 이것만 보인다. 머리안에서는 회로를 어느 쪽으로 돌릴 것인지, 설계한 회로 형태로 제대로 구성이 되고 있는 지 여러가지 생각을 하면서 작업을 하다보니, 잡념이 싹 사라진다. 

![DSC_0062](https://user-images.githubusercontent.com/20354551/58850911-889d3d00-86cb-11e9-90b0-b174490d6242.JPG)

요런 식으로 한다. 신입사원 때 욕 무지하게 먹으면서 연습많이 했다. 흡사 외과의사가 점점 성장하는 것처럼..

그 때는 열심히 했는데, 근 20년 이상을 해 오고 있는지라, 이제는 좀 귀찮다. 막상 하면 재미 있기는 한데, 발동이 걸리기 까지 시간이 좀 걸린다.

참고로 breadboard도 사진을 올린다.

![Electronics-White-Breadboard](https://user-images.githubusercontent.com/20354551/58851062-37da1400-86cc-11e9-91ee-f5414d4a7a75.jpg)

요건 대학교 때, 많이 썼다. 초보자들이 쓰기에는 참 좋다.

자, 빵판 없으니 땜쟁이는 그냥 만든다. 여러분들이 뭐라하더라도 방법이 없다. 빵판 준비되면 그 때 빵판으로 다시 하겠다.

먼저 저번에 이야기 했던, PWM 실험까지 해 보기 위해서, PWM까지 가능한 6번핀에 하나만 먼저 연결을 하겠다. PWM 모른다고? 땜쟁이 **[요부분](<https://shincad.github.io/arduino/2019/06/03/arduino-fade-pwm.html>)**을 클릭해서 보고와라. 물론 저항도 하나 붙여야 한다. 안 그러면 LED 탄다. 왜 붙이는 지는 저번에 이야기 했다. 또 모르는 분은 [요부분](<https://shincad.github.io/arduino/2019/06/01/arduino-5.html>) 보고 와라.

![photo_2019-06-04_13-28-33](https://user-images.githubusercontent.com/20354551/58851328-42e17400-86cd-11e9-939d-c7f62b19e962.jpg)

아두이노 우노 위에 헤더를 장착했다. 위에 보드를 하나 달아서, LED 붙이려고 구상했다. 

![photo_2019-06-04_13-28-36](https://user-images.githubusercontent.com/20354551/58851383-80de9800-86cd-11e9-89b1-159ac56bb9aa.jpg)

가지고 있는 만능 기판이 너무 커서 잘랐다. 옆면은 그라인더로 잘 갈았다. 이게 밥줄이다 보니, 땜쟁이는 장비가 꽤 있다. 

![photo_2019-06-04_13-28-40](https://user-images.githubusercontent.com/20354551/58851413-a7043800-86cd-11e9-9209-b8f91afc6417.jpg)

위에 보드를 얹어서 **솔더링(땜질)**을 했다. 자, 하나 달아보자.

![photo_2019-06-04_13-28-42](https://user-images.githubusercontent.com/20354551/58851481-e5015c00-86cd-11e9-8ce9-98cb981c6d1a.jpg)

하나 달아서 예제 한번 돌려 봤다. 이거 회로도가 궁금하다고? 간단하다.

회로도를 그려서 설명을 해야 하는데, 땜쟁이는 회사에서는 **OrCAD**를 사용한다. 이건 일반인들은 살 수 없는 어마어마한 금액이다. 그리고, 기능도 많아서 설명하기가 어렵다. KiCAD나 EagleCAD등 여러가지 툴도 있지만, 이것들도 초보자 입장에서는 사용하기가 쉽지 않다. 그래서 찾아본 결과, **Fritzing**에서 만든 초보자용 툴이 있었다. 첨 봤다. 무척 흥미로운 툴이다. 이걸로 땜쟁이는 설명을 할 까 한다. (표현하기 어려운 것은 어쩔 수 없이 OrCAD 같은 Tool을 사용한다.)

[fritzing Site](http://fritzing.org/download/)

여기들어가서 다운 받으면 된다. 사이즈가 무척크다. 설치도 아니고, 그냥 압축 풀어서 실행한다. 엄청나다. 사양이 안좋은 PC는 실행도 안될 것 같다. (땜쟁이 노트북도 벌써 7년이나 돼서, 넘 느리다.)

느리지만 겨우겨우 설치했다. 우선 빵판에다가 하는 것 처럼 해 보았다.

![face-bread](https://user-images.githubusercontent.com/20354551/58853562-b8514280-86d5-11e9-9aa4-a8c9428842ed.PNG)

간단하다. 저항값은 **1KOhm**으로 했다. 좀 높게 잡은이유는 요 LED 하나만 할 것이 아니라, 지금부터 LED를 좀 많이 붙일 생각이다. **전류량을 제한**하려면 이렇게 해야한다. 

![fade-sch](https://user-images.githubusercontent.com/20354551/58853605-d8810180-86d5-11e9-801f-35c5d61c0a95.PNG)

요게 회로도 이다. fritzing은 회로도도 귀엽다. 자, 그러면  동영상 한번 보자.

[![Video Label](http://img.youtube.com/vi/KZuh8WjzvwE/0.jpg)](https://youtu.be/KZuh8WjzvwE)

화면 클릭~!

그냥 깜박깜박 하는거랑 다르다. 크리스마스 트리처럼 천천히 켜지고, 천천히 꺼진다. 이게 **PWM**이다. 뭔가 감이오는 가?

감이 안오는 분들을 위해, 그냥 **On/Off** 동영상 나간다.

[![Video Label](http://img.youtube.com/vi/I6OJRZWipEY/0.jpg)](https://youtu.be/I6OJRZWipEY)

자~ 완전히 다르지 않은가? 이것이 그냥 On/Off이다.

자 그럼 귀찮지만, 좀 더 붙여보자.  이번에는 7개 이다.

![photo_2019-06-04_13-28-46](https://user-images.githubusercontent.com/20354551/58854032-1f232b80-86d7-11e9-84fe-205379b08ace.jpg)

좀 더 붙였다. 요걸로 좌우로 LED가 scroll하는 걸 한번 해 보겠다.

공고 강의때 만들었던 소스이다. 간단하게 구현했다.

```c
/*----------------------------------------*/
/* LED Scroll Program for Arduino Uno     */
/* 2012.10.10                             */
/* Written by jwshin(infiniteloop)        */
/*----------------------------------------*/


// --------------------------- LED Pattern Definition 
unsigned char pattern_table[] = {
    0x7F, /* 01111111 */
    0x3F, /* 00111111 */
    0x1F, /* 00011111 */
    0x8F, /* 10001111 */
    0xC7, /* 11000111 */
    0xE3, /* 11100011 */
    0xF1, /* 11110001 */
    0xF8, /* 11111000 */
    0xFC, /* 11111100 */
    0xFE, /* 11111110 */
    0xFC, /* 11111100 */
    0xF8, /* 11111000 */
    0xF1, /* 11110001 */
    0xE3, /* 11100011 */
    0xC7, /* 11000111 */
    0x8F, /* 10001111 */
    0x1F, /* 00011111 */
    0x3F, /* 00111111 */
    255
};

//------------------------------- LED Scroll Delay
unsigned int delay_table[] =
{
    90,
    70,
    50,
    40,
    40,
    40,
    40,
    50,
    70,
    90,
    70,
    50,
    40,
    40,
    40,
    40,
    50,
    70,
    0 
};

//----------------- variable for led count 
int LedCnt;

void setup()
{
    DDRD = B11111111;      // PORTD Initialization  (OUTPUT)
}

void loop()
{
    if(delay_table[LedCnt] > 0)
    {
        PORTD = ~pattern_table[LedCnt];
        delay(delay_table[LedCnt]);
        LedCnt++;
    }
    else 
    {
        LedCnt = 0;
    }
}
```

소스는 그저 단순한 것이 최고다. 아주 단순하게 했다. 요걸 업로드하면 다음과 같이 된다.

[![Video Label](http://img.youtube.com/vi/lPV56SrvBsM/0.jpg)](https://youtu.be/lPV56SrvBsM)

화면 클릭~!

자~! 좌우로 이동하는 것이 보이는 가? 오늘은 여기까지~! 다음 편에서 좀 더 LED를 붙인다. 기대하라.
