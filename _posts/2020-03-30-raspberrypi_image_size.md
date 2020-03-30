---
layout: post
title:  "raspberry pi iamge file size 줄이는 방법"
date:   2020-03-30
comments: true
categories: companywork
---

통상적으로 Win32DiskImager로 Backup을 하게되면,  MicroSD Memory Size 그대로 Backup이 되게된다. 안에 실제 내용은 6-7GB 정도이다. 용량으로서도 낭비고, 이걸 다른 MicroSD에 Write할 경우, 일반적으로는 그대로 되지만, 32GB인 경우 Vendor마다 크기가 달라서, Write가 안되는 경우가 많다. 그래서 Backup된 Image 파일을 줄여야 하는데, 이게 생각처럼 쉽지 않다.지금부터 이미지를 줄이는 방법을 하나씩 설명하고자 한다.

![win32image](https://user-images.githubusercontent.com/20354551/61258532-36af0300-a7b1-11e9-9aa7-b1be3e5f9d98.PNG)

먼저 win32DiskImager로 실제 Raspbian이 설치되어 있는 memory를 img 파일로 Backup한다. 

32GB 메모리라면, 32GB로 생성될 것이다. 크기도 크고, 시간도 오래걸린다.

우선, 같은 라즈베리파이에서 할 수 있는 작업을 설명한다.

먼저 단순하게 아무것도 없는 라즈베리파이로 부팅을 하여, 복사하고자 하는 라즈베리파이를 usb로 연결한다.

이렇게 연결하면 대부분 자동으로 마운트 된다.

다음과 같이 df -h 명령을 해보면, 마운트 된 상태가 보인다.

```
root@smartlib:/# df -h
Filesystem      Size  Used Avail Use% Mounted on
/dev/root        11G  5.3G  5.0G  52% /
devtmpfs        459M     0  459M   0% /dev
tmpfs           464M     0  464M   0% /dev/shm
tmpfs           464M  6.5M  457M   2% /run
tmpfs           5.0M  4.0K  5.0M   1% /run/lock
tmpfs           464M     0  464M   0% /sys/fs/cgroup
/dev/mmcblk0p1   41M   23M   18M  56% /boot
tmpfs            93M  4.0K   93M   1% /run/user/1000
/dev/sda1       112G   12G  100G  11% /media/pi/01D53AF90B411520
/dev/sdb1        41M   23M   19M  56% /media/usb0
/dev/sdb2        30G  5.0G   23G  18% /media/usb1
tmpfs            93M  4.0K   93M   1% /run/user/0
root@smartlib:/#

```

이 상태에서 보면, 설명하고자 하는 MicroSDmemory는 /dev/sdb2에 있는 30G 이다. 

파티션 사이즈를 조정하기위해 gparted 라는 프로그램을 설치한다.

![gparted](https://user-images.githubusercontent.com/20354551/61270515-e352aa00-a7dc-11e9-9d85-ab0ad20b8a4f.PNG)

gparted 프로그램을 터미널 창에서 실행하면 다음과 같은 프로그램이 실행된다.

![gparted-1](https://user-images.githubusercontent.com/20354551/61270905-016cda00-a7de-11e9-892e-1751cc4b8d0e.PNG)

이 화면이 gparted가 실행된 화면이다. 여기에서 화면 우측 상단을 보면, /dev/sdb라는 항목이 있다. 

벌써 세팅을 해 놓았지만 df -h에서 본 /dev/sdb항목 부분을 gparted에서 로딩하는 것이다.

우리가 조정을 해야 할 항목은 /dev/sdb2 항목이다. 그냥 바로 Resize는 안된다. 현재 mount되어 있는 것을 풀고(unmount) 조정해야 한다. /dev/sdb2에 마우스를 올리고 오른쪽 버튼을 누르면 unmount 또는 마운트해제가 나온다. 이걸 실행하면 마운트가 해제된다.

![gparted-2](https://user-images.githubusercontent.com/20354551/61271183-dafb6e80-a7de-11e9-9f59-12f65cf6866e.PNG)

사이즈를 조정하는 항목이다. 마우스로 잡아서 내리면 크기가 조정된다. 최소 크기에 10% 정도 여유를 주어야 한다.

조금 넉넉하게 잡아서 조정했다. 조정 후 연두색 check 마크를 누르면 적용이 되면서 사이즈 조정이 시작된다.

![gparted-3](https://user-images.githubusercontent.com/20354551/61272060-26af1780-a7e1-11e9-90c0-6990a68f222d.PNG)

![gparted-4](https://user-images.githubusercontent.com/20354551/61272091-3dee0500-a7e1-11e9-9477-3ec654cf72c9.PNG)

작업 중인 화면.

![gparted-5](https://user-images.githubusercontent.com/20354551/61272122-53fbc580-a7e1-11e9-8b43-1203635d6a67.PNG)

작업이 끝나면 붉은색 표시값을 적어두자. 만약 잊어버렸다면,

sudo fdisk -l

![gparted-6](https://user-images.githubusercontent.com/20354551/61272161-6d9d0d00-a7e1-11e9-9535-aab2e8b0e340.PNG)

이 명령으로 볼 수 있다. 붉은색의 이 2개의 값을 더한다. 

다음과 같이 명령을 내린다.

sudo dd if=/dev/sda of=/media/pi/01D53A....../backup.img  bs=512 count=2개의 더한값

여기서 of은 별도의 외장하드부분을 마운트해서 한 것이다. 상황에 따라 어디로 백업을 할지 사용자마다 다르다.

시간은 한참 걸린다.

백업이 끝나면 이 파일을 별도의 다른 MicroSDmemory에 복원해서 정상적으로 부팅을 확인하면 완료.

참고로 정확하게 계산해서 image를 생성해도 되고, 아래와 같이 대략적인 용량을 감안해서 해도 상관없다.

예를들어 전체용량이 대략 9GB 정도 된다고 가정하면, 넉넉하게 10-11GB정도 감안하여 다음과 같이 image를 생

성해도 무관하다.

sudo dd if=/dev/sda of=/media/pi/test/backup.img bs=100M count=100

이렇게 하면 대략 10GB 정도의 image가 생성된다.

df -h에서 ntfs로 포맷된 외장하드에 이미지를 저장하면 편리하다.



