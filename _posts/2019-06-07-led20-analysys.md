---
layout: post
title:  "knight rider 분석해보자."
date:   2019-06-07
comments: true
categories: arduino
---

무지하게 복잡하게 되어 있는 거 같다. 너무 어렵다.근데 실행해보면 멋있다. 내부 구조를 알고 싶은데, 어렵다. 하나씩 해보면 하나도 안 어렵다. 하나씩 보자.

```c
void setup() {
    for (uint8_t pin=0; pin<20; ++pin) {
        pinMode(pin, OUTPUT);
    }
}

uint8_t brightness(const int8_t led, const int8_t pos) {    
    switch (abs(led-pos)) {
        case 0:     return 128;
        case 1:     return 64;
        case 2:     return 32;
        case 3:     return 16;
        case 4:     return 6;
        case 5:     return 2;
        default:    return 1;
    }
}

void pulse_width_modulation(const uint8_t pos) {
    for(uint8_t times=0; times<3; ++times) {
        for (uint8_t pass=0; pass<128; ++pass) {
            for (int8_t led=0; led<20; ++led) {
                digitalWrite(led, (brightness(led, pos) > pass));
            }
        }
    }
}

void loop() {
    static uint8_t pos=0;

    while(pos<20) {
        pulse_width_modulation(pos);
        ++pos;
    }

    while(pos>0) {
        --pos;
        pulse_width_modulation(pos);
    }
}
```

하나씩 분석해 본다.

우리가 LED를 20개 달았다. 0부터 19까지 20개.



```
void setup() {
    for (uint8_t pin=0; pin<20; ++pin) {
        pinMode(pin, OUTPUT);
    }
}
```

초기화 부분이다. 포트 20개를 출력으로 초기화 한다. 이건 당연한 거니, 모르는 분 없을 것이다.

```
void loop() {
    static uint8_t pos=0;

    while(pos<20) {
        pulse_width_modulation(pos);
        ++pos;
    }

    while(pos>0) {
        --pos;
        pulse_width_modulation(pos);
    }
}
```

loop 부분이다. C언어의 main에 해당되는 부분이다. 여기서 다 생각하지 말고, 하나씩 보자.

먼저 pos이라는 변수를 static으로 선언하고 여기에 0을 지정했다.

그 다음 while문을 돌렸다. pos가 19가 될 때까지.

그 다음 pulse_width_modulation함수로 진입, 물론 pos는 계속 0이란 값을 가지고, 함수로 진입한다.

(여기까지는 다들 잘 이해 하셨으리라 본다.)

```
uint8_t brightness(const int8_t led, const int8_t pos) {    
    switch (abs(led-pos)) {
        case 0:     return 128;
        case 1:     return 64;
        case 2:     return 32;
        case 3:     return 16;
        case 4:     return 6;
        case 5:     return 2;
        default:    return 1;
    }
}

void pulse_width_modulation(const uint8_t pos) {
    for(uint8_t times=0; times<3; ++times) {
        for (uint8_t pass=0; pass<128; ++pass) {
            for (int8_t led=0; led<20; ++led) {
                digitalWrite(led, (brightness(led, pos) > pass));
            }
        }
    }
}
```

자, 나머지 부분이다. 여기가 제일 어렵다. (뭐, 하나씩 뜯어보면 어렵지 않다.)

위에서 본 것처럼, pos가 0이란 값을 가지고, pulse_width_modulation 함수로 진입했다.

안에 들어가니, for문이 3개 있다.

자 첫번 째 for문은 times가 0부터 시작하니, times=0인 상태로, 두번 째 for문에 진입해보자.

두번째 for문은 pass라는 값을 가지고 시작한다. 이것도 pass=0인 상태로 3번째 for문으로 진입한다.

3번째 for문을 보면 led=0부터 시작해서, led가 19까지 증가하도록 되어있다. 

