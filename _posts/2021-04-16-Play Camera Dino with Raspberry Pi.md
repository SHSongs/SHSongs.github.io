---
layout: post
title: "Play Camera Dino with Raspberry Pi"
date: 2021-04-16
excerpt: " Raspberry Pi에서 Camera Dino 시간측정(FPS)"
tag:
- Vision
- OpenCV
category: [ Artificial Intelligence ]
feature: ../assets/img/title/basic.jpg
comments: true
---


### Play Camera Dino with Raspberry Pi


라즈베리파이에서의 디노 시간 측정  


VNC를 이용해 진행하였는데 속도에 영향을 받을 수도 있다.  


그리고 기존 라즈베리파이 고장으로 새로운 라즈베리파이로 성능측정을 진행했는데 한 달간 공룡 게임을 실행했었던 라즈베리파이보다 조금 더 빨랐다.  

또한 해상도를 낮추면 더욱 성능이 향상되리라 생각한다.  

FPS(Frame Per Second)는 while 루프를 도는 시간을 측정한 후  
```
1 / 도는 시간
```
을 하여 FPS를 구했다.  

------
평소  20FPS  
![](/Images/AI/DinoTime/01_Original.png)  

Spacebar 누르는 코드 작동시 10FPS  
![](/Images/AI/DinoTime/02_PyGame.png)  

[PyGame Dino](https://github.com/shivamshekhar/Chrome-T-Rex-Rush) OpenSource 50FPS  

[PyGame Dino](https://github.com/shivamshekhar/Chrome-T-Rex-Rush) + 점프감지코드 16FPS  


간단하게 FPS 측정을 해 보았고  
optical flow 코드는 그냥 가져다 썼는데 더 공부한 후 지금 상황에 맞는 코드를 작성해야 한다.