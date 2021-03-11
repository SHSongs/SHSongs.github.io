---
layout: post
title: "How to use Docker2"
date: 2021-03-11
excerpt: "Docker"
tag:
- docker
category: [ others ]
feature: ../assets/img/title/basic.jpg
comments: true
---

docker container는 삭제되면 container 내부의 복구할 수 없다.  
docker container에서 작업한 것을 OS로 가져오고 싶다면 어떻게 해야 될까?  
 
container 내부에 깃을 설치해 원격 저장소에 푸쉬할 수 도 있고  

OS 내부 저장소의 한 폴더를 container의 한 폴더와 연결시킬 수도 잇고 (바인드 마운트)  

도커에서 권장하는 방법인 볼륨을 사용 할 수도 있다.  

이번엔 가장 간단하고 쉽운 방법인 바인드 마운트를 이용해 OS와 연결 해 보자  


일단 OS의 /home/unreal/python/hello.py를 docker container에서 실행시키고 싶다.  
<img src="/Images/Other/Docker2/00.png" height="400">  

이럴때는 docker run 할때 -v 라는 tag를 이용해 python 폴더를 docker container 내부의 한 폴더와 mapping 시킬 수 있다.  

  
-v /home/유저/app:/app  
-v `pwd`:/app  
<img src="/Images/Other/Docker2/02.png" height="400">  
이런식으로 콜론 ( : ) 앞은 OS 뒤는 컨테이너의 내용을 쓴다. 이런 방법은 포트를 맵핑할때도 동일하다.  


이번에 도커의 src폴더에서 docker_hello.py 를 생성해보고 OS의 /home/unreal/python 폴더를 확인해보자.  
docker에서 exit을 하지말고 터미널을 하나 더 접속해서 확인하면 편하다.  
<img src="/Images/Other/Docker2/03.png" height="400">  


### 다음 글

docker port forwarding  