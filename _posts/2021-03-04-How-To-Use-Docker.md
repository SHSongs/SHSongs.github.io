---
layout: post
title: "How to use Docker"
date: 2021-03-04
excerpt: "Docker"
tag:
- docker
category: [ others ]
feature: ../assets/img/title/basic.jpg
comments: true
---

관련글
- [Docker](https://shsongs.github.io/Docker/)  
- [How-To-Use-Docker](https://shsongs.github.io/How-To-Use-Docker/)  
- [How-To-Use-Docker2](https://shsongs.github.io/How-To-Use_Docker2/)  


이글은 도커를 사용하는 방법을 쓴 글이다.  
- Linux에서 도커를 설치하고 계정을 docker 그룹에 추가했다고 가정한다.  
- Ubuntu 18.04.5 LTS, putty를 이용해 SSH로 접속했다.  
  

도커로 파이썬하고 bash를 써보자  

google에 docker python을 검색하면  
[https://hub.docker.com/_/python](https://hub.docker.com/_/python)  
이 사이트가 상단에 뜨는 것을 볼 수 있다.  


<img src="/Images/Other/Docker/01.png" height="400">  
docker pull python  
이 명령어를 이용해 파이썬 이미지를 받을 수 있는것을 알 수 있다.  



이미지는 설치 파일이라 생각하면 쉽다.  
<figure class="half">
    <img src="/Images/Other/Docker/02.png">
    <img src="/Images/Other/Docker/03.png">
    <figcaption>다양한 설치파일들, 언제든지 초기 상태로 돌아갈 수 있게 해준다.</figcaption>
</figure>
  

웹페이지를 밑으로 내리다 보면 태그를 이용해 python 버전을 선택할 수 있는것을 알 수 있다.  
<img src="/Images/Other/Docker/03_1.png" height="400">  
python:<버전>  

```
docker pull python:3.6.11  
```
로 python 3.6.11 이미지를 받아보자  
<img src="/Images/Other/Docker/04.png" height="400">  

docker images로 방금 받은 이미지를 확인할 수 있다.  
<img src="/Images/Other/Docker/05.png" height="400">  


이 이미지를 컨테이너로 만들어야 한다.  
컨테이너는 이미지를 기반으로 만들어지고 OS와 독립된 환경에서 프로그램을 실행할 수 있게 해준다.  
<img src="/Images/Other/Docker/06.png" height="400">  
```
docker run -it python:3.6.11 /bin/bash  
```
-it 은 터미널에서 docker를 사용할 수 있게 해준다.  
/bin/bash 는 bash를 실행 시켜 터미널로 docker와 소통을 할 수 있게 해준다.  
python을 쓰면 python이 실행된다.  

이 명령어를 실행하면 os와 격리된 환경에서 bash 프로그램을 실행해 격리된 환경에서 파이썬을 사용할 수 있다.  


한번 테스트해보자  
```
python
```
<img src="/Images/Other/Docker/07.png" height="400">   

```
exit() 으로 Container 내부의 python을 종료시킬 수 있다.  
```
ssh와 거의 비슷하게 할 수 있다.  
<img src="/Images/Other/Docker/09.png" height="400">  


exit을 하면 컨테이너가 종료된다.  
<img src="/Images/Other/Docker/10.png" height="400">  


docker ps -a 로 모든 컨테이너를 확인 할 수 있다.  
<img src="/Images/Other/Docker/11.png" height="400">  

## 다음글
컨테이너에서 작업한 내용물을 OS에서 보는 방법 (마운트)  
포트 맵핑 