하나씩 해 보면, led=0일 때, digitalWrite(0, (brightness(0,0)>0)); 이렇게 실행이 된다.

digitalWrite(0  <-- 요 부분은 led 0 즉, 제일 첫번째 led를 지정하는 것이고,

brightness(0,0)은 말 그대로, 다시 brightness라는 함수를 호출 했다.

그 안으로 다시 들어가 보자.

```
uint8_t brightness(const int8_t led, const int8_t pos) {    
    switch (abs(led-pos)) {
        case 0:     return 128;
        case 1:     return 64;
        case 2:     return 32;
        case 3:     return 16;
        case 4:     return 6;
        case 5:     return 2;
        default:    return 1;
    }
}
```

 

led = 0 , pos = 0

이므로, switch(abs(0-0))이고 abs 함수는 절대값을 구하는 것이니, 0-0 = 0이 되어, case 0 --> 128 이라는 값을 리턴한다. 

다시 pulse_width_modulation 함수로 돌아오면,

digitalWrite(0,(brightness(0,0)>0))); ---> digitalWrite(0,(128>0)); --> digitalWrite(0,1); 이렇게 된다.

128>0 이게 왜 1이 되냐고? 128>0은 참이니까, 1

128<0 된다면, 거짓이니까, 0

자 그러면, 결국, led 0는 1이 되면서, led 0에 불이 들어올 것이다. 불한번 켜기 참 어렵다.

이 logic을 결국 하나하나 추적해서 값을 대입해보면 다음과 같다.

pass==0 일 때

| 19   | 18   | 17   | 16   | 15   | 14   | 13   | 12   | 11   | 10   | 9    | 8    | 7    | 6    | 5    | 4    | 3    | 2    | 1    | 0    |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| 1    | 1    | 1    | 1    | 1    | 1    | 1    | 1    | 1    | 1    | 1    | 1    | 1    | 1    | 1    | 1    | 1    | 1    | 1    | 1    |



pass==1 일 때

| 19   | 18   | 17   | 16   | 15   | 14   | 13   | 12   | 11   | 10   | 9    | 8    | 7    | 6    | 5    | 4    | 3    | 2    | 1    | 0    |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 1    | 1    | 1    | 1    | 1    | 1    |



pass==2,3,4,5 일 때

| 19   | 18   | 17   | 16   | 15   | 14   | 13   | 12   | 11   | 10   | 9    | 8    | 7    | 6    | 5    | 4    | 3    | 2    | 1    | 0    |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 1    | 1    | 1    | 1    | 1    |



pass==6,7,8,9,10,11,12,13,14,15 일 때

| 19   | 18   | 17   | 16   | 15   | 14   | 13   | 12   | 11   | 10   | 9    | 8    | 7    | 6    | 5    | 4    | 3    | 2    | 1    | 0    |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 1    | 1    | 1    | 1    |



pass==16부터 31 일 때

| 19   | 18   | 17   | 16   | 15   | 14   | 13   | 12   | 11   | 10   | 9    | 8    | 7    | 6    | 5    | 4    | 3    | 2    | 1    | 0    |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 1    | 1    | 1    |



pass==32부터 63 일 때

| 19   | 18   | 17   | 16   | 15   | 14   | 13   | 12   | 11   | 10   | 9    | 8    | 7    | 6    | 5    | 4    | 3    | 2    | 1    | 0    |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 1    | 1    |



pass==64부터 127 일 때

| 19   | 18   | 17   | 16   | 15   | 14   | 13   | 12   | 11   | 10   | 9    | 8    | 7    | 6    | 5    | 4    | 3    | 2    | 1    | 0    |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 1    |



자, 보면, 처음에는 LED가 전부 다 들어오고, 그 다음에는 0부터 5 까지 5개, 그 다음에는 4개, 그 다음에는 3개, 그 다음에는 2개, 마지막으로 1개가 들어온다. 즉, 이 pattern을 만들어 논 상태에서, pos가 이동이 되도록 하면 knight rider 효과가 나타나는 것이다.

