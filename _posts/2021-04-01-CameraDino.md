---
layout: post
title: "Camera Dino"
date: 2021-03-25
excerpt: "Optical flow를 활용해 Chorme Dino 게임 하기"
tag:
- Vision
- OpenCV
category: [ Artificial Intelligence ]
feature: ../assets/img/title/basic.jpg
comments: true
---

[Github Source](https://github.com/SHSongs/CameraDino)  

## Optical Flow

<figure class="half">
    <a href="/Images/AI/Dino/01_Opticalflow.jpg"><img src="/Images/AI/D/Images/AI/Dino/01_Opticalflow.jpg"></a>
    <a href="/Images/AI/Dino/02_Opticalflowjpg.jpg"><img src="/Images/AI/Dino/02_Opticalflowjpg.jpg"></a>
    <figcaption>출처 https://docs.opencv.org/3.4/d4/dee/tutorial_optical_flow.html</figcaption>
</figure>

Optical flow (광학 흐름)  
물체의 움직임 패턴.  
동작 추정과 영상 압축에 주로 쓰인다.  


이를 이용하면 측정 방향으로 움직이는 것을 감지해서  
조작을 해 게임을 플레이 할 수 있다.   

나는 Optical flow를 이용해 크롬 Dino 게임을 하겠다.  


## 카메라로 Dino Play하기

Optical flow를 한 후  

```py
nextPts, status, err = cv2.calcOpticalFlowPyrLK(prevImg, nextImg, prevPts, nextPts, criteria)
```

```
- prevImg: 이전 프레임 영상
- nextImg: 다음 프레임 영상
- prevPts: 이전 프레임의 코너 특징점, cv2.goodFeaturesToTrack() 로 검출
- nextPst: 다음 프레임에서 이동한 코너 특징점
- status: 결과 상태 벡터, nextPts와 같은 길이, 대응점이 있으면 1, 없으면 0
- err: 결과 에러 벡터, 대응점 간의 오차
- criteria: 반복 탐색 중지 요건 
```

```py
prevMv = prevPt[status == 1]  
nextMv = nextPt[status == 1]  
```

prevMv과 nextMv 의 차를 구하면 운동량을 구할 수 있습니다.  
```py
vec = prevMv - nextMv
```


<figure class="half">
    <a href="/Images/AI/Dino/03_01Prev.jpg"><img src="/Images/AI/Dino/03_01Prev.jpg"></a>
    <a href="/Images/AI/Dino/03_02Next.jpg"><img src="/Images/AI/Dino/03_02Next.jpg"></a>
    <a href="/Images/AI/Dino/03_03Vec.jpg"><img src="/Images/AI/Dino/03_03Vec.jpg"></a>
    <figcaption>출처 https://docs.opencv.org/3.4/d4/dee/tutorial_optical_flow.html</figcaption>
</figure>

vec 을 0차원을 기준으로 평균을 내  

vec의 평균 운동량을 구해줍니다.  

```py
vec = np.mean(vec, axis=0)
```

vec[1] 즉, y축의 운동량 Threshold(임계값)을 넘어가면  
JumpCnt를 늘려주고  

```py
if vec[1] > (Threshold+0.3 ) * (1/jumpcnt):
            #print(vec[1])  
            jumpcnt += 1
        else:
            jumpcnt = np.clip(jumpcnt - 1, 1, 5)
```
JumpCnt가 n(특정값)을 넘으면 Jump 처리합니다. 여기서는 pynput을 이용해 spacebar를 눌러준다.  

```py
if jumpcnt > 3:
            print('jump')
            jumpcnt = 1
            press_space()
```

여기서 Threshold는 vec[1]의 평균값 + alpha 를 해 구해준다.  

```py
Threshold = np.mean(np.array(buffer))
```

### [Github Source](https://github.com/SHSongs/CameraDino)  
