---
layout: post
title:  "Dos prompt에서 usb printer로 데이터 전송방법"
date:   2020-04-01
comments: true
categories: companywork
---

* 요즘은 프린터들이 대부분 usb아니면 network 이다. 옛날 프린터 개발할 때에는 lpt나 serial 밖에 없었는데, 참 편한 세상이다. 그런데, 요게 dos prompt에서 데이터를 전송하려면 좀 문제가 있다. 직접 전송이 안된다. 그래서 편법을 좀 써야한다. network으로 전송하는 것 처럼 해야한다. 먼저 프린터 드라이버를 설치하고나서 그 프린터를 네트워크 공유를 잡아줘야한다.

![공유화면](https://user-images.githubusercontent.com/20354551/78090545-623c5100-7405-11ea-9897-9ffb53fe79e6.PNG)

요런식으로~! 중요하다. 이거 안하면 인쇄할 방법이 없다.

이렇게하고나서,

```
net use lpt2 \\127.0.0.1\giant-100
```

요렇게 해주면 공유된 프린터가 lpt2로 mapping된다.

그 다음,

```
copy /b test.txt lpt2
```

이렇게 하면 데이터가 프린터로 휘익~! 날라간다. 되는가? 안되면 첨 부터 다시 해봐라~!