arduino 핀 중에는 pwm이 가능한 핀이 있고, pwm 기능이 안돼는 핀이 있다.  전체 20개의 핀을 다 써서, pwm가 비슷한 기능을 구현하려고 하니, 이러한 방법을 구현한 것이다. 

자 그러면 다시 loop routine을 보자.

```
void loop() {
    static uint8_t pos=0;

    while(pos<20) {
        pulse_width_modulation(pos);
        ++pos;
    }

    while(pos>0) {
        --pos;
        pulse_width_modulation(pos);
    }
}
```

while 문에서 pos 값을 하나씩 증가시키면서, 19까지 되도록 했다. 즉, 순차적으로 pattern을 우에서 좌로 이동시키면서, led의 갯수가 마지막에는 소멸하는 느낌처럼 만들어 논 것이다.

위의 루틴을 이렇게 한번 바꿔 보자.

```
void loop() {
    static uint8_t pos=0;

    while(pos<20) {
        pulse_width_modulation(pos);
        ++pos;
    }
	
	if(pos==20)
	{
		pos=0;
	}
  
}
```

자 이렇게 한번 해보고, 업로드 해 보자. 광선총이 나가는 느낌이 날 것이다. 즉, 갔다가 돌아오는 것이 아닌, 계속 앞으로만 갔다가 초기화 되는 느낌이 날 것이다.

[![Video Label](http://img.youtube.com/vi/wn9RFGRWdMw/0.jpg)](https://youtu.be/wn9RFGRWdMw)

화면 클릭~!

자 이 상태에서 실제 신호들은 어떻게 나오는 지 확인해 보자.

```
void loop() {
    static uint8_t pos=0;

    while(pos<20) {
        pulse_width_modulation(pos);
    //    ++pos;
    }
	
  
}
```



pos값을 증가 시키지 않고, pos가 0인 상태에서 각 LED 핀에 신호가 어떻게 가는지 확인해 보자.

[![Video Label](http://img.youtube.com/vi/g7Beo2XCOVk/0.jpg)](https://youtu.be/g7Beo2XCOVk)

화면 클릭~!



LED 상태가 이동되지 않고 고정되어 있는 모습니다. 하지만, 내부적으로는 계속적으로 On/Off를 하고 있다.

![photo_2019-06-07_19-36-41](https://user-images.githubusercontent.com/20354551/59098571-9d8fff80-895b-11e9-8fa4-cf6807e239ee.jpg)

Pin 0 Signal

![photo_2019-06-07_19-36-38](https://user-images.githubusercontent.com/20354551/59098578-a385e080-895b-11e9-8824-f31b9e8f8a20.jpg)

Pin 1 Signal

![photo_2019-06-07_19-36-34](https://user-images.githubusercontent.com/20354551/59098584-a84a9480-895b-11e9-866f-124ae87a0000.jpg)

Pin 2 Signal

![photo_2019-06-07_19-36-32](https://user-images.githubusercontent.com/20354551/59098590-ab458500-895b-11e9-9275-aaff1d7276ca.jpg)

Pin 3 Signal

![photo_2019-06-07_19-36-29](https://user-images.githubusercontent.com/20354551/59098592-ada7df00-895b-11e9-8729-f94997bb16ff.jpg)

Pin 4 Signal

![photo_2019-06-07_19-36-27](https://user-images.githubusercontent.com/20354551/59098595-af71a280-895b-11e9-9a16-31836fed547d.jpg)

Pin 5 Signal

각 핀들의 신호 상태가 보이는 가? 점점 Turn On 되어 있는 신호 폭이 줄어드는 것을 볼 수 있다.

땜쟁이처럼, logic을 분석할 때는 코드를 하나하나 입력해 가면서 분석을 하는 것이 도움이 된다. 

오늘은 여기까지~!

